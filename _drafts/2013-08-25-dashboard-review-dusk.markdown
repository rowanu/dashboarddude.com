---
layout: post
title: "Dashboard Reviews: Dusk"
comments: true
categories: dashboard reviews Dusk graphite visualization
---

## What is Dusk?

Dusk is a Cubism.js-based front-end for Graphite data.  It's another great
pieces of software by the prolific [Obfuscurity](http://obfuscurity.com/).

TBC

### Cubism.js

If you check out [Cubisim.js'](http://square.github.io/cubism/) project page,
you can see that it's the driving force behind Dusk.

TBC

## Usage

Unfortunately, there's no one dashboard __to rule them all__ - different
dashboards are good (and bad) for different things. Here's what I think you
should use Dusk for:

### Good For

You should consider Dusk if you have a lot of similar metrics that you need to
compare. If your metrics have some kind of relationship between them (and not
just that they're the same kind of metric eg. CPU) then that's even better. An
example of similar metrics with a relationship might be the CPU of nodes in a
cluster - Dusk is ideal for seeing when events start to impact multiple
instances of your metrics (ie. each node).

### Bad For

Metrics which don't have the same scale. While you could use Dusk to monitor
different metrics on the same dashboard, you would really want to make sure they
have a similar scale (eg. 0-100). While Cubism.js uses [horizon
charts](http://vis.berkeley.edu/papers/horizon/) to efficiently display metrics,
having to adjust (mentally) for different scales across a large number of
metrics is just not a good idea.

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
