# Commands used

## File Permission Issues on Mac

- Change ownership:
```
sudo chown <user-name>:<group-name> -R <file-path>
```
- Change permission:
```
sudo chmod 755 -R <file-path>
```


## Install Composer (Linux)
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
composer
```

## Install Drush (Linux)
```
wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar
chmod +x drush.phar
sudo mv drush.phar /usr/local/bin/drush
drush init
```

## Install Drupal Console (Linux)
```
curl https://drupalconsole.com/installer -L -o drupal.phar
php drupal.phar
sudo mv drupal.phar /usr/local/bin/drupal
chmod +x /usr/local/bin/drupal
drupal init
```

## Install Node.js and npm
```
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
sudo apt-get install build-essential
sudo apt-get install build-essential libssl-dev
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh -o install_nvm.sh
bash install_nvm.sh
source ~/.profile
nvm ls-remote
nvm install 8.10.0
nvm use 8.10.0
node -v
```

## Install Electron
```
npm install -g electron
git clone https://github.com/electron/electron-quick-start
cd electron-quick-start
npm install && npm start
```

## Install Angular CLI
```
npm install -g @angular/cli
ng -v
ng new my-angular-app
cd my-angular-app
ng serve --open
ng build --prod --base-href /mentor/ --aot
```
