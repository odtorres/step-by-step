
# create
stout create --bucket my.website.com --key MY_AWS_KEY --secret MY_AWS_SECRET

# deploy
stout deploy --bucket my.website.com --key MY_AWS_KEY --secret MY_AWS_SECRET

# deploy with directory
stout deploy --bucket my.website.com --key MY_AWS_KEY --secret MY_AWS_SECRET --root ./build

# If you don't want to deploy all the files in your folder
stout deploy --bucket my.website.com --key MY_AWS_KEY --secret MY_AWS_SECRET --root ./build --files "*.html,images/*"

# The deploy command will give you a deploy id you can use in the future to rollback
stout rollback --bucket my.website.com --key MY_AWS_KEY --secret MY_AWS_SECRET 1234

# the deploy.yaml
----
default:
  root: 'build/'

production:
  key: 'XXX'
  secret: 'XXX'
  bucket: 'eager.io'

dev:
  key: 'XXX'
  secret: 'XXX'
  bucket: 'next.eager.io'
----
deploy --env development


stout deploy --bucket ilovekickboxingarlingtontx.com --key 1234 --secret 1234 --region us-east-2