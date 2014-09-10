---
layout: post
status: publish
published: true
title: Get remote X Windows working in Ubuntu Karmic
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
excerpt: "<a href=\"http:&#47;&#47;flickr.com&#47;photos&#47;40418474@N00&#47;2776450260\"
  title=\"El gegant &#47;&#47; The Giant\"><img src=\"http:&#47;&#47;farm4.static.flickr.com&#47;3082&#47;2776450260_e35cd9a763.jpg\"
  &#47;><&#47;a>\r\n\r\nOne thing that troubled me moving to Ubuntu 9.10 Karmic Koala:
  my remote X applications stopped working with the error\r\n<code>X11 connection
  rejected because of wrong authentication<&#47;code>\r\n\r\n"
wordpress_id: 391
wordpress_url: http://gregorygrubbs.com/?p=391
date: '2009-10-26 12:09:24 -0700'
date_gmt: '2009-10-26 18:09:24 -0700'
categories:
- Development
- emacs
tags: []
comments:
- id: 226
  author: erikr
  author_email: erikriverson@gmail.com
  author_url: ''
  date: '2009-11-10 22:29:40 -0800'
  date_gmt: '2009-11-11 04:29:40 -0800'
  content: "Greg, I have this same problem, too. Is this xauth stuff really the \"official\"
    solution? I unfortunately know nothing about xauth. \r\n\r\nI can ssh to my remote
    box with X forwarding and run \"xeyes\" just fine, and even emacs runs fine.  My
    only problem is when I run emacsclient and try to create a new frame, I get the
    same error as you... I will try your solution! Thank you!\r\n\r\nP.S. Everything
    did work fine until the upgrade to karmic..."
- id: 235
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2009-11-12 09:28:25 -0800'
  date_gmt: '2009-11-12 15:28:25 -0800'
  content: "@erikr, I have logged on to several Linux machines to determine their
    default Xauthority database location, using xauth -v.  On Debian machines, I always
    get ~&#47;.Xauthority.  I get that result even on a server that has been upgraded
    to Karmic, but which does not have Gnome.  On my laptop, however, I get  &#47;var&#47;run&#47;gdm&#47;auth-for-gregj-3sy6gB&#47;database.
    \ That path changes every time I log in, with different salt.  Since everything
    else looks to your home .Xauthority file, this causes your emacsclient session
    to fail to authenticate.  \r\n\r\nI might try messing around with setting the
    XAUTHORITY environment variable, but I'm not sure that would work for Gnome."
