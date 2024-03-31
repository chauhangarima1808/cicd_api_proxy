# unicorn_api_proxy

This is our API Proxy code for use by trusted Unicorn.Rentals partners, and less trusted DevOps teams. Its purpose is to proxy API calls to our backend. It uses a different auth secret to auth to the backend, and to validate the result with the caller. Currently, the authorization token is updated by a *git push* at regular intervals.

## Architecture

Below was/is the proposed architecture for deploying this application. We have partially fulfilled the design in our MVP deployment.

![AWS Architecture](https://ee-assets-prod-us-east-1.s3.amazonaws.com/modules/9c0e89820b864addaed45ec2f5440379/v5/213ecc53-ca2e-4f71-8753-f4607f2feef4/cicd_architecture.png)


## Getting Started

If you want to locally test, etc:
* Have python 3.9 

This will deploy the python dependencies and run a local web server:

```
pip install -r requirements.txt
python app.py
```

## Tests
If deploying with CICD tooling, run tests via CodeBuild or any other CI tool:
```
python tests_app.py -v
```

Or you can manually test with cURL, httpie or a browser.

## Deployment

Deploy how suits you, but we included an *appspec.yml* for AWS CodeDeploy.

Optionally, have AWS xray deployed (executable not in this repo):
```
curl https://s3.dualstack.us-east-1.amazonaws.com/aws-xray-assets.us-east-1/xray-daemon/aws-xray-daemon-linux-3.x.zip -o xray.zip
unzip xray.zip
chmod +x xray 
nohup ./xray &
```

And have a default AWS region set, either via an environment variable, or *aws configure*.

## Built With
Python  
Flask  
flask_restful  
Requests  
watchtower
