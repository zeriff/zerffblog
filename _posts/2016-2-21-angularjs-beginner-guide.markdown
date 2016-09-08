---
author: SujanThakare
layout: post
title: "Angular Js Beginner Guide Part I"
date: 2016-2-21 21:00
comments: false
category: AngularJs
tags:
- JavaScript
---


I am writing this post just after reviewing the angularJs building blocks. the post aims is to present the topics and building blocks of angularjs for beginners.
To learn angularJs we can find handful of tutorials and documentation.
To getting started cursory glance through these stuff is not going to help.
These will lead to confusion and frustration.
This post will guide you through important topics of angularJs.
Which will help you to getting started with angularJs.


># Introduction

You just completed your first step of learning angularJs. Cheers, This post will cover following basic blocks.

- Directive
- Binding
- Controller

### Prerequisites

Basic knowledge of 

- HTML
- JavaScript
- CSS
- Events

># Let's  get started


At a first glance, AngularJs seems a library. But always mind it AngularJs is not a library. It's a JavaScript framework.
Angular can help you to write cleaner, more efficient code and can make your HTML more expressive and readable. 

for more details, what is <a href="https://docs.angularjs.org/guide/introduction">AngularJs</a>


### Let's Roll

It's better to code while learning so Let's first create our playground. 

In case of editor it's all your choice, but I will suggest Brackets, 
you can <a href="http://brackets.io/" target="_blank">download</a> and use it for free. Brackets is really a cool editor for web coding, Brackets has a feature of live previewing which solves the local server problem as we require a local server to serve our files.

Download angular source files from
<a href="https://angularjs.org/" target="_blank">here</a>

For look and feel of the web pages we will use simple css framework skeleton you can download it's
source files from <a href="http://getskeleton.com/" target="_blank">here</a>.

Now we have all the stuff for our playground let's compile it.

Setup directory as follows.

{% highlight javascript %}

    angulartodo
    |---js
    | |---app.js
    | |---angular.min.js
    |
    |---css
    | |---normalize.css
    | |---skeleton.css
    |
    |---index.html

{% endhighlight %}

or you can download zip from <a href="https://github.com/sujanthakare/angulartodo" target="_blank">here</a>. 

Husshhhhh........ done all stuff let's do some real work

>##### Note
You can understand better by typing the code. If you are familiar with the code you can copy/paste the code

Let's start with basic building blocks.


>## Directive
 Directives are certainly one of the most important facets of the framework, and as such, this is one of the biggest sections of the course.

AngularJs is all about the directives. Let's understand directives. 


{% highlight html %}

    <html>

    ... ...

    <body>
        <div ng-app>
            <div class="container">
                <center>
                    <h1>Hello Angular</h1>
                </center>
            </div>
        </div>
    </body>

    </html>
{% endhighlight %}

Here we have code in index.html, we used ng-app directive to create angular application. Directive *ng-app* defines where in our page an Angular application is running.

>###### The general idea behind directives is this:  
what if you could create your own element and attribute types with corresponding functionality? With directives, you can create custom, reusable components for your application that make developing interactive UI widgets drastically easier. No more custom jQuery code every time you want put a UI widget on the screen; you just place your custom directives there instead!

For general understanding It is analogous to attributes in html, like *onclick* which is event attribute for dom elements, which gives special feature to corresponding dom elements.

{% highlight html %}

    <div onclick="fun()"></div>
    
{% endhighlight %}

>##### Note:
 Don't waste time here to understand directives, it is very vast section you will understand as you practice, just understand the general use of directives.
 

so whenever you see the attribute preceding with *ng* it is an angular directive which indicates and hold special meaning in the dom.
    