- id: 364
  author: Joel J. Adamson
  author_email: adamsonj@email.unc.edu
  author_url: http://www.unc.edu/~adamsonj
  date: '2010-01-21 14:34:16 -0800'
  date_gmt: '2010-01-21 20:34:16 -0800'
  content: "Howdy,\r\n\r\nI've been working on this same problem too.  I submitted
    an Emacs\r\nbug(#5434) and was given this explanation by one of the respondents:\r\n\r\n,----\r\n|
    \r\n| > Okay, I'll try that, but a quick question: should an xauth problem result\r\n|
    > in failures for every X application I try to run?  Other applications\r\n| >
    (other than emacsclient) run just fine.\r\n| \r\n| There is a difference.  When
    you start other clients, you do it from\r\n| the shell started by the ssh login
    process.  When you do emacsclient\r\n| -c it only tells your emacs daemon to open
    a frame on your DISPLAY.\r\n| The emacs daemon is not started from your ssh shell.\r\n|
    \r\n| Try starting another X client from a shell not related to the ssh\r\n| shell
    with the ssh-forwarded display (localhost:10) and see what you\r\n| get.  You
    should get permission denied.  But your Emacs daemon may\r\n| have other displays
    opened, that can influence matters also.\r\n`----\r\n\r\nAll my machines (two
    Fedora 12, one Ubuntu Karmic Koala) have the\r\nnewest gnome, and I confirm the
    same bizarre xauth locations as you\r\ndo.\r\n\r\nI'm at least glad I'm not the
    only one!\r\n\r\nJoel"
- id: 365
  author: Joel J. Adamson
  author_email: adamsonj@email.unc.edu
  author_url: http://www.unc.edu/~adamsonj
  date: '2010-01-21 14:39:22 -0800'
  date_gmt: '2010-01-21 20:39:22 -0800'
  content: It works!
- id: 385
  author: Ben Hyde
  author_email: bhyde@pobox.com
  author_url: http://enthusiasm.cozy.org/
  date: '2010-07-29 11:38:21 -0700'
  date_gmt: '2010-07-29 17:38:21 -0700'
  content: |-
    I am not absolutely certain this is correct, but it has worked for me.

    The problem I wanted to solve was to ssh from my laptop to a ubuntu server and then invoke emacsclient to obtain a x window's frame on my lap top served up from the emacs running on the ubuntu server.  The xauth inside emacs is the one into which I needed to add the xauth credentials.  The following worked, at least once :)

    This script resides on the ubuntu server is run after you ssh to the server, forwarding your
    laptop's X display.

    <pre>
    #!&#47;bin&#47;bash

    # First we need to add to xauth of the server emacs
    # permission to throw up windows on our X server.
    # But .Xauthorization accumlates so we have to auth
    # more than you'd think.
    xauth -f ~&#47;.Xauthority list | grep -v ':0' | while read foo; do
      emacsclient -e "(shell-command \"xauth add $foo\")"
    done

    # Ok, now we should now be able to connect.
    emacsclient -c
    <&#47;pre>

    Thanks for the hint!
---
<p><a href="http:&#47;&#47;flickr.com&#47;photos&#47;40418474@N00&#47;2776450260" title="El gegant &#47;&#47; The Giant"><img src="http:&#47;&#47;farm4.static.flickr.com&#47;3082&#47;2776450260_e35cd9a763.jpg" &#47;><&#47;a></p>
<p>One thing that troubled me moving to Ubuntu 9.10 Karmic Koala: my remote X applications stopped working with the error<br />
<code>X11 connection rejected because of wrong authentication<&#47;code></p>
<p><a id="more"></a><a id="more-391"></a><br />
The reason seems to be that Gnome moved the location of X authorization to [wherever-the-hell-i-dont-remember], whereas ssh and everything else still use the same location (<code>~&#47;.Xauthority<&#47;code>).  Note: I clearly forgot whatever it was I discovered about xauth, so please enlighten me in the comments, and I will update this exceedingly lame paragraph.</p>
<p>This is going to be tagged as an Emacs post because my principal reason to use remote X is Emacs' awesome <code>make-frame-on-display<&#47;code> command.</p>
<p>The bash script I use is saved in ~&#47;bin&#47;xauthmagic:</p>
<pre lang="bash" line="1">
#!&#47;bin&#47;bash<br />
xauth -f ~&#47;.Xauthority list | grep -v ':0' | while read foo; do xauth add $foo; done<br />
<&#47;pre></p>
<p>This means: look through all the xauth cookies in <code>~&#47;.Xauthority<&#47;code>, remove the ':0' (local) display cookie, take the remaining cookies and run the <code>xauth<&#47;code> command on them.</p>
<p>The steps I take to use this:</p>
<ul>
<li>On my remote host (emunah), start an ssh section forwarding X:
<pre lang="bash">
greg@emunah$ ssh greg@maui -Y<br />
<&#47;pre><br />
<&#47;li></p>
<li>
On my local host (maui), run the <code>xauthmagic<&#47;code> script above</p>
<pre lang="bash">
greg@maui$ ~&#47;bin&#47;xauthmagic<br />
<&#47;pre><br />
<&#47;li></p>
<li>
From my local host emacs, run <code>M-x make-frame-on-display RET localhost:10.0 RET<&#47;code><br />
<&#47;li><br />
<&#47;ul></p>
<p>Et voil&aacute;!</p>
