Intension of this repo is to make zappa deployment agnostic of your machine  
Lambda are  deployed on docker based on lambdaci in aws, we are building stuff on that

Steps to achieve this

1) this will create a docker image name zappashell on your machine

```bash
docker build -t zappashell -f zappa-dockerfile .
```

2) now add this to your .bash_profile

```bash
alias zappashell='docker run -ti -e AWS_PROFILE=$AWS_PROFILE -v $(pwd):/var/task -v ~/.aws/:/root/.aws  --rm zappashell bash'
```

what it will do is it will mount current directory and aws credential directory into the docker


3) go to your zappa directory(containing zappa_settings.json) and run (dont forget to source ~/.bash_profile)

```bash
zappashell
```

4) install virtual environment env(one time for one repo, this is add venv directory in your directory, add that in your gitignore and zappa_settings.json)
```bash
virtualenv venv
source venv/bin/activate
pip3 install -r requirements.txt
```

# We are ready to deploy now 

```bash
zappa deploy or zappa update
```

Caveat
add below to avoid including virtualenv we created above in package

```json
...
"exclude" : ["venv*"],
...
```

Happy Lambda !!

