## Install common packages
```
sudo apt-get update
sudo apt-get install -y curl git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev zsh vim
```

## Install Yarn
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt update && sudo apt install yarn
```

## Setup Oh My Zsh
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
/Note/: Type Y then press [Enter] if get the prompt.
## Install Ruby and Rails
```
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.zshrc
exec $SHELL

rbenv install 2.6.6
rbenv global 2.6.6

echo "gem: --no-document" >> ~/.gemrc

gem install bundler
rbenv rehash
gem install rails
rbenv rehash
```
## Install MySQL
```
sudo apt-get install mysql-server mysql-client libmysqlclient-dev
```
/Note/: If get any prompt, just press [Enter] to continue.

## Install PostgreSQL
```
sudo apt install postgresql postgresql-contrib
```

## Install NodeJS
```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```
## Config Git
```
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com"
```
/Note/: If get any prompt, just press [Enter] to continue.
## Config to connect to MySQL Server without sudo permission (If needed)
```
sudo mysql -uroot

DROP USER 'root'@'localhost';
CREATE USER 'root'@'%' IDENTIFIED BY '';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

quit
```
