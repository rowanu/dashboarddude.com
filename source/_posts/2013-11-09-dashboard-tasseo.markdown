---
layout: post
title: "Dashboard: Tasseo"
date: 2013-11-09 18:00
comments: true
categories: dashboard review Graphite visualization JavaScript Tasseo Obfuscurity
---

So I lied. The first of my series of [dashboard reviews](/blog/2013/09/09/dashboard-reviews/) is NOT on Dusk, but one of
Obfuscurity's other great dashboards: [Tasseo](https://github.com/obfuscurity/tasseo).

## Tasseo
[Tasseo](https://github.com/obfuscurity/tasseo) is a small, lightweight dashboard that's good for throwing together a
useful monitoring dashboard in a minimal amount of time. It's built with
[Rickshaw](http://code.shutterstock.com/rickshaw/) graphs (themselves based on
the fantastic JavaScript library [D3.js](http://d3js.org/)) on top of a small
[Sinatra](http://www.sinatrarb.com/) application.

![graph](https://github.com/obfuscurity/tasseo/raw/master/lib/tasseo/public/i/tasseo.png
"Tasseo Dashboard")

<!--more-->

### Features
* Configuration for dashboards is done with simple JavaScript Objects.
* You can set value thresholds for changing the colour of a graph from green
  (default), yellow (warning), and red (critical).

### Good For
* **Getting up and running quickly.** There's just enough configuration options,
  but not too many. This can get you from the default Graphite dashboards (which
can be a bit hard on the eye) to a nice looking monitoring dashboard in minutes,
not hours.
* **Showing specific, discrete metrics** for a high-level operations dashboard.
* Metrics you want to set visual thresholds for.

### Not so Good For
* **Displaying large numbers of metrics.** The layout eats in to your total
  space (if you want to display lots of similar metrics, look at horizon charts
like Dusk instead).
* **Discovering new important metrics.** Mainly because it doesn't show a large
  number of metrics, you're unlikely to find out new key metrics while using
Tasseo.
* **Viewing metrics in detail over time.** There's no rulers showing you what
  the values in the chart represent, so it can be hard to know what the exact
values were in the past. The current value is displayed numerically, so it's not
an issue if you're only interested in historical trends - not values.
* **Zooming/investigating metrics on the dashboard.** What you see is what you
  get, but it's enough for a high-level monitoring dashboard.

### Links
Check it out on [GitHub](https://github.com/obfuscurity/tasseo).

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
