
## specify an alternate path for data files using the --dbpath option to mongod.exe,
C:\mongodb\bin\mongod.exe --dbpath d:\test\mongodb\data

## start
mongod

## connect
mongo

##  name of the current database
db

## display the list of databases
show dbs

## Switch to a new database
use mydb

## Create two documents named j and k
j = { name : "mongo" }
k = { x : 3 }

## Insert the j and k documents into the testData collection
db.testData.insert( j )
db.testData.insert( k )

## List collections
show collections

db.sites.find({url:"www.example.com"})

db.sites.updateOne({url:"www.example.com"},{ $set:{url:"example.com"}})