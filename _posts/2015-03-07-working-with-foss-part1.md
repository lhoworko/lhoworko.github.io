---
layout: post
title: Working With FOSS, Part 1
---

As part of assignment 2 in Cmpt395 I have been tasked with finding and working with, in some way, an open source project. When I read about this assignment I was quite excited as I've been wanting to get involved with FOSS for a while now. What has always stopped me in the past was usually one of two things; I didn't think a project interested me enough, or that I wasn't a good enough developer to contribute anything useful. Well, with the push this assignment has given me I suppose I no longer have any excuses holding me back. So that is why I have chosen to dive into Atom, the open source text editor from GitHub, as my first open source project.

<!--excerpt-->

<h3>VLC Player</h3>

Before I decided on Atom, the first open source project I looked at was [VLC Player](https://github.com/videolan/vlc). I have used VLC Player for quite a while but never actually knew it was open source until I found it on GitHub. Ok, so I forked it, cloned it, and set out to build it on the CS50 virtual machine. After hours of frustrations I could not get it to build. In the end I believe the problem was that CS50 is a 32 bit machine, whereas VLC requires 64 bits to build. Ok, fair enough, I suppose that's the trouble with FOSS. At this point I moved onto Atom.

<h3>Atom</h3>

I've been using [Atom](https://github.com/atom/atom) -- the new open source text editor from GitHub -- for a few months so I figured that it would be a great project to work with. I looked over the project on GitHub, and although I've never worked with CoffeeScript with a bit of Google foo I think I can handle it. So again I fork it, clone it onto CS50, and build it. No luck. This was prior to my epiphany about the 32 bit machine and funny enough in the Atom repo it specifies that it requires 64 bits to build. Thankfully in the end Cam allowed me to work on OSX where I was able to build Atom without any problems.

And with that I will introduce my first artifact. I thought it would be appropriate to provide complete build instructions for anyone looking to build Atom on OSX Yosemite. The installation instructions can be found below.

<h2>Installation</h2>

Building the code from source is the first step to working with any open source project. For that reason I will go through the steps that I took to get Atom built and installed on OSX Yosemite. There are a few requirements for Atom, all of which I will explain as we come across them. The instructions I followed when I built it were straight from the Atom [repository](https://github.com/atom/atom/blob/master/docs/build-instructions/os-x.md).

The first thing we have to do is clone the Atom repository. I have the code forked into my own account so that is where I will clone from. Assuming you have git installed run the following command to clone the repo.

{% highlight bash %}
git clone https://github.com/lhoworko/atom.git
{% endhighlight %}

<h3>node.js</h3>

Building Atom on OSX has a few requirements, the first of which is [node.js](https://nodejs.org/). We require node v0.10.x, so if you already have node installed check the version with:

{% highlight bash %}
node --version
{% endhighlight %}

If you are beyond 0.10, you are good to continue. If you don't have node installed at all you can find a nice set of instructions [here](http://thechangelog.com/install-node-js-with-homebrew-on-os-x/). Updating node is different based on the way it was first installed. [This Stack Overflow thread](http://stackoverflow.com/questions/11284634/upgrade-nodejs-to-the-latest-version-on-mac-os) gives instructions for each way to update on OSX.

<h3>Xcode</h3>

Once we have node installed the next requirement is [Xcode](https://developer.apple.com/xcode/). The build instructions in the atom repository say you only need the Command Line Tools, but even with them the build process spit out a bunch of errors. It did build with only the CommandLineTools, but all of the error were taken care of with Xcode installed. If you only want the CommandLineTools run the following command.

{% highlight bash %}
xcode-select --install
{% endhighlight %}

As for Xcode itself you can find that for free in the [app store](https://itunes.apple.com/ca/app/xcode/id497799835?mt=12).

<h3>Build</h3>

Once we are set with node and Xcode we can actually build Atom. The following command will build and install Atom, making it extremely easy.

{% highlight bash %}
atom/script/build
{% endhighlight %}

This will take awhile to run but once it's done you should have a fully functional build of Atom. The default location of Atom is in /Applications/Atom.app, so it's easily found in the Launchpad. It can also be launched from the command line by simply running 'atom', which will open in the context of the directory it was launched from.

Now that Atom is built and installed we are ready to play around with it. Take note, if you wish to rebuild atom after making changes it's as easy as running the build script again. It actually runs significantly faster as no localization files need to be installed again.

<h2>Playing Around With Packages</h2>

So once I had Atom installed I started looking around to see what I could find. I looked thought documentation, some of the bug reports, trying to find something I could experiment with. I came across packages, small add-ons that enhance the functionality of the editor, and decided that was as good of place as any to start. So for my second artifact I've decided to follow a tutorial and write a small, easy package to get my feet wet, something to introduce me to how the process of writing them works. The tutorial I followed, located [here](https://atom.io/docs/v0.64.0/your-first-package), replaces the selected text with ascii art. I know it doesn't sound amazing, but I have to start somewhere.

Atom makes it very easy to create new packages. Basically find 'Generate Package' in the menu and Atom creates a default package that we can extend. Following the tutorial was fairly straight forward, the only place I got hung up was on the CoffeeScript syntax. Other than that it was quite simple. The ease of creating the package was suprising, but more so was the ease at creating key bindings. By just adding the method to the package.cson file it basically does it for you. This was my first experience at writing a package for anything, but if this is how enjoyable Atom makes it I'm sure I will be back to write something real.

To satisfy the assignment requirement I thought I should include some images and code fragments for what I actually did. As I said before, the key binding was incredibly simple. They actually have a CSS style syntax that allows you to define the scope for which the key binding will work. For example, in this tutorial the scope is set to the editor window only, entering the shortcut has no effect when the file tree has focus. I could definately see how handy that would be, allowing the same key binding to have diferent effects based on window focus. Anyways, here is what the key binding code looks like.

{% highlight js %}
'atom-text-editor':
    'ctrl-alt-a': 'ascii-art:convert'
{% endhighlight %}

You just tell it what method you want to call, 'convert', and the shortcut, 'ctrl-alt-a'. You can also see the scope, 'atom-text-editor'.

Here it is in action:
<a href="http://imgur.com/6mdYkQx"><img src="http://i.imgur.com/6mdYkQx.png" title="source: imgur.com" /></a>
<a href="http://imgur.com/CeZLJZo"><img src="http://i.imgur.com/CeZLJZo.png" title="source: imgur.com" width="720"/></a>

Amazing. Ok maybe not but it's pretty cool to me. I would have never realized how easy it would be.

GitHub repo of the package is hosted by Atom [here](https://github.com/atom/ascii-art)

PasteBin of what I did [here](http://www.pastebin.ca/2947510)

And with that I am done my first post for Cmpt395 assignment 2. In the coming weeks there will be a second post where I explore some other artifacts related to FOSS. Thanks.
