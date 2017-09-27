##install 
npm -g install sails

## create a project
sails new <testProject>

## start 
sails lift
//At this point, if you visit (http://localhost:1337/) you will see the default home page.

## generate api	
sails generate api <APIname>

### create a message
 curl --data "email=test@book.com&message=Hi this is first message of APIs" http://localhost:1337/message