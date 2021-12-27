# Driving Multiple Browsers in Katalon Studio

## Installing docker command

I installed `docker` command into my Mac Book Air

    $ brew install docker
    ...

I checked if the `docker` command is running.

    $ docker --version
    Docker version 20.10.2, build 2291f61
    :~
    $

Windows users can use "Docker Desktop on Windnows" of course,

-   <https://docs.docker.com/desktop/windows/install/>

## Starting up HTTP server at <http://127.0.0.1/>

I made a temporary directory named `flaskr` where I launch a web app.

    $ cd ~
    $ mkdir flaskr

I started a web app using a docker image.

    $ cd ~/flaskr
    $ docker run -it -p 80:8080 --rm kazurayam/flaskr-kazurayam:1.0.3
    Serving on http://0.0.0.0:8080

Now I can open a browser and visit

-   <http://127.0.0.1:80/>

then a page like this would be visible.

![flaskr just started](docs/images/flaskr_just_started.png)

This is the sample web app of ["Flask Tutorial"](https://flask.palletsprojects.com/en/2.0.x/tutorial/). It is *a basic blog application called Flaskr. Users will be able to register, log in, create posts, and edit or delete their own posts.* I justed typed in the sample codes as published.

I made a docker image which is publicly available at Docker Hub :

-   <https://hub.docker.com/repository/docker/kazurayam/flaskr-kazurayam>

## Scenario

1.  I will use **Flaskr** at `http://127.0.0.1` as a partner for me to develop a set of test scripts in Katalon Studio.

2.  I will open 2 Chrome browsers. On each, I will visit the Flaskr site and interact with it. I will keep 2 browsers open and operate on them simultaneously.

3.  On one browser, I will register a user **Alice** and make some posts.

4.  On another browser, I will register another user **Bob** and make some posts.

5.  Alice should be able to read the posts made by Bob. Bob should be able to read the posts made by Alice. My web ui test in Katalon Studio will check this conversation.
