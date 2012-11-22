Radiate Buildpack
=================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) to set up a [Radiate](https://github.com/philippbosch/radiate) server.

Since Radiate is based on Node.js, this buildpack is based on the [Node.js buildpack)[https://github.com/heroku/heroku-buildpack-nodejs].


Setup
-----

To set-up a Radiate instance try this (substitute `APPNAME` with something meaningful):

```
$ mkdir APPNAME
$ cd APPNAME
$ git init
Initialized empty Git repository in /path/to/APPNAME/.git/
$ touch radiate.conf
$ ls
radiate.conf
$ git add .
$ git commit -m "Initial."
[master (root-commit) 0a1b2c3] Initial.
0 files changed
create mode 100644 radiate.conf
$ heroku create --buildpack https://github.com/philippbosch/heroku-buildpack-radiate.git APPNAME
Creating APPNAME... done, stack is cedar
BUILDPACK_URL=https://github.com/philippbosch/heroku-buildpack-radiate.git
http://APPNAME.herokuapp.com/ | git@heroku.com:APPNAME.git
Git remote heroku added
$ git push heroku master
...
-----> Heroku receiving push
-----> Fetching custom git buildpack... done
-----> Radiate app detected
-----> 
       Initialized empty Git repository in /tmp/build_3fr1y780kd6hp/radiate/.git/
-----> Resolving engine versions
       Using Node.js version: 0.8.14
       Using npm version: 1.1.65
-----> Fetching Node.js binaries
-----> Vendoring node into slug
-----> Installing dependencies with npm
...
Dependencies installed
-----> Building runtime environment
-----> Discovering process types
       Procfile declares types -> web
-----> Compiled slug size: 4.7MB
-----> Launching... done, v7
       http://APPNAME.herokuapp.com deployed to Heroku

```

The buildpack will detect your app as a Radiate instance if it has the file `radiate.conf` in the root. The content of the file is currently ignored by Radiate since there are no configuration options.


Usage
-----

```
$ curl -X PUT -d value=0 http://APPNAME.herokuapp.com/counter
{
  "value": "0"
}
$ curl -X PUT -d action=INCR http://APPNAME.herokuapp.com/counter
{
  "value": "1"
}
$ curl http://APPNAME.herokuapp.com/counter
{
  "value": "1"
}
```
