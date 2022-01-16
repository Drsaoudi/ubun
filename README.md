# HerokuDE

This project is an attempt to run a (more or less) fully-featured desktop
environment in Heroku to be able to run applications in it.

Note however, even though this image was designed to work on Heroku, it also
works as standalone Docker image that you can run locally yourself.


## How does it work

Since Heroku [allows deployment of Docker images](https://devcenter.heroku.com/articles/build-docker-images-heroku-yml#heroku-yml-overview),
one could create an image with minimal window manager, VNC server
software and NoVNC as a way to use VNC in browser (due to Heroku restricting
open ports to HTTP/HTTPS only.)

Here, the following components are used:

* Xvfb for virtual display initialization
* Fluxbox as window manager
* X11VNC as VNC server


## Usage

### Deploying to Heroku (with Heroku CLI)

```shell
$ heroku -a <app-name> container:push web
$ heroku -a <app-name> container:release web
```


### Running locally

```shell
$ git clone https://github.com/dreamscached/herokude HerokuDE
$ docker build --rm -t herokude:ubuntu20.04 .
$ docker run --rm -d --name herokude -e PORT=80 -p 80:80 herokude:ubuntu20.04
```