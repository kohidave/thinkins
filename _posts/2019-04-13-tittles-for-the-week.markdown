---
layout: post
title:  "Time is so weird"
date:   2019-04-13 12:09:00
categories: tittles
---


_Tittles are the fun bits of information that I've learned, found interesting or had conversations about in the past week. This week's tittle is inspired by Matt Parker's new, awesome book [Humble Pie](https://www.amazon.com/Humble-Pi-Comedy-Maths-Errors/dp/0241360234/)._

## What's a year?

Take a second and think of a few units of time. Seconds, minutes, hours, days, months, fortnights, weeks, years. If I were to ask you how each of these units were defined, you might say something like: "A minute is defined as 60 seconds. An hour is defined as 60 minutes. A second is..."

If you just assume there's a unit of time called a second, you can create other units of time relative to that base unit. But what the heck is a second? The truth is, the absolute value of a second doesn't have a huge intrinsic value - its value is in that it's defined and constant. 

### Wait, what's a second?

But how that value is defined might depend on what you use time for. Maybe you want the duration of a second to just be consistent so that you can share your bread recipe with your friends and you can tell them exactly how long to leave the dough in the oven. In this case, we don't actually care about what a second is, we just care that we have a common description of time. 

![A pendulum defining a second](/assets/images/clock-pendulum.gif)

So since we don't care what a second really is, let's just define it based on the acceleration of gravity? A pendulum is an amazing pice of machinery. The time it takes the pendulum to complete a full swing (from left to right back to its starting point) is a function of the pendulum's length and the acceleration of gravity (pendulums also have a cool property of isochronism where, even if the length of their swing decreases due to friction, the length of time to complete that period remains the same). 

{% raw %}
$$T = 2\pi\sqrt{\frac{L}{g}}$$
{% endraw %}

Sweet - so the length of time our pendulum swings can be our second. So long as everyone is using the same length pendulum - we've defined a consistent second! But wait, isn't this cheating a little? We're defining a second based off a value which is already in terms of seconds, the force of gravity. If we take the acceleration of gravity as given, then we can definitely use these cool pendulums to have an easy to produce, widespread counter of seconds. 

### Wait, what's gravity?

Oh my. Our little illusion of time is starting to unravel. Remember earlier when we were just trying to define what a year is? Simpler times. So, full disclosure, I'm not a physicist so bare with me. Our current task is to figure out where the magic  {% raw %}$$g=9.8\frac{m}{s^{2}}$${% endraw %}. That's actually not so hard, especially if you allow me to use Newton's law of universal gravitation. 

> Newton's law of universal gravitation states that every particle attracts every other particle in the universe with a force which is directly proportional to the product of their masses and inversely proportional to the square of the distance between their centers

That means that you can calculate a gravitational force between two objects, in general as with this formula:

{% raw %}
$$F = G\frac{m_{1}m_{2}}{r^{2}}$$
{% endraw %}

Sorry, I haven't defined any of these letters. In our case, __F__ represents the force gravity exerts between two forces. __m1__ and __m2__ are the two actors gravity is acting on. __r__ is the distance between the two actor's centers. And __G__ is problematic... it's a constant and we'll talk about it in a few minutes. Let's see if we can calculate what __F__ is for our pendulum on Earth. 

In our case, we can fill in these variables as:

__m1__ will be Earth, which comes in at a clean __5.97 * 10^24 kg__
__m2__ will be our pendulum, which we can guess as __1 kg__
__r__ is the distance from our pendulum to Earth's surface, which is about __6371 km__
__G__, our mysterious constant is defined as __6.67408×10^−11 m^3⋅kg^−1⋅s^−2__


{% raw %}
$$F = \frac{6.67408 \cdot 10^{-11} m^{3}}{kg \cdot s^{2}} \frac{5.97 \cdot 10^{24}kg \cdot 1kg}{(6.371×10^{6})^{2}m^{2}}$$
{% endraw %}