>## Binding
 Binding is one of the powerful features of Angular. It basically synchronize data between views and models automatically
 
 “whoa buddy, what it actually means.”  :( relax Let's understand what it means by doing

Let’s set up a model in a view.

{% highlight html %}

       <div ng-app>
            <div class="container">
                <center>
                    <h1>Hello Angular</h1>
                    <input type="text" ng-model="todo">
                </center>
            </div>
        </div>

    
{% endhighlight %}

Here we created a text field and has an ng-model attribute of *todo*. as we seen in previous section of directive, ng-model is also an angular directive, it basically binds a variable to an input field, means whatever value inside the input field it get assign to scope variable you are binded with ng-model here the scope variable is *todo*. let’s see the magic of binding. let’s bind our todo variable into our view. see the following code snippet


{% highlight html %}

    <div ng-app>
        <div class="container">
            <center>
                <h1>Hello Angular</h1>
                <input type="text" ng-model="todo">
                <h2>
                {% raw %}
                    {{todo}}
                {% endraw %}
                </h2>
            </center>
        </div>
    </div>

{% endhighlight %}

Let’s see into the browser, (if you are using Brackets go to File--live preview, it will start local server and will render your index page)

If we start typing into input field. we can see the magic, text we’re typing appear below our input field. as we binded variable {% raw %} *{{todo}}*    {% endraw %} in to our view.
why this happens because what’s in between the curly brackets is an angular expression. curly brackets let's angular knows that there is an expression that needs to be evaluated, so angular evaluates the expression and replaces curly brackets with evaluated value. 

you can write expression like addition, subtraction etc e.g  {% raw %} {{ 1 +  2 }} {% endraw %}

see the angular guide for <a href="https://docs.angularjs.org/guide/expression" target="_blank">expression</a>  


>## Controller
 The role of controllers in Angular is to serve data to our view and to provide functions that contains logic of our application.
 

Let's understand controllers by doing.

First create an angular application with following code.

{% highlight html %}

    <div ng-app="app">
        <div class="container">
            <center>
                <h1>controllers</h1>
            </center>
        </div>
    </div>

{% endhighlight %}


The value given to directive ng-app tells angular that what module to look when angular boots up.
here we have value *app*.

now let’s create *app* module


{% highlight html %}

       <body>
        <div ng-app="app">
            <div class="container">
                <center>
                    <h1>controllers</h1>
                </center>
            </div>
        </div>

        <script>
            'use strict';
            var app = angular.module('app', []);
        </script>
       </body>

{% endhighlight %}

so we created a module named *app*, using *angular.module*, the second parameter to *angular.module* is an array of dependencies that our module uses.
currently we don’t have any dependencies we will use this later .

Now this *app* module will contain the controllers.

Let’s create controller.

{% highlight html %}

    <script>
        'use strict';
        var app = angular.module('app', []);

        app.controllers('MyFirstCtrl', function () {
            var me = this;
            me.message = "my first controller";
        });
    </script>


{% endhighlight %}

Now we have our controller ready to serve message, let’s use it in to the view.

{% highlight html %}

       <div ng-app="app">
        <div class="container">
            <div ng-controller="MyFirstCtrl as myCtrl">
                <center>
                    <h1>Controller</h1>
                    <h2>{% raw %} {{myCtrl.message}} {% endraw %}</h2>
                </center>
            </div>
        </div>
        </div>

{% endhighlight %}

Here, we used directive *ng-controller*. It will assign controller to the curresponding *div* and you are allowed to use functions and variables of this controller with in this div. also we have created it's alias as *myCtrl* using *as* keyword. so we can use it's variables and function using dot operator.

Now we learned variables let’s see function.

Let’s create a *updateMessage* function that will update our message, to use this function let’s create text field and update button on click of update button message will get updated with value in text field.

{% highlight html %}

    <body>
        <div ng-app="app">
        <div class="container">
            <div ng-controller="MyFirstCtrl as myCtrl">
                <center>
                    <h1>Angular</h1>
                    <hr>
                    <input ng-model="newMessage" type="text" placeholder="message">
                    <button ng-Click="myCtrl.updateMessage(newMessage)">Update</button>
                    <h2>{{myCtrl.message}}</h2>
                </center>
            </div>
        </div>
        </div>
        <script>
            'use strict';
            var app = angular.module('app', []);

            app.controller('MyFirstCtrl', function () {
                var me = this;
                me.message = "my first controller";
                me.updateMessage = function (newMessage) {
                    me.message = newMessage;
                }
            });
        </script>
    </body>
    
{% endhighlight %}


Here in the code snippet. we are assigning *updateMessage* function on click of update button using directive *ng-Click* and passing the value of text field to the function. so as we change the value of *message* variable of controller which is binded in the view as *myCtrl.message* the view will get updated with our new value.

Now you understood how to use controllers. for code modularity we can move script part to new js file  *app.js* which will be center of our application. let’s move script part to app.js and include file reference in index.html.


{% highlight html %}
    
    <head>
        <script src="js/angular.min.js"></script>
        <script src="js/app.js"></script>
    </head>
 
{% endhighlight %}
