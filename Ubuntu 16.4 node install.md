# Ubuntu 16.4 

## node installation

sudo apt-get install python-software-properties

curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

sudo apt-get install nodejs

## Mongo

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927

echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

sudo apt-get update

sudo apt-get install -y mongodb-org

cd /lib/systemd/system/
nano mongod.service

------------
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target
Documentation=https://docs.mongodb.org/manual

[Service]
User=mongodb
Group=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target
-------------

sudo systemctl daemon-reload

sudo systemctl start mongod
sudo systemctl enable mongod

## other things

sudo apt-get install make g++ python
sudo npm install gulp gulp-cli -g

npm install -g node-gyp

npm uninstall gulp-imagemin

npm install gulp-imagemin

sudo npm install pm2 -g

cp credentials.json dist/