
## get metadata
curl -T EN-OscarDanielTorres.docx http://192.168.101.100:9998/meta --header "Accept: application/json"

## get text of the file 
curl -T EN-OscarDanielTorres.docx http://192.168.101.100:9998/tika/main --header "Accept: text/plain"

## MIME/media type Detector
curl -X PUT --upload-file EN-OscarDanielTorres.docx http://192.168.101.100:9998/detect/stream

## Language Resource
curl -X PUT --data-binary @EN-OscarDanielTorres.docx http://192.168.101.100:9998/language/stream

## Translation
curl -X PUT --data-binary @sentences http://192.168.101.100:9998/translate/all/org.apache.tika.language.translate.Lingo24Translator/es/en lack of practice in Spanish

## Rmeta
curl -T test_recursive_embedded.docx http://192.168.101.100:9998/rmeta