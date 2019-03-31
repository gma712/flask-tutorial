# Flask Tutorial

## docker setup
```
$ docker build . -t app_nginx_uwsgi
$ docker run -p 8080:80 app_nginx_uwsgi
$ docker exec -it CONTAINER_ID /bin/bash
```
