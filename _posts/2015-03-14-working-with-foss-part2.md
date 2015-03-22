---
layout: post
title: Working With FOSS, Part 2
---

To continue on from my last post I will go over three more artifacts related to Atom.

<!--excerpt-->

<h3>Artifact 1</h3>

To begin this post off I wanted to review an article I found online that compare Atom to other popular text editors, mainly Sublime. A few months ago I began using Atom after trying a bunch of others, none of which I really enjoyed using. I thought it appropriate to discuss my reasons, as well as well as others, for why I like Atom.

The article was written by Loren Segal and is called [My Week With GitHub's Atom](http://gnuu.org/2014/03/10/my-week-with-githubs-atom-editor/). This article was writen just over a year ago so some things have definitely changed but the issues then are still worth talking about.

So the first thing Loren does is mention that Atom is similar to Sublime in almost all ways. This is not the first time I've come across this statement. In fact, it seems that Sublime hit it so far out of the park with Sublime Text 2 that everyone and their dog is making their editor behave the same. Not only with functionality but also colours and layout. I'm not saying I mind, it's just that Sublime Text 2 must have been something very new and exciting at the time to make it the de facto standard for comparing editors.

An exciting feature about Atom is that it is built for web developers using the technologies that web developers know. JavaScript (CoffeeScript), HTML, & CSS are what Atom are built on, making it extremely easy to develope modules and even drastically change the layout and colour scheme. One thing I really look for in an editor is being able to customize it to my liking, and with Atom I can easily change the keyboard shortcuts and menu layout to my liking. As for the author, he acknowledges that using HTML is a desktop application is questionable, but in this case it definitely works.

I haven't yet got too deep into the Git aspects of Atom, but the author notes that considering Atom is built by GitHub there isn't a whole lot of Git functionality built in. There is the ability to diff and see what branch you're on but why no built in commit option? As for Loren, he says that it should be there, hopefully in the future.

The next thing mentioned is Atom's performance issues. Perhaps this is one of the things improved since March 2014, but I don't notice what the author states. He notes slow start up (which does happen sometimes) to visible lag while typing (which I've never noticed). He is quite worried about the long term performance of Atom, stating that as the editor grows it will only get worse, something that the guys at GitHub must have already solved.

The author continues his critical stance on Atom with his discussion of the API. My only experience with the API was in my previous post where I followed the tutorial to created a simple plug in. I quite enjoyed that but obviously that just scratched the surface of what is available. Loren states that everything seems to be half done, "as if they decided they were going to write a text editor app half way through implementing the text editor component". Ok, lets see what he means by this.

Documentation. Or actually the lack of it. What is there is wrong or misleading, and what is missing is desperately needed. To be able to actually write something, the author actually had to look at other plug ins to see how to do certain things since the documentation leaves that part out. He notes that two of the most important API methods don't have any documentation; a method for working with files, and anything to do with events. Both of which he says were vital to plug ins he wrote. If you can't rely on the official documentation to help you, what can you rely on? Well apparently other people, as long as you know who to talk to.

Onto the next topic, MVC, but in atom's case it's only the V. Loren says that you are always working with a view, unless you aren't. At that point you're not really sure what you're working with. There is a strong concept of a view, but no hint of anything to do with a controller. For example to register a view Loren has to call a method called WorkspaceView. There is no associated Workspace object, only the view is available. He ends with a single work that I think is also appropriate. [Wat](http://i0.kym-cdn.com/photos/images/newsfeed/000/173/576/Wat8.jpg?1315930535). There are a few more issues he goes into detail about, all of which deserve the same treatment.

He ends the article by saying that he want to like Atom. He knows it's beta, but can't get over the performance issues. In fact, if he knew he was going to be working with large files he would just fire up Subime to save himself the hassle. In the end he says he is just going to go back to Sublime until Atom can mature a bit. There are just too many issues to justify switching.

I can't say I blame Loren for what he wrote. You put in all this time to learn Atom, write some significant plug ins, and even even more time banging your head against the wall. I didn't use Atom in March 2014, but if this article is anything to go by I'm glad I didn't. But as of now I couldn't be happier. I suppose Atom has matured in the last 12 months, perhaps to a point that Loren would be willing to give it another shot. Perhaps he already has.

To end this artifact I just want to say that the time I've spent with Atom have been very enjoyable. The performance is up to my standards, as is the customizability and extensability. I haven't dove into the code too much but from what I can tell the folks at GitHub have really improved the documentation since this article was written. That's it.

<h3>Artifact 2</h3>

Ok, so for the second artifact I wanted to find a bug or enhancement that I could work on in Atom. I browsed the issues section on GitHub and came across a lot of enhancements that seemed doable. The main one was an indicator in the lower corner of the window that would specify the current indentation level. For example, whether it's set for two spaces, 4 spaces, tabs, etc. One of the maintainers of Atom commented on the thread and mentioned that it would be well suited as a package rather than in the Atom source. I thought I could do it, but when I started to look around I saw that the problem had already been solved multiple times so there was not much point in doing it again. At this point I've  done 3 artifacts and am beginning to run out of ideas for the last two. I know one has to be a contribution to the code base but at this point I don't know if that's going to be possible. Probably should have chosen a smaller project with more bugs and fewer contributors. Oh well. After being unable to find anything to work on I decided to look through some of the other bug reports and see if I could confirm any of them. So that's what I did for this artifact.

The bug report, which can be found [here](https://github.com/atom/atom/issues/2964) seems easy to replicate, although it doesn't seem much like a bug. What the bug report states is that when opening a folder from the command line, if you already have that folder open a second Atom icon will briefly appear on the dock. Ok, so I open up a folder, and open it up again. This is what I see.

<a href="http://imgur.com/maPusgj"><img src="http://i.imgur.com/maPusgj.png" title="source: imgur.com" /></a>

As you can tell there is a second Atom logo in the dock. It only appears for a fraction of a second, that's why I don't have a decent photo of it, I had to be really quick.

Now that I know I can reporduce it, I checked my version number and went to post on the thread. There was some recent discussion on the topic, but nobody that confirmed it left a version number, so I did. If you want to check out the thread you can find it [here](https://github.com/atom/atom/issues/2964). Thanks.
