## POST
curl --data "param1=value1&param2=value2" https://example.com/resource.cgi

curl --form "fileupload=@my-file.txt" https://example.com/resource.cgi

curl --form "fileupload=@my-file.txt;filename=desired-filename.txt" --form param1=value1 --form param2=value2 https://example.com/resource.cgi

curl --data '' https://example.com/resource.cgi

curl -X POST https://example.com/resource.cgi

curl --request POST https://example.com/resource.cgi

For large files, consider adding parameters to show upload progress:
curl --tr-encoding -X POST -v -# -o output -T filename.dat http://example.com/resource.cgi
The -o output is required, otherwise no progress bar will appear.

## GET
curl -u admin:admin https://example.com/resource.cgi


curl --data "{'email' : 'test@book.com','message' : 'Hi this is first message of APIs'}" http://localhost:1337/message

## DELETE
curl -X DELETE http://localhost:1337/crawlprocess/2

curl --data "url=http://localhost:8080" http://localhost:1337/summary/full

## Submit a file
curl -F 'zip=template1.zip' url

## Virus total example
curl -v --request POST --url 'https://www.virustotal.com/vtapi/v2/url/scan' -d apikey=apik -d 'url=http://www.ftfgastonia.com/index.php'