# CSS Regions, and why you’ll be using them before you know it

CSS Regions is a [W3C working draft][1] that allows you to flow text between
different areas of a page. The simplest use-case might be column layouts, where
each column is an explicit region, but the powerful part is that the regions
don’t have any constraints on their position or size. This means that columns
barely scratch the surface of the full power of regions, as evidenced by having
their [very own w3c spec][2].

The quickest way to see how powerful regions are is with a window-resizing
example. This example contains a single div of content that flows across four
regions. The re-flow between regions occurs as the window resizes, ensuring that
each word of the content seamlessly renders in its correct region. This screen
capture shows the finished result:

<iframe class="youtube-player" type="text/html" src="http://www.youtube.com/embed/sOaFizRIhFE?version=3&amp;rel=1&amp;fs=1&amp;showsearch=0&amp;showinfo=1&amp;iv_load_policy=1&amp;wmode=transparent" frameborder="0" height="400" width="640"></iframe>

To try it out yourself [on codepen][3], follow along with the following three
sections that explain:

1. *Where/When can we use CSS regions (as of September 2013)*
2. *How* to use CSS regions
3. *Why* we’re going to want to use CSS regions in the future

By the end of this article I hope you’ll be busting out your experimental
browser and hacking some awesome regions into your own site!

## Where/When can I use CSS Regions?

Unless you’re running a pretty bleeding edge browser your might not see the nice
regions when browsing [our example][4]. At first glance, the [caniuse page][5]
for CSS regions seems to suggest you need a copy of IE10+, or a beta of Safari
and that’s your lot. But the real story is a little more subtle:

* IE10+ works but requires content to come from an iframe. (Let’s ignore this 
for now).
* Safari 6.1 (currently beta) just works, using the -webkit- prefix
* MobileSafari in iOS7 just works, using the -webkit- prefix
* Google Chrome Canary (or version 29+) works once “web platform experimental 
features” are enabled, also using the -webkit prefix
* Opera only works if you’re running a webkit-based version, with the -webkit 
prefix
* Firefox has no support right now, favoring the [CSS Overflow][6] draft for 
some of the use cases that regions solve

For curious developers, you can get a fine-grained view on rendering engine
support: the CSS working group maintains a [test suite results page][7] showing
exactly what works under the hood in the main rendering engines.

## *How* to use CSS regions

Regions require two simple concepts: a block of content where the content will
flow-from, and one or more blocks that the content will flow-into. The following
DOM structure reflects this:

    <div class="content">Lorem ipsum etc... All your real content here</div>
    <div class="myregion" id="region1"></div>
    <div class="myregion" id="region2"></div>
    <div class="myregion" id="region3"></div>

The following CSS turns the `myregion` divs into regions. Combined with a float
and a width restriction, the lorem ipsum content will flow into three columns:

    .content {
      flow-into: myipsum;
      -webkit-flow-into: myipsum;
    }

    .myregion {
      flow-from: myipsum;
      -webkit-flow-from: myipsum;

      float: left;
      width: 100px;
    }

In the above example, `myipsum` is the name we gave to this particular region
setup. Separate names allows us to use regions to layout several pieces of
content.

We’re not restricted in the stylings and structure of our regions. We can add
another large region below the columns, or another with absolute positioning. We
can add many more regions if we wanted extra columns. We could lay out the
regions with a flexible box if we want form a fluid layout with them. And so on:
the possibilities are extensive.

Take a look at the [interactive example on codepen][8] I put together to get a
flavor of how content flows between regions.

## *Why* we’re going to use CSS regions in the future

The above only scratches the surface of what’s possible with regions. We could
create more columns, or we could use [transforms][9], [transitions][10] and
[animations][11] to create a moving carousel full of rotating content that
expands and re-flows as the window resizes.

We can create responsive layouts that adapt to phone, tablet or desktop layouts,
and adapt our fluid layouts even further for users with super-massive displays
instead of locking the width or expanding to an absurd width.

Once browser support cements further, things like [Book.js][12] give us a hint
of things to come. It’s an experimental Javascript library that takes your
semantic mark-up and a simple configuration to make web pages look like book
pages. It uses css regions under the hood. The source gives [full usage
instructions][13].

Finally, with MobileSafari getting in on the action (as announced in the iOS7
WWDC keynote), combining gestures on touch devices with regions gives us the
capabilities to build really interesting, interactive magazine-style experiences
on the web.

## Next steps

**Get yourself a browser that supports regions** – either download [Google 
Chrome Canary][14] and set *“Enable experimental Web Platform features”* in the 
“`about:flags`” page, get hold of IE10+, or get a beta from the [Safari Dev 
Center][15].

**Try out** [the codepen above][16], fork it, hack it, extend it, then post 
your creations in the comments below.

**Skim or read the** [W3C’s Regions draft][17], it’s full of interesting ideas 
and capabilities to inspire your next project.

Whatever you do with regions, have fun!

[1]: http://www.w3.org/TR/css3-regions/
[2]: http://www.w3.org/TR/css3-multicol/
[3]: http://codepen.io/guybrush0/pen/ExyJf
[4]: http://codepen.io/guybrush0/pen/ExyJf
[5]: http://caniuse.com/css-regions
[6]: http://www.w3.org/TR/css-overflow-3/
[7]: http://test.csswg.org/harness/results/css-regions-1_dev/grouped/
[8]: http://codepen.io/guybrush0/pen/ExyJf
[9]: http://www.w3.org/TR/css3-transforms/
[10]: http://www.w3.org/TR/css3-transitions/
[11]: http://www.w3.org/TR/css3-animations/
[12]: http://sourcefabric.github.io/BookJS/
[13]: http://sourcefabric.github.io/BookJS/book.js
[14]: https://www.google.com/intl/en/chrome/browser/canary.html
[15]: https://developer.apple.com/devcenter/safari/index.action
[16]: http://codepen.io/guybrush0/pen/ExyJf
[17]: http://www.w3.org/TR/css3-regions/