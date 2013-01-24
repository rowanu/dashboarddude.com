---
layout: post
title: "Dashboards for Graphite"
date: 2013-01-23 08:17
comments: true
categories: Graphite Javascript d3.js dashboards Giraffe Cubism.js Graphene Tasseo Graphiti Descartes GDash GraphExplorer Dashing
---

It's no secret I like [Graphite](http://graphite.wikidot.com/) - it's a great example of Open Source software
which is just as good (actually, it's even better) than similar closed-source,
enterprise-grade (and much more __expensive__) software.

{% img right /images/posts/dashboards-for-graphite/boring.png 400 300 A bit dull...%}

While Graphite is fantastic, the front-end that comes with it leaves a little
bit to be desired. You _can_ use the built-in rendering and dashboard for viewing
your system metrics, just like you _can_ use Internet Explorer 6 to browse the
inter net - it'll work, but [you're gonna have a bad time](http://www.quickmeme.com/meme/3osf83/).

Thankfully, there are a lot of alternatives out there, but the [Graphite Tools](http://graphite.readthedocs.org/en/latest/tools.html)
page is a little out of date (with abandoned/incomplete projects), so here's a 
list or dashboards I have or would consider using:

<!--more-->

## Client-side Dashboards
These dashboards use the [Graphite Render API](http://graphite.readthedocs.org/en/latest/render_api.html) to get data, and show them using
some of the latest client-side Javascript libraries (like [D3.js](http://d3js.org/)) to render
graphs.

These dashboards usually __perform noticeably better than the built-in renderer__,
because it shifts the rendering work to your browser, rather than the server
(which is already working to retrieve the metrics from disk, etc).

[{% img right /images/posts/dashboards-for-graphite/giraffe.png 150 300 Giraffe %}](https://github.com/kenhub/giraffe)
### [Giraffe](https://github.com/kenhub/giraffe)
A [Rickshaw](http://code.shutterstock.com/rickshaw/)-based (which is built on d3.js) dashboard with a nice interface for 
toggling metrics and changing the time period being shown on the fly.

While I haven't used it personally, it looks good. My only concern is the
performance, as even [the small demo](http://kenhub.github.com/giraffe/#dashboard=Demo&timeFrame=1d) is a bit slow.

### [Cubism.js](http://square.github.com/cubism/)
[{% img right /images/posts/dashboards-for-graphite/cubism.js.png 400 300 Cubism.js %}](http://square.github.com/cubism/)
This is a great dashboard for fitting a large number of metrics on one screen.
The horizon graph is suited to comparing many similar metrics, and the default
colour scheme is really easy on the eyes, without loosing detail.

While the current values are displayed, you'll need to mouse-over the previous
updates which may not suit some dashboards.

[{% img right /images/posts/dashboards-for-graphite/graphene.png 400 300 Graphene %}](http://jondot.github.com/graphene/)
### [Graphene](http://jondot.github.com/graphene/)
A good general-purpose replacement for your Graphite dashboards.
As you can see on its demo page, it has widgets for gauges and counters, if
you're using [StatsD's](https://github.com/etsy/statsd) extra features.

It has a nice auto-discovery feature, which can convert your existing
Graphite dashboards to their Graphene equivalent quickly, but I find the
dark/high contrast/high intensity colour scheme tough to look at for long
periods of time (but that can be changed with some extra CSS styling).

### [Tasseo](https://github.com/obfuscurity/tasseo)
[{% img right /images/posts/dashboards-for-graphite/tasseo.png 400 300 Tasseo %}](https://github.com/obfuscurity/tasseo)
Another Rickshaw-based front-end, it's a very light-weight dashboard for viewing
many different metrics (ie. they don't have to be on the same scale) at once.

It Can be easily configured to change colour when certain thresholds are breached, 
which makes it nice as a high-level dashboard. It's not suited for long-term
metric monitoring, as there are no y-axes drawn which can make working out
historical values a bit hard.

This is a dashboard by Jason Dixon, who also does the Descartes dashboard (see below).

## Database-backed Dashboards
These databases have more features than the client-side dashboards, but require
more set up and configuration to get running. Most reduce the load on your
Graphite server by caching often-used data (eg. by using [Redis](http://redis.io/)).

[{% img right /images/posts/dashboards-for-graphite/graphiti.jpeg 400 300 Graphiti %}](https://github.com/paperlesspost/graphiti)
### [Graphiti](https://github.com/paperlesspost/graphiti)
A Redis-backed dashboard replacement which uses JSON to configure graphs. It 
uses Redis as a metric and settings cache, and it has the ability to store 
snapshots of your graphs on Amazon's S3. One thing to note is that it
deliberately doesn't do authentication - it makes the (not unreasonable)
assumption that your Graphite data and dashboards are not on a public network.

### [Descartes](https://github.com/obfuscurity/descartes)
Definitely the most comprehensive replacement for Graphite's built-in dashboard
so far, which isn't really surprising given it's by Jason Dixon (see below).
It depends on Redis and PostreSQL, which also puts it at the top of the
requirements list.

[{% img right /images/posts/dashboards-for-graphite/descartes.png 400 200 Descartes %}](https://github.com/obfuscurity/descartes)
It has the ability to set templates for graphs, and uses sparklines to give you 
a high-level overview of your metrics and help you decide what you want to 
include in your dashboard, which is always useful.

Authentication of users can be done with Goolge OpenID or Github, and comes
with great instructions on how to deploy to Heroku, which will help you get up
and running quickly.

While I haven't had a chance to use Descartes myself, I would trust anything
that [Jason Dixon](https://github.com/obfuscurity) puts out - he is one of the [Graphite Project](https://github.com/graphite-project?tab=members) maintainers 
and did the Tasseo dashboard (see above), so you know he knows his stuff.
His blog is full of useful [Graphite tips](http://obfuscurity.com/Tags/Graphite).

## Other Dashboards
While not specifically Graphite dashboards, the following get an honourable
mention:

### [GDash](https://github.com/ripienaar/gdash)
[{% img right /images/posts/dashboards-for-graphite/gdash.png 200 100 GDash %}](https://github.com/ripienaar/gdash)
This dashboard is not client-side (it uses Graphite's internal renderer for 
images) or database backed, so it's more of a "skin" on the default dashboard. 
It lets you configure your dashboards using YAML, and is built on the Twitter
Bootstrap web-framework.

### [Graph Explorer](https://github.com/Dieterbe/graph-explorer)
[{% img right /images/posts/dashboards-for-graphite/explorer.png 300 150 Graph Explorer %}](https://github.com/Dieterbe/graph-explorer)
While this isn't a dashboard (like the others in this list), it's a new take on
metric exploration for Graphite. Made to be very interactive, it can definitely
help you decide what metrics to include in your dashboard. The nice thing is
that he graphs created are interactive, which is a big improvement over the
usual metric explorer built-in to Graphite.

### [Dashing](http://shopify.github.com/dashing/)
[{% img left /images/posts/dashboards-for-graphite/dashing.png 200 200 Dashing %}](http://shopify.github.com/dashing/)
A general-purpose dashboard by the boffins at [Shopify](http://www.shopify.com/), Dashing can accept data
from many different sources, and display many different types of data through
various widgets. This includes being able to display Graphite data through
direct calls to the Render URL API (you'll have to roll them yourself), and
display them using their Rickshaw graph widget.

I'm a big fan or Dashing for non-technical dashboards because it can accept so
many types/sources of data, and looks great out of the box. They also have a
gauge widget which works really nicely with the StatsD's gauge metrics.
The have a [great demo of the various widgets in action](http://dashingdemo.herokuapp.com/sampletv).

## Need Help?
There you have it! If you guys have any experiences or comments for these
dashboards, let me know below. If you have any dashboards I missed, please let
me know in the comments.

If you need any help setting up any of these dashboards, or Graphite itself,
check out [my dashboard consulting services](/services) and [get in touch with me](/contact).
