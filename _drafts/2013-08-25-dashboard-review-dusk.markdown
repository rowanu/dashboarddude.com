---
layout: post
title: "Dashboard Reviews: Dusk"
comments: true
categories: dashboard reviews Dusk graphite visualization
---

## What is Dusk?

Dusk is a Cubism.js-based front-end for Graphite data.  It's another great
pieces of software by the prolific [Obfuscurity](http://obfuscurity.com/) that I
can see being of great use to a lot of businesses who use Graphite.

<!--more-->

If you check out [Cubisim.js'](http://square.github.io/cubism/) project page,
you can see that it's the driving force behind Dusk. Cubism's big feature is
that it uses **horizon graphs** to convey a lot of information in a little
space. One of the main benefits of horizon charts is that it allows for quick
and easy comparison of similar metrics. If you want to get in to the theory
behind them, you should definitely check out <a
href="http://vis.berkeley.edu/papers/horizon/2009-TimeSeries-CHI.pdf">the
original whitepaper (PDF)</a>.

## Usage

Unfortunately, there's no **one dashboard to rule them all** - different
dashboards are good (and bad) for different things. Here's what I think you
should use Dusk for:

### Good For

You should use Dusk if you have a lot of similar metrics that you need to
compare. An example of similar metrics with a relationship might be the CPU of
nodes in a cluster - Dusk is ideal for seeing when events start to impact
multiple instances of your metrics (ie. each node).

### Bad For

Metrics which don't have the same scale. While you could use Dusk to monitor
different metrics on the same dashboard, you would really want to make sure they
have a similar scale (eg. within an order of magnitude of each other). While you
can display the metrics together, having to adjust mentally for different scales
across a large number of metrics is not a good idea.

### Configuration

Obfuscurity states in the [post on
Dusk](http://obfuscurity.com/2013/06/Dusk-Yet-Another-Graphite-Dashboard) that
he wanted to avoid any external requirements, and as such configuration is
simple and all done through URL parameters.

TBC

## Links

* [Dusk on Github](https://github.com/obfuscurity/dusk)
* [Obfuscurity's post](http://obfuscurity.com/2013/06/Dusk-Yet-Another-Graphite-Dashboard)
* [Cubism on Github](https://github.com/square/cubism)
