# Hello World Flask App Deployed to AWS Elastic Beanstalk using Travis.com and Docker

http://flask.novskytech.com/


### App Components
* Aws Elastic Beanstalk
* Travis CI 
* Flask/Python
* Docker

### App Resources (links may break)
* [Aws App Environment](https://us-east-2.console.aws.amazon.com/elasticbeanstalk/home?region=us-east-2#/environment/dashboard?applicationName=flask-app-template&environmentId=e-zsbsqbgptm)
* [Aws App Dashboard](https://us-east-2.console.aws.amazon.com/elasticbeanstalk/home?region=us-east-2#/applications)
* [Travis Ci](https://app.travis-ci.com/github/kono10/FlaskElasticBeanstalkTemplate)
* [App Link](http://flaskapptemplate-env.eba-v9rkjc5v.us-east-2.elasticbeanstalk.com/)

### App Notes
* Uses a single docker container
* The docker-compose.yml file is needed for AWS Elastic Beanstalk. AWS EB will automatically recognize the docker-compose.yml file and then build and run the docker container needed to deploy the application.
* Once code is merged into the main branch it will be deployed and publicly available using the url generated by AWS Elastic Beanstalk.
* This is an example app used as a proof of concept for continuous integration and development. Do not use this app for production development that includes sensitive information or connections (for example an app that connects to a database). 
* This app does not use nginx.

## How to build and run app locally using docker compose

... in the same directory as the docker-compose.yml file

Summary
```
> docker compose build

> docker compose up
```
Detail
```
❯ docker compose build
[+] Building 5.4s (11/11) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                                                     0.0s
 => => transferring dockerfile: 32B                                                                                                                                                                                      0.0s
 => [internal] load .dockerignore                                                                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/python:3.8                                                                                                                                                            0.6s
 => [internal] load build context                                                                                                                                                                                        0.0s
 => => transferring context: 606B                                                                                                                                                                                        0.0s
 => [1/6] FROM docker.io/library/python:3.8@sha256:f732d55571549b427e12edb89d0951372e7b73c67f717ad0645bb0cda19fc05e                                                                                                      0.0s
 => CACHED [2/6] RUN apt-get update                                                                                                                                                                                      0.0s
 => CACHED [3/6] WORKDIR /app                                                                                                                                                                                            0.0s
 => [4/6] COPY . .                                                                                                                                                                                                       0.0s
 => [5/6] RUN pip3 install -r requirements.txt                                                                                                                                                                           4.0s
 => [6/6] RUN pytest test_app.py                                                                                                                                                                                         0.4s
 => exporting to image                                                                                                                                                                                                   0.2s
 => => exporting layers                                                                                                                                                                                                  0.2s
 => => writing image sha256:4bb91800ff544ebe6fac681ff5a3efbd4e52be696e3848f231a7dec481dc7a1d                                                                                                                             0.0s
 => => naming to docker.io/library/flasktemplateelasticbeanstalk_web                                                                                                                                                     0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
❯ docker compose up
[+] Running 1/0
 ⠿ Container flasktemplateelasticbeanstalk_web_1  Created                                                                                                                                                                0.0s
Attaching to web_1
web_1  | [2022-05-03 15:54:34 +0000] [1] [INFO] Starting gunicorn 20.1.0
web_1  | [2022-05-03 15:54:34 +0000] [1] [INFO] Listening at: http://0.0.0.0:5000 (1)
web_1  | [2022-05-03 15:54:34 +0000] [1] [INFO] Using worker: sync
web_1  | [2022-05-03 15:54:34 +0000] [8] [INFO] Booting worker with pid: 8
web_1  | [2022-05-03 15:54:34 +0000] [9] [INFO] Booting worker with pid: 9
web_1  | [2022-05-03 15:54:34 +0000] [10] [INFO] Booting worker with pid: 10
```

## Build and run app locally using Dockerfile
* access the app in browser at http://localhost:8080/
* run commands in the same directory as the docker-compose.yml file

Summary
```
❯ docker build -t jakeapp app

❯ docker run -p 8080:5000 jakeapp
```
Detail
```
❯ docker build -t jakeapp app
[+] Building 1.3s (11/11) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                                                     0.0s
 => => transferring dockerfile: 253B                                                                                                                                                                                     0.0s
 => [internal] load .dockerignore                                                                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/python:3.8                                                                                                                                                            1.2s
 => [1/6] FROM docker.io/library/python:3.8@sha256:f732d55571549b427e12edb89d0951372e7b73c67f717ad0645bb0cda19fc05e                                                                                                      0.0s
 => [internal] load build context                                                                                                                                                                                        0.0s
 => => transferring context: 1.90kB                                                                                                                                                                                      0.0s
 => CACHED [2/6] RUN apt-get update                                                                                                                                                                                      0.0s
 => CACHED [3/6] WORKDIR /app                                                                                                                                                                                            0.0s
 => CACHED [4/6] COPY . .                                                                                                                                                                                                0.0s
 => CACHED [5/6] RUN pip3 install -r requirements.txt                                                                                                                                                                    0.0s
 => CACHED [6/6] RUN pytest test_app.py                                                                                                                                                                                  0.0s
 => exporting to image                                                                                                                                                                                                   0.0s
 => => exporting layers                                                                                                                                                                                                  0.0s
 => => writing image sha256:4bb91800ff544ebe6fac681ff5a3efbd4e52be696e3848f231a7dec481dc7a1d                                                                                                                             0.0s
 => => naming to docker.io/library/jakeapp                                                                                                                                                                               0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
❯ docker run -p 8080:5000 jakeapp
[2022-05-03 15:56:56 +0000] [1] [INFO] Starting gunicorn 20.1.0
[2022-05-03 15:56:56 +0000] [1] [INFO] Listening at: http://0.0.0.0:5000 (1)
[2022-05-03 15:56:56 +0000] [1] [INFO] Using worker: sync
[2022-05-03 15:56:56 +0000] [8] [INFO] Booting worker with pid: 8
[2022-05-03 15:56:56 +0000] [9] [INFO] Booting worker with pid: 9
[2022-05-03 15:56:56 +0000] [11] [INFO] Booting worker with pid: 11
```

## Run app using Python and Flask development server
* run commands in the app directory
* access app via browser at http://localhost:5000/

Summary
```
❯ virtualenv flaskEnv -p python3
❯ source flaskEnv/bin/activate
❯ pip install -r requirements.txt
❯ python app.py
```
Detail
```
❯ pwd
~/development/FlaskTemplateElasticBeanstalk/app
❯ virtualenv flaskEnv -p python3
created virtual environment CPython3.8.8.final.0-64 in 899ms
  creator CPython3Posix(dest=/Users/jkonovsky/development/FlaskTemplateElasticBeanstalk/app/flaskEnv, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/jkonovsky/Library/Application Support/virtualenv)
    added seed packages: pip==22.0.4, setuptools==62.0.0, wheel==0.37.1
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator
❯ source flaskEnv/bin/activate
❯ pip install -r requirements.txt
Collecting Flask
  Downloading Flask-2.1.2-py3-none-any.whl (95 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 95.2/95.2 KB 2.3 MB/s eta 0:00:00
Collecting gunicorn
  Using cached gunicorn-20.1.0-py3-none-any.whl (79 kB)
Collecting pytest
  Downloading pytest-7.1.2-py3-none-any.whl (297 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 297.0/297.0 KB 5.0 MB/s eta 0:00:00
Collecting importlib-metadata>=3.6.0
  Using cached importlib_metadata-4.11.3-py3-none-any.whl (18 kB)
Collecting Werkzeug>=2.0
  Downloading Werkzeug-2.1.2-py3-none-any.whl (224 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 224.9/224.9 KB 4.8 MB/s eta 0:00:00
Collecting Jinja2>=3.0
  Downloading Jinja2-3.1.2-py3-none-any.whl (133 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 133.1/133.1 KB 3.5 MB/s eta 0:00:00
Collecting click>=8.0
  Downloading click-8.1.3-py3-none-any.whl (96 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.6/96.6 KB 2.6 MB/s eta 0:00:00
Collecting itsdangerous>=2.0
  Using cached itsdangerous-2.1.2-py3-none-any.whl (15 kB)
Requirement already satisfied: setuptools>=3.0 in ./flaskEnv/lib/python3.8/site-packages (from gunicorn->-r requirements.txt (line 2)) (62.0.0)
Collecting tomli>=1.0.0
  Downloading tomli-2.0.1-py3-none-any.whl (12 kB)
Collecting packaging
  Downloading packaging-21.3-py3-none-any.whl (40 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.8/40.8 KB 1.2 MB/s eta 0:00:00
Collecting pluggy<2.0,>=0.12
  Downloading pluggy-1.0.0-py2.py3-none-any.whl (13 kB)
Collecting attrs>=19.2.0
  Downloading attrs-21.4.0-py2.py3-none-any.whl (60 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.6/60.6 KB 1.1 MB/s eta 0:00:00
Collecting iniconfig
  Downloading iniconfig-1.1.1-py2.py3-none-any.whl (5.0 kB)
Collecting py>=1.8.2
  Downloading py-1.11.0-py2.py3-none-any.whl (98 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.7/98.7 KB 1.8 MB/s eta 0:00:00
Collecting zipp>=0.5
  Using cached zipp-3.8.0-py3-none-any.whl (5.4 kB)
Collecting MarkupSafe>=2.0
  Using cached MarkupSafe-2.1.1-cp38-cp38-macosx_10_9_x86_64.whl (13 kB)
Collecting pyparsing!=3.0.5,>=2.0.2
  Downloading pyparsing-3.0.8-py3-none-any.whl (98 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.5/98.5 KB 2.7 MB/s eta 0:00:00
Installing collected packages: iniconfig, zipp, Werkzeug, tomli, pyparsing, py, pluggy, MarkupSafe, itsdangerous, gunicorn, click, attrs, packaging, Jinja2, importlib-metadata, pytest, Flask
Successfully installed Flask-2.1.2 Jinja2-3.1.2 MarkupSafe-2.1.1 Werkzeug-2.1.2 attrs-21.4.0 click-8.1.3 gunicorn-20.1.0 importlib-metadata-4.11.3 iniconfig-1.1.1 itsdangerous-2.1.2 packaging-21.3 pluggy-1.0.0 py-1.11.0 pyparsing-3.0.8 pytest-7.1.2 tomli-2.0.1 zipp-3.8.0
❯ python app.py
 * Serving Flask app 'app' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on all addresses (0.0.0.0)
   WARNING: This is a development server. Do not use it in a production deployment.
 * Running on http://127.0.0.1:5000
 * Running on http://10.32.150.151:5000 (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 896-622-362

```
