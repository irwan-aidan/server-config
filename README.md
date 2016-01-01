brew update && brew upgrade
brew tap homebrew/dupes
brew tap homebrew/php
brew install --without-apache --with-fpm --with-mysql php56
mkdir -p ~/Library/LaunchAgents
ln -sfv /usr/local/opt/php56/homebrew.mxcl.php56.plist ~/Library/LaunchAgents/
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php56.plist
lsof -Pni4 | grep LISTEN | grep php

brew install mysql
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
mysql_secure_installation

sudo cp -v /usr/local/opt/nginx/*.plist /Library/LaunchDaemons/
sudo chown root:wheel /Library/LaunchDaemons/homebrew.mxcl.nginx.plist

mkdir -p /usr/local/etc/nginx/logs
mkdir -p /usr/local/etc/nginx/sites-available
mkdir -p /usr/local/etc/nginx/sites-enabled
mkdir -p /usr/local/etc/nginx/conf.d
mkdir -p /usr/local/etc/nginx/ssl
sudo mkdir -p /var/www

sudo chown :staff /var/www
sudo chmod 775 /var/www

sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.nginx.plist

launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php56.plist
