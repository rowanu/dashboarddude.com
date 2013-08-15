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
Dashing, but __hotter__. My plan is for this to be a big, bold, colourful way of
drawing focus to metrics which need immediate attention (because something's
about to explode, etc).

The Number widget actually has 'warning' and 'danger' values that can be set
(which cause the widget to pulse), but these require a status to be set on the
data sent to the widget (from the job). I wanted something that would 'just
work' with numerical data, as it's a commit use-case I see.

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

With that, the [existing examples](https://github.com/Shopify/dashing/tree/master/templates/project/widgets),
and the [3rd party widgets](https://github.com/Shopify/dashing/wiki/Additional-Widgets) as
reference points, there are more than enough examples to make your idea work.

## HTML Template

The template I decided was appropriate was super-simple - this widget is really
only trying to convey a single value, so I based it off the 'vanilla' Number
Widget. You can see it in [HTML template](hotness.html)

## CoffeeScript Functionality

{% img right /images/posts/dashing-hotness-widget/neutral.png 250 250 %}

The widget functionality resides in a CoffeeScript/JavaScript file, which will
be included Dashing at runtime. All of the included widgets are written in
CoffeeScript, so I wanted to keep consistent. I'm also a big fan of
CoffeeScript - I find it a bit more maintainable than JavaScript, and small
snippets like this rarely run in to any issues with getting
CoffeeScript/JavaScript to work nicely together.

### The onData Event

All my file needed to do was listen to the `onData` event, which all widgets
receive when (surprise surprise!) data is sent to them by the schedule jobs.
This event listener would need to:

1. Update the Value displayed.
1. Change the background colour of the widget to represent its place between
two user supplied values: 'warm' and 'cool'. Anything outside those values will
be shown as 'hot' and 'cold' respectively (ie. the max and min colour values).

## Styling with SASS

{% img left /images/posts/dashing-hotness-widget/cool.png 250 250 Everything's cool%}

Dashing comes with [SASS](http://sass-lang.com/) support, which is another nice
touch by the developers.

I had originally hoped to auto-generate the colour spectrum for the widget
using some of SASS' [advanced colour methods](http://nex-3.com/posts/89-powerful-color-manipulation-with-sass), but
in the end I decided to keep it simple for this first version, and use a
palette created by [Nekyo](http://www.colourlovers.com/lover/nekoyo) called
[Sweet Lolly](http://www.colourlovers.com/palette/56122/Sweet_Lolly), which I
found through the [COLOURlovers](http://www.colourlovers.com/) site. I grabbed
this because I really wanted something that went from green to red, with yellow
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

## Conclusion

Hopefully this will help you create a widget for Shopify's Dashing Dashboard.
Kudos to the Shopify guys for making a cool piece of software, and making it so
easy to extend.

If you've got a good idea for a widget (and it's not after September 13th,
2013), you should enter the [Shopify Widget Challenge](http://dashing.challengepost.com/)!

{% img center /images/posts/dashing-hotness-widget/cold.png 250 250 Green is good%}
