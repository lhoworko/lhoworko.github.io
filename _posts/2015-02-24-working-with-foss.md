---
layout: post
title: Working With FOSS
---

I have been wanting to get involved with an open source project for a while now. I was quite happy when I found out that I'd be required to work with FOSS for a school assignment, it would finally make me commit to a project. I had a few projects in mind, some in C, others in Javascript, but regardless of the language I wanted it to be a project that I actually use. So with some direction and an end goal I set out to find a project I wanted to contribute to.

<!--excerpt-->

The first project I came across was [VLC player](https://github.com/videolan/vlc). I have used it for a while but never acturally knew it was open source until I found it on GitHub. Ok, great, so I forked it, cloned it, and set out to build it on the CS50 machine. And... no luck. I don't know if I took a wrong turn somewhere but VLC just wouldn't cooperate. Ok, fair enough, lets try another.

I've been using [Atom](https://github.com/atom/atom) -- the new open source text editor from GitHub -- for a few months, that would be a great project. I've never worked with CoffeeScript, but after a bit of Google foo I think I can handle it. So again, fork, clone, build, no luck. It seemed that nothing was cooperating with the CS50 machine, and after some further Googleing I found out that Atom won't build on 32 bit machines. Well thankfully for me Cam allowed me to work on OSX where I was able to build Atom without any problems.

And with that I will introduce my first artifact. I thought it would be appropriate to provide complete build instructions for anyone looking to build Atom on OSX Yosemite. The installation instructions can be found below.

<h2>Installation</h2>

Building the code from source is the first step to working with an open source project. For that reason I will go through the steps that I took to get Atom built and installed on OSX Yosemite. There are a few requirements for Atom, all of which I will explain as we come to them.

The first thing we have to do is clone the Atom repository. I have the code forked into my own account, so that is where I will pull from. Assuming you have git installed run the following command to clone the repo.

{% highlight bash %}
git clone https://github.com/lhoworko/atom.git
{% endhighlight %}

Building Atom on OSX has a few requirement. First of which is node.js v0.10 or later. To check your current node version run the following command.

{% highlight bash %}
node --version
{% endhighlight %}

If you don't have node installed at all you can find a nice set of instructions [here](http://thechangelog.com/install-node-js-with-homebrew-on-os-x/).

Once we have node installed the next requirement is Xcode. The build instructions in the atom repo say you only need the Command Line Tools, but even with them the build process spit out a bunch of errors, all of which Xcode gets rid of. If you only want the Command Line Tools run the following command.

{% highlight bash %}
xcode-select --install
{% endhighlight %}

As for Xcode itself you can find that for free in the app store.

Once we are set with node and Xcode we can actually build Atom. The following command will build and install Atom, making it extremely easy.

{% highlight bash %}
atom/script/build
{% endhighlight %}

This will take awhile to run but once it's done you should have a fully functional build of Atom. The default location of Atom is in /Applications/Atom.app, so it's easily found in the Launchpad. It can also be launched from the command line by simply running 'atom'.
