# Testing a Blog system with 2 Chrome browsers in Katalon Studio

## Background

I have a Web Application to test. It is the runninng sample code presented by
["Flask Tutorial"](https://flask.palletsprojects.com/en/2.0.x/tutorial/). It is *a basic blog application called Flaskr. Users will be able to register, log in, create posts, and edit or delete their own posts.* I just typed in the sample codes as published without any changes. At first, let me go through the pages to grasp what it is. Later I will describe how to set it up on your own PC.

I open Chrome browser to visit <http://127.0.0.1/> . I see the index page as follows, which has no blog posts submitted yet.

![1 start from here](./docs/images/test_flaskr/1_start_from_here.png)

At first, I need to register a User for me before creating posts. I click the `Register` link. Then a form is presented where I am requested to type a credential (username and password pair).

![2 going to register a username](./docs/images/test_flaskr/2_going_to_register_a_username.png)

I click the `Register` button. I am transferred to the LogIn page.

![3 a username has been registered](./docs/images/test_flaskr/3_a_username_has_been_registered.png)

I re-type the credential (username and password) that I used to create my User.

![4 about to login](./docs/images/test_flaskr/4_about_to_login.png)

I click the `Log In` button. Then I am transferred to the Index page. Please note that the username is displayed in the header. This implies that now I am logged-in the web application.

![5 the user have logged in](./docs/images/test_flaskr/5_the_user_have_logged_in.png)

Now I am going to create a new post. I click the `New` link. Then a empty form is displayed.

![6 opened page to create a new post](./docs/images/test_flaskr/6_opened_page_to_create_a_new_post.png)

I type a text into the `title` field, and a text into the `body` field.

![7 has typed texts into a post](./docs/images/test_flaskr/7_has_typed_texts_into_a_post.png)

I click the `Save` button. Then I am transferred to the index page. Please find a post has been saved into the Blob system and is now displayed in the list of posts.

![8 the post is found in the list](./docs/images/test_flaskr/8_the_post_is_found_in_the_list.png)

## Problem to solve

You can imagine; we can create 2 or more users. We should be able send multiple posts to <http://127.0.0.1/> from 2 or more browsers simultaneously. When a user Alice made a post, then another user Bob should be able to see the post by Alice in an instant. When Bob made a post, then soon Alice should be able to see the Bob’s post.

This test scenario --- testing a web app with 2 browsers simultaneously --- is a practical one. Let me assume I have a Electric-Commerce web app which has 2 types of user interface: Customer UI and Administrator UI. When a user submit an order to purchase a product, then an administrator should be able to see it in the list of outstanding orders. I want to test the Customer UI and the Administrator UI together. I want my Web UI test submit an order in the Customer UI, and I want my test verify if the order is appropriately processed in the Administrator UI.

**But how can I do it using Selenium-based Web UI automation tool? How can I do it in Katalon Studio?**

### Problem1 : Katalon Studio can not natively open 2 browsers.

## Solution

## Description

### Target Web App

## Envrionment setup

### Installing docker command

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

### Starting up HTTP Server App at <http://127.0.0.1/>

I made a temporary directory with any name.

    $ cd ~
    $ mkdir flaskr

In the temp directory, I started a web app using a docker image.

    $ cd ~/flaskr
    $ docker run -it -p 80:8080 --rm kazurayam/flaskr-kazurayam:1.0.3
    Serving on http://0.0.0.0:8080

Or, you can use the following shell script in the root directory of this project.

-   [startup\_flaskr.sh](./startup_flaskr.sh)

<!-- -->

    if [ ! -e ./tmp ]; then
        mkdir tmp
    fi 
    cd ./tmp
    docker run -it -p 80:8080 --rm kazurayam/flaskr-kazurayam:1.0.3
    cd -

Now I can open a browser and visit the following URL.

-   <http://127.0.0.1:80/>

![flaskr just started](docs/images/flaskr_just_started.png)

I made a docker image which is publicly available at Docker Hub :

-   <https://hub.docker.com/repository/docker/kazurayam/flaskr-kazurayam>

## Web UI Test Scenario

1.  I will use **Flaskr** at `http://127.0.0.1` as a partner for me to develop a set of Web UI test scripts in Katalon Studio.

2.  I will open 2 Chrome browsers. On each, I will visit the Flaskr site and interact with it. I will keep 2 browsers open and operate on them simultaneously.

3.  On one browser, I will register a user **Alice** and make some posts.

4.  On another browser, I will register another user **Bob** and make some posts.

5.  Alice should be able to read the posts made by Bob. Bob should be able to read the posts made by Alice. My web ui test in Katalon Studio will check this conversation.

## Experiments
