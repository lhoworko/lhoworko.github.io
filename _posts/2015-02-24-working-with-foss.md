---
layout: post
title: Working With FOSS
---


<!--excerpt-->

INTALLATION

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


