---
layout: post
title: "Dashboard: Giraffe"
date: 2013-12-16 16:00
comments: true
categories: dashboard review Graphite visualization JavaScript Giraffe
---

Giraffe is great example of what's possible with a JavaScript-only dashboard on top of Graphite data. Like many other Graphite dashboards, it's built on top of [D3.js](). It differs slightly because it's made with the [Rickshaw graphing library](http://code.shutterstock.com/rickshaw/) instead of using D3.js directly, which gives it some nice polish.

![graph](/images/posts/dashboard-giraffe/demo.png "Giraffe Dashboard")

<!--more-->

### Features

* Stackable metrics.
* One-click changing between (pre-set) time periods.
* Customizable summary methods and display information.
* Configuration is done with JavaScript objects.

### Good For

* **Browsing time periods** is really easy. With one click you can see you metrics with fidelity from 10 minutes to 7 weeks (and a bunch of sensible values in-between).
* **No server is required**, so getting up and running is as simple as editing `dashboard.js` and opening the directory in your browser locally.
* **Detailed example dashboards** are provided, so you can follow along.
* **Stacking similar metrics** is a simple as using a wildcard or specifying multiple targets, and they'll all show up on one graph.
* **Its summary details/legend** can be shown/hidden as part of the display. It includes things like the range of values over the viewed time period, which is a nice time-saver for relevant metrics.

### Not so Good For

* **Viewing lots of metrics** starts to eat a lot of RAM (regardless of how they're laid out). This issue is probably caused by Rickshaw (rather than Giraffe), but knowing that doesn't solve the problem.
* **The layout doesn't use the all space available**, which makes it less attractive as a monitoring dashboard. The config defaults to a 3-graphs-per-row layout, and while you can make graphs span multiple columns (even more than the default 3), I couldn't get the graphs to scale-out to my wide display.
* **Fine metrics being compared to each other** can be difficult to see because multiple metrics on one graph are stacked. Being stacked means that the ordering of the metrics is important, and it's not easy to change on the fly (you have to edit the dashboard configuration object). Note that you can toggle the visibility of metrics in the interface, but this still requires some manual intervention.
* **Configuration is a bit complicated**, but only because  there are a lot of options/aliases/etc. It's much easier to set up when you already have a clear idea of the metrics you want to display.

## Summary

I would use this dashboard to quickly access and browse (historically) metrics that I know are important, but might not be my 'top' monitoring metrics.

I don't think I would use this as my main monitoring dashboard (ie. on a big-screen for everyone to see all the time) because of the manual intervention and fine-grained detail, but those extra details make it a good for specific metrics/tasks.

### Links

* Check out a [sample dashboard](http://giraffe.kenhub.com/).
* The project [GitHub page](https://github.com/kenhub/giraffe).

## More to Come

If you're interested in finding out more about JavaScript dashboards for
Graphite, don't forget to sign up to the mailing list!

<!-- Begin MailChimp Signup Form -->
<div id="mc_embed_signup" style="text-align: center;">
<form action="http://learnfastmath.us2.list-manage.com/subscribe/post?u=73d02cd94a0c4a3fa258d4d12&amp;id=9d0805d199" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
  <label for="mce-EMAIL">Get Updates From The Dude</label>
  <input type="email" value="" name="EMAIL" class="email" id="mce-EMAIL" placeholder="email address" required>
  <div class="clear"><input type="submit" value="Subscribe" name="subscribe"
    id="mc-embedded-subscribe" class="button"></div>
</form>
</div>
<!--End mc_embed_signup-->
