---
layout: post
title: "Dashing Dashboard Widget Challenge: The Hotness"
date: 2013-08-16 14:49
comments: true
categories: Dashing dashboard widget challenge
---

{% img right /images/posts/dashing-hotness-widget/hot.png 250 250 Hot hot hot!%}

The friendly [David from Shopify](https://twitter.com/davefp) contacted me
recently about the [Shopify Widget Challenge](http://dashing.challengepost.com/) that they're holding. I've
written about [Dashing before](/blog/2013/01/23/dashboards-for-graphite), and
I'm a big fan of its style and versatility.

It didn't take me long to think of some widget ideas, so I thought I'd share
what it took for me to enter the challenge with a basic idea.

<!--more-->

## My Idea

The idea I had was for a widget that changed colour, depending on the value it
is displaying - kind of like the Meter and Number Widgets that comes with
Dashing, but __hotter__.

My plan is for this to be a big, bold, colourful way of
drawing focus to metrics which need immediate attention (because something's
about to explode, etc).

It's worth noting that the Number widget actually has (undocumented?) 'warning'
and 'danger' values that can be set (which cause the widget to pulse), but these
require a status to be set on the data sent to the widget (from the job). I
wanted something that would 'just work' with numerical data, as it's a common
use-case I see.

## The Dashing Dashboard

The [Dashing page](http://shopify.github.io/dashing/) has the basic information
you need to create your own widget:

> Anatomy of a widget
>
> an HTML file used for layout and bindings
> 
> a SCSS file for styles
> 
> a coffeescript file which allows you to handle incoming data & functionality

That combined with the [existing examples](https://github.com/Shopify/dashing/tree/master/templates/project/widgets)
and the [3rd party widgets](https://github.com/Shopify/dashing/wiki/Additional-Widgets) as
reference points means that there are plenty examples out there to learn from.

## My Widget

### HTML Template

The template I decided was appropriate was super-simple - this widget is really
only trying to convey a single value, so I based it off the 'vanilla' Number
Widget.

    <h1 class="title" data-bind="title"></h1>

    <h2 class="value" data-bind="value | shortenedNumber | prepend prefix | append suffix"></h2>

    <p class="updated-at" data-bind="updatedAtMessage"></p>

This just shows the title (if present), value (in a shortened format, with
prefix and suffixes - if present), and finally a small 'updated at' message (as
most widgets in Dashing do).

## Styling with SASS

{% img left /images/posts/dashing-hotness-widget/cool.png 250 250 Everything's cool%}

Dashing comes with [SASS](http://sass-lang.com/) support, which is another nice
touch by the developers.

I had originally hoped to auto-generate the colour spectrum for the widget
using some of SASS' [advanced colour methods](http://nex-3.com/posts/89-powerful-color-manipulation-with-sass), but
in the end I decided to keep it simple for this first version, and use a
palette created by [Nekyo](http://www.colourlovers.com/lover/nekoyo) called
[Sweet Lolly](http://www.colourlovers.com/palette/56122/Sweet_Lolly). I found
this through the [COLOURlovers](http://www.colourlovers.com/) site, and grabbed
it because I really wanted something that went from green to red, with yellow
in the middle.

### CSS3 Transitions

After reading this [great description of CSS3 transitions](http://css3.bradshawenterprises.com/transitions/), I created the
required SCSS for my widget. In order to make the code a little more readable,
I included a
[mixin](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#mixins) to
handle all the browser-specific directives:

    @mixin transition($transition-property, $transition-time, $method) {
      -webkit-transition: $transition-property $transition-time $method;
      -moz-transition: $transition-property $transition-time $method;
      -o-transition: $transition-property $transition-time $method;
      transition: $transition-property $transition-time $method;
    }

Which meant that when I wanted to transition the background-color for my
widget, all I need to include in the SCSS is:
  
    @include transition(background-color, 1s, linear);

### CoffeeScript Functionality

{% img right /images/posts/dashing-hotness-widget/neutral.png 250 250 %}

The widget functionality resides in a CoffeeScript/JavaScript file, which will
be included by Dashing at runtime. All of the included widgets are written in
CoffeeScript, so I wanted to keep consistent with that. I'm also a big fan of
CoffeeScript - I find it a bit more maintainable than JavaScript, especially for
small files like this.

#### The onData Event

In my basic widget, all of the magic happens in the `onData` event, which all widgets
receive when (surprise surprise!) data is sent to them by the scheduled jobs.

All I needed to do was change (toggle) the background colour (using CSS) of the
widget to represent its place between two user supplied values: 'warm' and
'cool'. Anything outside those values will be shown as 'hot' and 'cold'
respectively (ie. the max and min colour values). Anything inside those values
will use an interpolated value from three possible choices (cool, neutral, and
warm).

There's also a `ready` event, which fires when the widget is first loaded (ie.
when the page is loaded). This could be useful to configure the widget in a
certain way, depending on user settings, etc.

Here's the `onData` listener that makes the widget work (in CoffeeScript):

    onData: (data) ->
      node = $(@node)
      value = parseInt data.value
      cool = parseInt node.data "cool"
      warm = parseInt node.data "warm"
      level = switch
        when value <= cool then 0
        when value >= warm then 4
        else 
          bucketSize = (warm - cool) / 3 # Total # of colours in middle
          Math.ceil (value - cool) / bucketSize

It could've easily been shortened to a few lines, but I like taking a few extra
to make it a even more readable.

## Conclusion

Hopefully this will help you create your own widgets for Shopify's Dashing
Dashboard.

Kudos to the Shopify guys for making a cool piece of software, and making it so
easy to extend!

If you've got a good idea for a widget (and it's not after September 13th,
2013), you should enter the [Shopify Widget Challenge](http://dashing.challengepost.com/)!

{% img center /images/posts/dashing-hotness-widget/cold.png 250 250 Green is good%}
