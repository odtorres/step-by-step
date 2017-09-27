# PM2

## install
npm install pm2 -g 

## start an app 
pm2 start app.js -n name

## Monitoring all processes launched
pm2 monit

## List all processes
pm2 list

## Act on them
pm2 stop    
pm2 restart 
pm2 delete 

## show information
pm2 show name

## show logs
pm2 logs name --lines 1000