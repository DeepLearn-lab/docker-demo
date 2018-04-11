# Docker Demo

Install Docker

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get update
$ apt-cache policy docker-ce
$ sudo apt-get install -y docker-ce
$ sudo systemctl status docker
```

Install Flask
```
$ pip install Flask
```

Write the following lines in `app.py`
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Flask Dockerized'

if __name__ == '__main__':
app.run(debug = True, host = '0.0.0.0')
```
Write the following lines in `requirements.txt`
```
Flask==0.10.1
```
Write the following lines in `Dockerfile`

**Note**: There is no extension in this file.
```
FROM ubuntu:latest
MAINTAINER Your Name "yourmail@gmail.com"
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
```
Write the following lines in `docker-compose.yml`
```
web:
  build: ./web
  ports:
   - "5000:5000"
  volumes:
- .:/code
```
