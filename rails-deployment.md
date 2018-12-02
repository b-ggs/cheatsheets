# https://gorails.com/deploy/ubuntu/18.04

sudo adduser deploy
sudo adduser deploy sudo
su deploy
cd ~

# https://github.com/postmodern/ruby-install
wget -O ruby-install-0.6.1.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.1.tar.gz
tar -xzvf ruby-install-0.6.1.tar.gz
cd ruby-install-0.6.1/
sudo make install

ruby-install ruby-2.5.1

sudo apt-get install -y dirmngr gnupg
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
sudo apt-get install -y apt-transport-https ca-certificates

sudo sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger bionic main > /etc/apt/sources.list.d/passenger.list'
sudo apt-get update

sudo apt-get install -y nginx-extras libnginx-mod-http-passenger

if [ ! -f /etc/nginx/modules-enabled/50-mod-http-passenger.conf ]; then sudo ln -s /usr/share/nginx/modules-available/mod-http-passenger.load /etc/nginx/modules-enabled/50-mod-http-passenger.conf ; fi
sudo ls /etc/nginx/conf.d/mod-http-passenger.conf

sudo service nginx start

sudo /usr/bin/passenger-config validate-install

sudo vim /etc/nginx/conf.d/mod-http-passenger.conf

===
passenger_ruby /home/deploy/.rbenv/shims/ruby; # If you use rbenv
# passenger_ruby /home/deploy/.rvm/wrappers/ruby-2.1.2/ruby; # If use use rvm, be sure to change the version number
# passenger_ruby /usr/bin/ruby; # If you use ruby from source
===

sudo service nginx restart

sudo apt-get install mysql-server mysql-client libmysqlclient-dev

mysql
CREATE USER 'deploy'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'deploy'@'localhost';
FLUSH PRIVILEGES;

mysql -u deploy
SET PASSWORD = 'password';

https://github.com/postmodern/chruby/wiki/Passenger