{% raw %}
$$F = \frac{6.67408 \cdot 10^{-11} m}{s^{2}} \frac{5.97 \cdot 10^{24}}{(6.371×10^{6})^{2}}$$
{% endraw %}

{% raw %}
$$F = \frac{3.98442576 \cdot 10^{14} m}{4.0589641 \cdot 10^{13} s^{2}} $$
{% endraw %}

{% raw %}
$$F = \frac{3.98442576 \cdot 10 m}{4.0589641 s^{2}} $$
{% endraw %}

{% raw %}
$$ F = g \approx 9.817 \frac{m}{s} $$
{% endraw %}


Sweet! We calculated the force of gravity on our pendulum! We can just plug that into our pendulum period equation 🙌

### Wait, what's the universal gravitational constant

I had this weird hope that maybe you'd just not ask about that. 

{% raw %}
$$ G = \frac{6.67408 \cdot 10^{−11}}{kg \cdot s^{2}} $$
{% endraw %}

There it is. Staring at us, in contempt. This amazing number. This is the very heart and essence of gravity and is used to describe everything from the [limits of time](https://en.wikipedia.org/wiki/Planck_time) and the [limits of space](https://en.wikipedia.org/wiki/Planck_length). But where does it come from? Well let's take a look at the wiki entry for it:

> The gravitational constant (also known as the "universal gravitational constant", the "Newtonian constant of gravitation", or the "Cavendish gravitational constant"), denoted by the letter G, is an empirical physical constant involved in the calculation of gravitational effects in Sir Isaac Newton's law of universal gravitation and in Albert Einstein's general theory of relativity.

The key here is that it's an _"an empirical physical constant"_ meaning it's derived from experiments. We have to observe this value in order to know it - we can't just calculate it. Moreover, __G__ is considered a _"fundamental constant"_ which means we have no idea why the value is what it is!

So this is kind of the end of the road of this exploration. _G_ is still in terms of seconds, so it doesn't help us figure out what the heck a second even is.

### The less satisfying answer

So we went through this rabbit hole. We took an object that had to do with time and was used to measure time, a pendulum, dissected the physical formula which defined it, and dug into that. We saw that the temporality of our pendulum came directly from the temporality of the force of gravity. We dug into that, to try and understand gravity and time. Eventually we found the very essence relating gravity and time, but realized it was just a constant. It simply relates the time and force but it doesn't define time. 

To really understand what a second is, we've got to look to the sky. 

![A Sundial View From Above](/assets/images/equatorial_sundial.gif)

Sundials are so cool - they cast a shadow relative to the position of the sun in the sky. Every day, at exactly noon, a correctly configured sundial will point either directly north or south. The earth will rotate 360 degrees, and then it'll be noon again. Every 15 degrees of that 360 degree rotation would define an hour (and 360/15 is 24, so 24 hours in a day - a day the interval between two successive returns of the Sun to the local meridian). This method of tracking time is called "apparent solar time" and has the obvious flaw that for us non-equatorial residents, the amount of time we see the sun differs between the months as the Earth spins on its axis.

While this isn't perfect, it's pretty good - and our problem changes from defining what "time" is, to minimizing seasonal differences. With some astronomy and math, you could calculate how far off you were from the "mean" solar time - the time that an imaginary sun would travel across the celestial equator. If you applied these corrections, you could get a consistent time, across seasons, derived by the apparent solar time. 

Since we have 24 hours in our sundial day (15 degree moments on our sundials representing an hour), and there are 60 minutes in an hour and 60 seconds in a minute (this is all just by definition), a solar day should have 86,400 seconds in it. This was the truth until the 1950's, when we discovered some unpredictable irregularities in the Earth's rotation which and had to add "leap seconds" to adjust for these variations. 

But not getting too deep into the astronomy of the solar day, that's where our definition of a second comes from. It's derived astronomically - from the sun. When we discovered we could use atoms to measure frequency without the instability of Earth's "unpredictable" rotation, we switched to them. We took an ideal solar second, calibrated our atomic clocks to that, and now have a reliable second. 

