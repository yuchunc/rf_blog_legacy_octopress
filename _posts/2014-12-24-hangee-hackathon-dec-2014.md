---
layout: post
title: "HanGee Hackathon Dec 2014"
date: 2014-12-24 21:25:49 +0800
comments: true
tags: nodejs, hackathon
---

<a href="https://www.flickr.com/photos/129247110@N02/16092912371" title="IMG_20141221_173200 by Mickey Chen, on Flickr"><img src="https://farm8.staticflickr.com/7467/16092912371_0d7881bb0e_z.jpg" width="640" height="474" alt="IMG_20141221_173200"></a>

I finally got the chance to attend my first hackathon last weekend(21st, 22nd)!
Two days, free food, pizza party, and intense geeky coding all through the night. Couldn't
get much more interesting than this!

I saw the even the day before, with wife and kids out of town, it couldn't
have been on a better timing. I was exposed to NodeJS and ReactJS during the first
day by [smlsunxie](https://github.com/smlsunxie) and [coodoo](https://github.com/coodoo). The
topic was on *NodeJS Testing* and *Beginning with ReactJS* respectively. Coodoo's speak and
codes was instrumental for our project. We did an project which I had always wanted to do,
**location-based-reddit-like-service**.

So, I'll try to summarized what I come to understand about ReactJS, an awesome JS framework.

Let's start somewhere simple.

## Backend

The backend is rather straight forward, install strongloop, and

    slc loopback

will generate backend scaffolding.

    slc loopback:model

for triggering the interactive model creation.

Finally, you do

    slc run.

to get your backend server running.

Strongloop/loopback is a basic Node API server, following the REST conventions. However,
unlike Rails, which has 7 routes (8 to be precise), Strongloop creates 11 routes for you.

<img src="http://strongloop.com/wp-content/uploads/2014/04/985x565xStrongLoop-API-Explorer-2014-04-19-15-49-48-2014-04-19-15-50-53.png.pagespeed.ic.pBlCARX1qr.png">

During the hacking process, initially, we wanted to place our distance calculations inside backend.
However, after much thought, I was convinced otherwise and did not touch the backend code besides
the system generated models.

The reason?

If I understand correctly, **MVW Frameworks** and **Client-Side WebApp**  encourages developer to
place much of the calculations on the client side. In our case, it felt right! After coming to this
conclusion, our development also make so much more sense. No more, "pass x to server, pass back y,
then calculate x - y to display z", it was all in one simple and easy to understand module. Life's
Good. \*Thumbs Up\*

## Frontend
This is where ReactJS comes in, he also brought along he's less popular brother, Flux.

<img src="https://raw.githubusercontent.com/facebook/flux/master/docs/img/flux-diagram-white-background.png">

Above image sums up everything React and Flux is doing, keep it in mind and you are good. Here's
how it kept us sane.

React organizes views into .jsx files, which interestingly collects both html-like dsl and javascripts
of the same behavior together. The user then triggers actions which are captured and passed along to
the action creator, which then communicates with the backend and/or sends the action object to dispatcher.
Dispatcher is responsible for controlling the flow, and will wait for the previous process to finish
before allowing the next one. Store is where the business logic are placed, and it will act on the
data passed along from the dispatcher, then emit a request to update the virtual DOM of the React
view.

phew, that's a mouthful.

But once you get the basic concept, development was a breeze. Everything work as they should, and
you can bring teammates up to speed pretty rapidly. One thing could have done better, instead of distance
calculation in view, we should have placed it in store.

<a href="https://www.flickr.com/photos/129247110@N02/16094120682" title="IMG_20141221_173804 by Mickey Chen, on Flickr"><img src="https://farm9.staticflickr.com/8659/16094120682_8035ba52f7_z.jpg" width="640" height="474" alt="IMG_20141221_173804"></a>

It was a really awesome event! Really good to know people of the similar interest. One thing that
surprised me, was the Rails background I had was pretty helpful, much of the concept can be easily
translated.

Anyway, Happy Christmas Everybody!! = )

<a href="https://www.flickr.com/photos/129247110@N02/15908746169" title="IMG_20141221_194013 by Mickey Chen, on Flickr"><img src="https://farm8.staticflickr.com/7536/15908746169_8ede4a2a8b_z.jpg" width="474" height="640" alt="IMG_20141221_194013"></a>
