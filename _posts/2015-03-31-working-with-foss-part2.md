---
layout: post
title: Working With FOSS, Part 2
---

To continue on from my last post I will go over three more artifacts related to Atom.

<!--excerpt-->

<h3>Artifact 1</h3>

To begin this post off I wanted to review an article I found online that compare Atom to other popular text editors, mainly Sublime. A few months ago I began using Atom after trying a bunch of others, none of which I really enjoyed using. I thought it appropriate to discuss my reasons, as well as well as others, for why I like Atom.

The article was written by Loren Segal and is called [My Week With GitHub's Atom](http://gnuu.org/2014/03/10/my-week-with-githubs-atom-editor/). This article was written just over a year ago so some things have definitely changed but the issues then are still worth talking about.

So the first thing Loren does is mention that Atom is similar to Sublime in almost all ways. This is not the first time I've come across this statement. In fact, it seems that Sublime hit it so far out of the park with Sublime Text 2 that everyone and their dog is making their editor behave the same. Not only with functionality but also colors and layout. I'm not saying I mind, it's just that Sublime Text 2 must have been something very new and exciting at the time to make it the de facto standard for comparing editors.

An exciting feature about Atom is that it is built for web developers using the technologies that web developers know. JavaScript (CoffeeScript), HTML, & CSS are what Atom are built on, making it extremely easy to develop modules and even drastically change the layout and color scheme. One thing I really look for in an editor is being able to customize it to my liking, and with Atom I can easily change the keyboard shortcuts and menu layout as I wish. As for the author, he acknowledges that using HTML is a desktop application is questionable, but in this case it definitely works.

I haven't yet gone too deep into the Git aspects of Atom, but the author notes that considering Atom is built by GitHub there isn't a whole lot of Git functionality built in. There is the ability to diff and see what branch you're on but why not built in commit option? As for Loren he says that it should be there, hopefully in the future.

The next thing mentioned is Atom's performance issues. Perhaps this is one of the things improved since March 2014, but I don't notice what the author states. He notes slow start up (which does happen sometimes) to visible lag while typing (which I've never noticed). He is quite worried about the long term performance of Atom, stating that as the editor grows it will only get worse, something that the guys at GitHub must have already solved.

The author continues his critical stance on Atom with his discussion of the API. My only experience with the API was in my previous post where I followed the tutorial to create a simple package. I quite enjoyed that but obviously that just scratched the surface of what is available. Loren states that everything seems to be half done, "as if they decided they were going to write a text editor app half way through implementing the text editor component". Ok, lets see what he means by this.

Documentation. Or actually the lack of it. What is there is wrong or misleading, and what is missing is desperately needed. To be able to actually write something the author actually had to look at other packages to see how to do certain things since the documentation leaves that part out. He notes that two of the most important API methods don't have any documentation; a method for working with files, and anything to do with events. Both of which he says were vital to the packages he wrote. If you can't rely on the official documentation to help you, what can you rely on? Well apparently other people, as long as you know who to talk to or what to look at.

Onto the next topic, MVC, but in atom's case it's only the V. Loren says that you are always working with a view, unless you aren't. At that point you're not really sure what you're working with. There is a strong concept of a view, but no hint of anything to do with a controller. For example to register a view Loren has to call a method called WorkspaceView. There is no associated Workspace object, only the view is available. He ends with a single work that I think is also appropriate. [Wat](http://i0.kym-cdn.com/photos/images/newsfeed/000/173/576/Wat8.jpg?1315930535). There are a few more issues he goes into detail about, all of which deserve the same treatment.

He ends the article by saying that he want to like Atom. He knows it's beta, but can't get over the performance issues. In fact, if he knew he was going to be working with large files he would just fire up Sublime to save himself the hassle. In the end he says he is just going to go back to Sublime until Atom can mature a bit. There are just too many issues to justify switching.

I can't say I blame Loren for what he wrote. You put in all this time to learn Atom, write some significant packages, and even more time banging your head against the wall. I didn't use Atom in March 2014, but if this article is anything to go by I'm glad I didn't. But as of now I couldn't be happier. I suppose Atom has matured in the last 12 months, perhaps to a point that Loren would be willing to give it another shot. Perhaps he already has.

To end this artifact I just want to say that the time I've spent with Atom have been very enjoyable. The performance is up to my standards, as is the customizability and extensibility. I haven't dove into the code too much but from what I can tell the folks at GitHub have really improved the documentation since this article was written. That's it.

<h3>Artifact 2</h3>

Ok, so for the second artifact I wanted to find a bug or enhancement that I could confirm in Atom.

The bug report, which can be found [here](https://github.com/atom/atom/issues/2964) seems easy to replicate, although it doesn't seem much like a bug. What the bug report states is that when opening a folder from the command line, if you already have that folder open a second Atom icon will briefly appear on the dock. Ok, so I open up a folder, and open it up again. This is what I see.

<img src="http://i.imgur.com/maPusgj.png" title="source: imgur.com" />

As you can tell there is a second Atom logo in the dock. It only appears for a fraction of a second, that's why I don't have a decent photo of it, I had to be really quick.

Now that I know I can reproduce it, I checked my version number and went to post on the thread. There was some recent discussion on the topic, but nobody that confirmed it left a version number, so I did. If you want to check out the thread you can find it [here](https://github.com/atom/atom/issues/2964).

<h3>Artifact 3</h3>

For my final artifact I decided to write some actual code. As required for this assignment one of the artifacts must be a modification of the code, so that is sort of what I did. As I was looking through the issues on GitHub I came across someone requesting an [enhancement](https://github.com/atom/atom/issues/6057) that displays the current tab settings in the status bar at the bottom of the window as well as allowing users to change the setting. Currently, to view and change the tab settings you must go into settings and find it listed there. However, in the post on GitHub a contributor mentioned that features like this should not be created through modification of Atom itself, but through a package. So that is what I created. Not so much modifying the Atom code base, but this is the best I could come up with. So with that lets get into it.

On the issue page I mentioned there are a few examples of the requested feature shown, but I chose not to look at them to make sure I didn't copy their code at all. I wanted to see if I could do this on my own.

The first thing I had to do was create a new package. As mentioned in the second artifact of post 1, Atom allows us to easily create a skeleton package. It's created in such a way that allows us to run the code and immediately see this:

<img src="http://i.imgur.com/Mum4syZ.png" title="source: imgur.com" />

My first task was to get that to display in the status bar rather than at the top of the window. After a long time and a lot of Google foo I was able to do it. The code that I had to change was this, that creates an element at the top of the window,

{% highlight coffeescript %}
@modalPanel = atom.workspace.addModalPanel(
    item: @testView.getElement(),
    visible: false
)
{% endhighlight %}

to this, that creates a new status bar element:

{% highlight coffeescript %}
@bottomPanel = atom.workspace.addBottomPanel(
    item: @showIndentView.getElement()
)
{% endhighlight %}

This is what I ended up with at this point. A good start, but now we need to display the actual tab settings.

<img src="http://i.imgur.com/9t9HJzR.png" title="source: imgur.com" />

Looking through the Atom API I found 2 useful functions, [editor.getSoftTabs()](https://atom.io/docs/api/v0.188.0/TextEditor#instance-getSoftTabs) and [editor.getTabLength()](https://atom.io/docs/api/v0.188.0/TextEditor#instance-getTabLength). getSoftTabs returns true if the current settings are soft tabs, and getTabLength returns the size of the tab in spaces. Soft tabs turn into getTabLength number of spaces, and hard tabs turn into a tab character getTabLength is size. So now we can call these functions when we toggle the package to display the current settings. The code that checks the tabs is below, as well as the result.

{% highlight coffeescript %}
updateIndent: ->
  editor = atom.workspace.getActiveTextEditor()
    if (editor)
      softtabs = editor.getSoftTabs()
      length = editor.getTabLength()
      @setText(softtabs, length)

setText: (soft, length) ->
  if (soft)
    text = "Spaces: "
  else
    text = "Tabs: "
  @element.children[0].textContent = text + length
{% endhighlight %}

<img src="http://i.imgur.com/bAiFRO4.png" title="source: imgur.com" />

So at this point lets discuss Atom's tab behavior. Any file that is opened will use the tab settings as they were when it was opened. If you later change the tab settings, it won't effect the settings of open files, only files opened after the change. This means that multiple opened files can all have different tab settings. Therefore, to display the current setting per file I needed an event that fired every time the active file was changed. I found that event, called onDidChangeActivePaneItem. Therefore, any time this event fired, I called the code that checked the tab settings for the current file, and set the text appropriately. It ended up working much better and was much easier than I expected. In the end I had text at the bottom of the pane that accurately displays the windows current tab settings, even when multiple windows have different settings.

I am quite happy with the result. I do however regret that I was unable to get the package to allow changing the settings from the status bar. It was still an enjoyable exercise.

The code can be found on my [GitHub](https://github.com/lhoworko/show-indent).

And with that I am done the second FOSS post. If you made it this far then you must be Cam.
