---
author: SujanThakare
layout: post
title: "Stopwatch using javascript"
date: 2015-12-28 21:00
comments: false
category: JavaScript
tags:
- JavaScript
---
 
 
 While designing JavaScript based UI we some time need a concept of stopwatch,  which gives functions like pause, resume and reset the watch. by using these functions we can manage complex UI where we have time constraint and JavaScript timer functions like 'setInterval' and 'setTimeout' are not enough to meet the requirement. so this post will explain you how to design stopwatch using JavaScript.
 
># Background
>Recently I came across a requirement where I have to refresh UI after some time interval. now you will say "hey man! this is very easy just use JavaScript timer function 'setInterval' ", but there is twist in the requirement, if user is active on the UI, means user is working on any popup then UI is not allowed to refresh. now you will say "then pause timer while user is active and resume as user stops activity. Hmmmmmm, for this you will need stopwatch." ٩(•̮̮̃-̃)۶ <br> 
for such kind of requirment stopwatch comes in the mind but there is no such stopwatch thing, in the JavaScript we just have simple timer functions setInterval and setTimeout which are not sufficient to achieve such requirement where we require pause, resume and reset functions


## Stopwatch Using JavaScript <small>Module Pattern</small>


We can use Module pattern and create stopwatch as a module.
Advantage to use module pattern is we can create n number of stopwatch instaces and can use it anywhere in any JavaScript application.

{% highlight javascript %}


    var stopwatch = function () {
        var me = this;

        me.timeremaining = 0;
        me.timeout = 0;
        me.timeoutCallback = undefined;
        me.timerId = undefined;

        var setStopWatch = function (time, timeout_callback) {
            me.timeout = time;
            me.timeremaining = time;
            me.timeoutCallback = timeout_callback;
            timer();
        }

        var timer = function () {
            if (me.timeremaining <= 0) {
                me.timeoutCallback();

            } else {
                me.timeremaining = me.timeremaining - 1000;
                me.timerId = setTimeout(function () {
                    timer();
                }, 1000);
            }
        }

        var pause = function () {
            clearTimeout(me.timerId);
        }
        var resume = function () {
            timer();
        }
        var reset = function () {
            pause();
            me.timeremaining = me.timeout;
            timer();
        }

        return {
            set: setStopWatch,
            pause: pause,
            resume: resume,
            reset: reset
        }
    }
{% endhighlight %}


Ok our module is ready, now how to use it
<br>
first create your stopwatch instance

{% highlight javascript %}

    var yourStopWatch = new stopWatch();

{% endhighlight %}

Now set the stopwatch by setting time and callback function. whatever you want to execute after timeout put in callback function.

{% highlight javascript %}

    yourStopWatch.set(10000,function(){
        console.log("Yeeee, after 1000 milisecond");
    })
{% endhighlight %}

In between if you want to pause, resume and reset the stopwatch just call 

{% highlight javascript %}

    yourStopWatch.pause();

    yourStopWatch.resume();

    yourStopWatch.reset();

{% endhighlight %}

It's super easy to use in any javascript framework like angularJs.

# Stopwatch using ExtJs


Let's see it using ExtJs, ExtJs is one of the mature javascript framework. ExtJs is derived from YUI library, YUI is totally based on module pattern. so it will have same structure as in above code snippet. 

Let's write the code with same logic and understand how to use it.

{% highlight javascript %}
    
    Ext.define('Stopwatch', {
        timeremaining: 0,
        timeout: 0,
        timeoutCallback: undefined,
        timerId: undefined,
        set: function (time, timeout_callback) {
            var me = this;
            me.timeout = time;
            me.timeremaining = time;
            me.timeoutCallback = timeout_callback;
            me.timer();
        },
        timer: function () {
            var me = this;
            if (me.timeremaining <= 0) {
                me.timeoutCallback();

            } else {
                me.timeremaining = me.timeremaining - 1000;
                me.timerId = setTimeout(function () {
                    me.timer();
                }, 1000);
            }
        },
        pause: function () {
            var me = this;
            clearTimeout(me.timerId);
        },
        resume: function () {
            var me = this;
            me.timer();
        },
        reset: function () {
            var me = this;
            me.pause();
            me.timeremaining = me.timeout;
            me.timer();
        }
    });

{% endhighlight %}

Here we defined a class named Stopwatch. now we have an ExtJs class and we can instantiate this class anywhere in ExtJs application,
If you want stopwatch should have single instance through out the application, make it singletone.

Let's create instace of stopwatch

{% highlight javascript %}

    var stopwatch = Ext.create('Stopwatch');

{% endhighlight %}

Now set the stopwatch by setting time and callback function. whatever you want to execute after timeout put in callback function.

{% highlight javascript %}
    
    stopwatch.set(1000, function(){
       console.log("Yeeee, after 1000 milisecond"); 
    });
{% endhighlight %}

By using this logic you can create stopwatch in any framework and language.

All rights are not reserved, so feel free to copy and share...٩(•̮̮̃-̃)۶  
