---
layout: post
status: publish
published: true
title: 10 Tips for Powerful Emacs on Windows
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
excerpt: "<a title=\"Ladybug Liftoff\" href=\"http:&#47;&#47;flickr.com&#47;photos&#47;23084352@N00&#47;403926829\"><img
  src=\"http:&#47;&#47;farm1.static.flickr.com&#47;163&#47;403926829_cc213ee88b.jpg\"
  alt=\"\" &#47;><&#47;a>\r\n\r\nI avoided using Microsoft Windows for almost 15 years,
  but with my\r\nnew job at a Microsoft-enthralled development shop, those idyllic\r\ndays
  have come to an abrupt end.  Because in the past I could always\r\nuse my trusty
  Linux and OS X machines, I never did push past the\r\nhurdles of using Emacs on
  Windows.  My utter reliance on Org-mode,\r\nTRAMP, and Ediff (to name a few) made
  it essential to get Emacs\r\nworking on Windows if at all possible.\r\n\r\nNow I
  am using Emacs on Windows XP and Windows 7 on a daily basis,\r\nand am quite happy
  with the results.  It was not easy to get to the\r\npoint of full functionality,
  so I wanted to share the magic that\r\nmakes it all work.\r\n"
wordpress_id: 439
wordpress_url: http://gregorygrubbs.com/?p=439
date: '2010-05-23 12:24:14 -0700'
date_gmt: '2010-05-23 18:24:14 -0700'
categories:
- emacs
tags:
- emacs
- Emacs Lisp
- System software
- Microsoft Windows
- Windows XP
- Software download links
comments:
- id: 369
  author: Shawn
  author_email: shawn@topfroggraphics.com
  author_url: http://top-frog.com
  date: '2010-05-23 14:03:13 -0700'
  date_gmt: '2010-05-23 20:03:13 -0700'
  content: You give up on Ubuntu?
- id: 371
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2010-05-23 16:51:03 -0700'
  date_gmt: '2010-05-23 22:51:03 -0700'
  content: |-
    I never gave up on Ubuntu ... I am currently Lucid and will soon be Magnanimous (or whatever).  But I must use MSWindows now on a daily basis.

    We should have lunch soon and catch up eh.
- id: 373
  author: Will
  author_email: will.willis@gmail.com
  author_url: http://silent11.com/
  date: '2010-05-23 22:09:30 -0700'
  date_gmt: '2010-05-24 04:09:30 -0700'
  content: "I too prefer linux&#47;os x as well, but I'm forced to use XP at work
    too.. the 2 apps I have come to love in my Windows work&#47;development environment
    (aside from emacs) are 1) XKeymacs and 2) executor\r\n\r\nhttp:&#47;&#47;www.cam.hi-ho.ne.jp&#47;oishi&#47;indexen.html\r\n\r\nhttp:&#47;&#47;executor.dk&#47;"
- id: 405
  author: Evan
  author_email: eaowens@gmail.com
  author_url: http://blog.arithm.com
  date: '2010-08-17 16:30:58 -0700'
  date_gmt: '2010-08-17 22:30:58 -0700'
  content: "Great tips, but I can't seem to get aspell to work.  Just setting (setq-default
    ispell-program-name \"aspell\") causes emacs to whine thusly:  (file-error \"Searching
    for program\" \"no such file or directory\" \"spell\")\r\n\r\nAny ideas?"
- id: 410
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2010-09-07 19:27:56 -0700'
  date_gmt: '2010-09-08 01:27:56 -0700'
  content: |-
    Evan:  Did you set default-ispell-program-name:
    (setq-default ispell-program-name "aspell")

    If so, is aspell.exe in your path (check by doing M-x shell RET aspell RET)

    Or, if you don't want to put it into the PATH, you can add its directory to exec-path

    Hope this helps!
- id: 422
  author: Drew
  author_email: drew.wells00@gmail.com
  author_url: ''
  date: '2010-10-12 14:12:16 -0700'
  date_gmt: '2010-10-12 20:12:16 -0700'
  content: 'I recently tried to switch to emacs port to windows.  How do you resolve
    the issue with FIND: Parameter format not correct when using grep, rgrep, etc.'
- id: 426
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2010-11-11 11:03:06 -0800'
  date_gmt: '2010-11-11 17:03:06 -0800'
  content: "@Drew: I don't get that error.  The problem is probably that you have
    the Windows system32 directory in your PATH environment prior to the Cygwin path.
    \ So for example, if you have something like \n\nPATH=C:\\WINDOWS\\system32;C:\\cygwin\\bin
    .... \n\nYou will have the problem.  The Windows FIND command is the one giving
    the parameter complaint."
- id: 427
  author: Drew Wells
  author_email: drew.wells00@gmail.com
  author_url: ''
  date: '2010-11-11 11:12:04 -0800'
  date_gmt: '2010-11-11 17:12:04 -0800'
  content: "After much pain and suffering, I decided to go with the GNU WIN32 that
    packages everything together.  I'm a little hesitant to put cygwin commands before
    windows, because other things may be expecting the windows FIND and get they cygwin
    one instead.  I know, I know this is sort of a cop out and now I'm tied to them,
    but it has been working very well (almost as well as emacs on Ubuntu).\r\n\r\nI
    do believe it was a path problem, however when I started hitting cygwin stupid
    things would break like rgrep.  For example, rgrep expects paths like d:&#47;workspace
    and cygwin expects them &#47;cygdrive&#47;d&#47;workspace.  I believe there is
    a fix for this too, in the end I gave up and uses windows compiled versions of
    the binaries that came with GNU WIN32.\r\n\r\nThanks for the tips they were helpful!"
- id: 429
  author: Kyle Sexton
  author_email: ks@mocker.org
  author_url: http://www.mocker.org
  date: '2010-12-08 09:06:21 -0800'
  date_gmt: '2010-12-08 15:06:21 -0800'
  content: Thanks for all of these tips!
- id: 430
  author: ignacio
  author_email: ignacio.pazposse@gmail.com
  author_url: http://ignaciopp.wordpress.com/
  date: '2010-12-08 13:45:01 -0800'
  date_gmt: '2010-12-08 19:45:01 -0800'
  content: "hi Greggory, \r\nI got really excited about your use of tramp in windows
    (avoiding the emacs cygwin compilation), but unfortunately got no luck with your
    approach. I'd really love being able to reach the point of working remotely on
    files tunneled by ssh.  with my regular window emacs version (i'm currently using
    23.1.91.1) .\r\nCould you please elaborate a little more  on what you do to ssh
    a file after having set your tramp configs into the .emacs file?\r\n I don't quite
    understand what you mean exactly with \"Try M-x shell, then visit a TRAMP site
    such as &#47;user@site: and try M-x shell from there!\"\r\nDon't you open it doing
    C-x C-f? Sorry but I might be missing something pretty obvious here.  Thank you
    in advance for this!\r\nIgnacio"
- id: 485
  author: J Donald
  author_email: jeddak@verizon.net
  author_url: http://www.JonathanDonald.com
  date: '2011-05-05 07:22:00 -0700'
  date_gmt: '2011-05-05 13:22:00 -0700'
  content: "Great post! Lots of useful info. I was especially glad to see the tip
    for printing from Emacs on Windows. I've tried various workarounds before, with
    varying degrees of success&#47;usefulness.\r\n\r\nA tip for those who are trying
    to use gsprint with Emacs on Windows 7: you will need to force gsprint to use
    the 64-bit version of gsview; by default, it tries to launch the 32-bit version.\r\n\r\nTo
    see if you're experiencing the same issue, try running gsprint from a CMD prompt.
    If you see the message \"Failed to exec program c:\\{path\\to}\\gswin32.exe\",
    read on.\r\n\r\nOn my machine, I created a configuration file called gsprint.cfg
    containing the following two lines:\r\n\r\n-ghostscript \r\n\"C:\\Applications\\gs\\gs9.02\\bin\\gswin64c.exe\"\r\n\r\nThis
    is placed in the same directory as gsprint.exe.\r\n\r\nSee documentation at http:&#47;&#47;pages.cs.wisc.edu&#47;~ghost&#47;gsview&#47;gsprint.htm
    for more details."
- id: 503
  author: angel
  author_email: angel21ccs@hotmail.com
  author_url: ''
  date: '2011-06-30 22:09:47 -0700'
  date_gmt: '2011-07-01 04:09:47 -0700'
  content: Hi..I've a question..I've installed emacs23 on native windows, and I've
    cygwin and I want use w3m, is necessary install the cygwin emacs version or I
    can use w3m outside cygwin too??..thanks for the article
- id: 604
  author: dqj
  author_email: dqj@authentrics.com
  author_url: ''
  date: '2011-12-27 10:18:27 -0800'
  date_gmt: '2011-12-27 16:18:27 -0800'
  content: Thank you!  My situation is almost identical.  The last time I worked with
    Windoze was on 3.1 app development.  Emacs is unbeatable for some tasks, and I
    am really missing it every day.
- id: 626
  author: The Cathedral and the Bazaar, GNU, Emacs, Cygwin Links &laquo; armanketujuh
  author_email: ''
  author_url: http://armanketujuh.wordpress.com/2012/07/05/the-cathedral-and-the-bazaar-gnu-emacs-cygwin-links/
  date: '2012-07-04 22:50:30 -0700'
  date_gmt: '2012-07-05 04:50:30 -0700'
  content: "[...] 10 Tips for Powerful Emacs on Windows&nbsp;http:&#47;&#47;gregorygrubbs.com&#47;emacs&#47;10-tips-emacs-windows&#47;
    [...]"
- id: 629
  author: Sebastian
  author_email: stammler.s@gmail.com
  author_url: ''
  date: '2012-07-12 19:00:48 -0700'
  date_gmt: '2012-07-13 01:00:48 -0700'
  content: "great tips!\r\nfor the new version 24 of emacs you need newer win32 libs
    for png image previews than the ones gnuwin32. you can get sufficiently new ones
    at http:&#47;&#47;www.gtk.org&#47;download&#47;win32.php\r\nplease change the
    links given in the introduction.\r\n\r\ncheers!"
- id: 630
  author: Sebastian
  author_email: stammler.s@gmail.com
  author_url: ''
  date: '2012-07-12 20:02:04 -0700'
  date_gmt: '2012-07-13 02:02:04 -0700'
  content: "I just solved another issue with previews, now it is finally working for
    me. The current auctex release 11.86 did not work for me together with gs 9.05,
    it crashed with the message\r\n\r\nError: &#47;typecheck in --setfileposition--\r\n\r\nIt
    is an issue in preview.el which is fixed in the cvs tree.\r\nI downloaded the
    file preview.el manually from cvs and placed it in the appropriate directory in
    the emacs folder, download HEAD (at the moment 1.286) from http:&#47;&#47;cvs.savannah.gnu.org&#47;viewvc&#47;auctex&#47;preview&#47;preview.el?root=auctex&amp;view=log\r\ndon't
    forget to delete the old .elc file\r\n\r\n@J Donald, I found out another way of
    telling auctex to use the 64 bit version of gs, just modify the preview-gs-command
    variable appropriately"
- id: 2771
  author: Zenadix
  author_email: maguayo2@gmail.com
  author_url: ''
  date: '2014-06-05 08:29:26 -0700'
  date_gmt: '2014-06-05 14:29:26 -0700'
  content: "I wanted to add some observations on your comparison of native Windows
    Emacs and  Cygwin Emacs:\r\n\r\n- You can get a \"pretty\" emacs even inside the
    Cygwin terminal, without the need to run Cygwin-X. You just have to enable the
    256-color terminal.\r\n- Window Opacity Control does work in Cygwin Emacs if you
    run it inside the terminal. Right click on any part of the terminal-> Options
    -> Transparency.\r\n- Cygwin mirrors always offer the latest version from gnu.org.
    \ For instance, current Emacs version is 24.3 both in gnu.org and in Cygwin.\r\n-
    You say that native Emacs runs faster than the Cygwin version. Can you elaborate
    on that? I've found that the Cygwin Terminal Emacs does some stuff actually faster
    than the native version. For example, running find-file with ido-mode in a very
    large directory makes native Emacs hang for several seconds, but it's much faster
    on Cygwin, presumably because it uses the very efficient Unix 'find' command.
    Try it yourself!\r\n\r\nTherefore, I think there no is base to say that native
    Windows Emacs is better than Cygwin Emacs. It is well known that term, ansi-term
    and multi-term do not work in native Emacs, but they do work inside Cygwin. Besides,
    Cygwin Emacs supports fullscreen mode out of the box, which is really great. Of
    course, Cygwin Emacs has some slight deficiencies: there is no mouse support (but
    isn't the whole point of using Emacs to break free from the mouse?), and proced
    doesn't work out of the box. Still, I really feel that Cygwin Emacs has more to
    offer than the native Windows port."
- id: 2841
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2014-06-23 09:17:41 -0700'
  date_gmt: '2014-06-23 15:17:41 -0700'
  content: "@Zenadix, I really appreciate your comments.  I will give the cygwin version
    another look!"
---
<p><a title="Ladybug Liftoff" href="http:&#47;&#47;flickr.com&#47;photos&#47;23084352@N00&#47;403926829"><img src="http:&#47;&#47;farm1.static.flickr.com&#47;163&#47;403926829_cc213ee88b.jpg" alt="" &#47;><&#47;a></p>
<p>I avoided using Microsoft Windows for almost 15 years, but with my<br />
new job at a Microsoft-enthralled development shop, those idyllic<br />
days have come to an abrupt end.  Because in the past I could always<br />
use my trusty Linux and OS X machines, I never did push past the<br />
hurdles of using Emacs on Windows.  My utter reliance on Org-mode,<br />
TRAMP, and Ediff (to name a few) made it essential to get Emacs<br />
working on Windows if at all possible.</p>
<p>Now I am using Emacs on Windows XP and Windows 7 on a daily basis,<br />
and am quite happy with the results.  It was not easy to get to the<br />
point of full functionality, so I wanted to share the magic that<br />
makes it all work.<br />
<a id="more"></a><a id="more-439"></a></p>
<p>I have decided against using the Cygwin Emacs package for several reasons:</p>
<ul>
<li>Running a windowed&#47;multi-frame&#47;pretty version requires running<br />
Cygwin-X, which is quite a lot of overhead just to run Emacs. I<br />
have had a few interface and display problems lately with Cygwin-X<br />
also.<&#47;li></p>
<li>Cool-though-seldom-used features that work in the native port do<br />
not work in the Cygwin port: Window opacity control, for example<&#47;li></p>
<li>Using the native port means I can always be running the latest<br />
released version from gnu.org<&#47;li></p>
<li>The native port just runs faster<&#47;li><br />
<&#47;ul><br />
On the other hand, Cygwin does play a crucial role in making the<br />
native Emacs port work properly.  I have tried and hated using PuTTY<br />
and Plink, and various one-off ports of standard Unix commands.<br />
Using Cygwin and its package management makes all this<br />
much simpler and more reliable.</p>
<p>So all the hints given here use the "official" Emacs for Windows<br />
(sometimes referred to as NTEmacs), as well as Cygwin (with no<br />
dependency on Cygwin-X).</p>
<p>I really hope this helps some poor beleaguered Linux&#47;OS X Emacs user<br />
make the giant backwards leap. With these tips and little helpers like<br />
<a href="http:&#47;&#47;www.launchy.net&#47;">Launchy<&#47;a>, you won't even have to<br />
acknowledge that you're running Windows!</p>
<h2>Software download links<&#47;h2><br />
Here's where you will find all the software referenced in the tips:</p>
<ul>
<li><a href="http:&#47;&#47;ftp.gnu.org&#47;pub&#47;gnu&#47;emacs&#47;windows&#47;">Emacs for Windows<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;www.cygwin.com&#47;">Cygwin<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;gnuwin32.sourceforge.net&#47;">GnuWin32<&#47;a> for image libraries<&#47;li>
<li><a href="ftp:&#47;&#47;ftp.franken.de&#47;pub&#47;win32&#47;develop&#47;gnuwin32&#47;cygwin&#47;porters&#47;Humblet_Pierre_A&#47;V1.1&#47;ispell-3.2.06-cygwin-1.3-bin.tar.gz">ISpell package<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;files.emacsblog.org&#47;ryan&#47;elisp&#47;maxframe.el">Maxframe.el<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;mirror.cs.wisc.edu&#47;pub&#47;mirrors&#47;ghost&#47;ghostgum&#47;gsv49w32.exe">GSView<&#47;a><&#47;li><br />
<&#47;ul></p>
<h2>Tip #1: General Usage<&#47;h2></p>
<ul>
<li>Execute runemacs.exe or emacsclientw.exe.  On your Linux and OS X<br />
systems, the binary names or emacs and emacsclient: just use the<br />
windows-specific wrappers included in the standard port when on MS Windows.<&#47;li></p>
<li>Add Cygwin &#47;bin to exec-path.
<pre lang="Lisp">      (if (file-directory-p "c:&#47;cygwin&#47;bin")<br />
      (add-to-list 'exec-path "c:&#47;cygwin&#47;bin"))<&#47;pre><br />
<&#47;li><br />
<&#47;ul></p>
<h2>Tip #2: Make TRAMP work nicely -- and without PuTTY<&#47;h2><br />
There are people using PuTTY and Plink.exe to get this working, but<br />
I like using good old OpenSSH much better: no translation required<br />
for the keys I use, and I have it installed anyway in Cygwin.</p>
<ul>
<li>Install Cygwin, including the OpenSSH package<&#47;li>
<li>In your Emacs init, set shell to bash
<pre lang="Lisp">      (setq shell-file-name "bash")<br />
      (setq explicit-shell-file-name shell-file-name)<&#47;pre><br />
<&#47;li></p>
<li>In Emacs init, set tramp-default-method to "sshx" or "scpx"
<pre lang="Lisp">      (cond  ((eq window-system 'w32)<br />
      (setq tramp-default-method "scpx"))<br />
      (t<br />
      (setq tramp-default-method "scpc")))<&#47;pre><br />
<&#47;li></p>
<li>Windows 7 note: &nbsp; I was unable to get this to work on Win7 until I set the runemacs.exe binary to run in Windows XP (Service Pack 3) compatibility mode.<&#47;li>
<li>Test: Try <code>M-x shell<&#47;code>, then visit a TRAMP site such as <code>&#47;user@site:<&#47;code> and try <code>M-x shell<&#47;code> from there!<&#47;li><br />
<&#47;ul></p>
<h2>Tip #3: Use SVN and GIT without tears<&#47;h2><br />
Version control should work out of the box -- but SSH problems can<br />
interfere sometimes.  So once you get TRAMP working properly, you<br />
should have no problems with VC.</p>
<ul>
<li>Install subversion and git from Cygwin<&#47;li>
<li>Use built-in vc-dir, or psvn.el and magit.el<&#47;li><br />
<&#47;ul></p>
<h2>Tip #4: Display images in buffers, including doc-view<&#47;h2><br />
You may have noticed that your Windows Emacs has no ability to<br />
display images.  This is simply due to the fact that the port is<br />
not distributed with the libraries necessary to display them.</p>
<p>The solution is to visit the GnuWin32 link above, download the<br />
packages relevant to the types of images you want to display<br />
(including zlib1 for compressed images), and copy the DLLs into the<br />
bin directory of your Emacs installation (e.g, C:\Program<br />
Files\emacs23-2\bin).</p>
<p>Images will only be displayed after restarting Emacs.</p>
<p>Here's a list of DLLs that I now have in my installation:</p>
<ul>
<li>jpeg62.dll<&#47;li>
<li>libXpm.dll<&#47;li>
<li>libjpeg-62.dll<&#47;li>
<li>libpng-bcc.lib<&#47;li>
<li>libpng.dll.a<&#47;li>
<li>libpng.la<&#47;li>
<li>libpng.lib<&#47;li>
<li>libpng12-0.dll<&#47;li>
<li>libpng12.def<&#47;li>
<li>libpng12.dll<&#47;li>
<li>libpng12.dll.a<&#47;li>
<li>libpng12.la<&#47;li>
<li>libtiff3.dll<&#47;li>
<li>zlib1.dll (for compression, not images)<&#47;li><br />
<&#47;ul></p>
<h2>Tip #5: Use W3M<&#47;h2><br />
The W3M web browser works fine once you install the w3m binary --<br />
and once the image display step above is working, you will be able<br />
to display images in the W3M buffers as well.</p>
<ul>
<li>Install w3m from Cygwin<&#47;li>
<li>Test image display by hitting <code>T<&#47;code> (w3m-toggle-inline-images)<&#47;li>
<li>Example screenshot:<br />
<a rel="attachment wp-att-450" href="http:&#47;&#47;gregorygrubbs.com&#47;emacs&#47;10-tips-emacs-windows&#47;attachment&#47;emacs_pacman_google&#47;"><img class="alignnone size-medium wp-image-450" title="W3M Browser in Emacs" src="http:&#47;&#47;gregorygrubbs.com&#47;wp-content&#47;uploads&#47;2010&#47;05&#47;emacs_pacman_google-300x127.jpg" alt="W3M Browser in Emacs" width="300" height="127" &#47;><&#47;a><&#47;li><br />
<&#47;ul></p>
<h2>Tip #6: Bring back Ediff and Smerge<&#47;h2><br />
Ediff is yet another thing which doesn't work as it should.  You<br />
will get an error complaining about Dos-style versus Unix-style<br />
paths.  Fixing it is a simple matter of setting an environment variable.</p>
<ul>
<li>Assure you have Cygwin's diff package installed<&#47;li>
<li>Set the Windows environment variable nodosfilewarning=1<&#47;li>
<li>Restart Emacs, and verify that the environment variable is set by executing <code>M-x shell<&#47;code>, then typing <code>env | grep dos<&#47;code>, for example<&#47;li>
<li><strong>Always, prior to running ediff<&#47;strong>, execute <code>M-x shell<&#47;code><&#47;li><br />
<&#47;ul></p>
<h2>Tip #7: Spell using ISpell or Aspell<&#47;h2><br />
Fortunately very easy to get working by following <a href="http:&#47;&#47;bria.nwood.org&#47;node&#47;49">Brian Wood's directions<&#47;a> using the ISpell package for Cygwin linked above.</p>
<p><strong>Note added later:<&#47;strong></p>
<p>Aspell is even easier to use: just install aspell and the correct language(s) in Cygwin, then use the following in your emacs init:</p>
<pre lang="Lisp">(setq-default ispell-program-name "aspell")<&#47;pre></p>
<h2>Tip #8: Maximized frame works using maxframe.el<&#47;h2><br />
Those of us who practice Distraction-Free Emacsing, or DFE, will<br />
lament the inability to maximize the frame as we can do on other<br />
systems (ie, a true maximized windows, with no OS window<br />
decoration).  The solution is provided by maxfame.el, linked above.</p>
<p>After loading maxframe.el, use <code>M-x maximize-frame<&#47;code> and <code>M-x restore-frame<&#47;code></p>
<h2>Tip #9: Print on PostScript printers<&#47;h2><br />
And finally, printing.  Even this just didn't work out of the box<br />
for me.  The solution was to use a nice little utility called<br />
GSPrint from the GSView package linked above.</p>
<ul>
<li>Install Ghostscript in Cygwin<&#47;li>
<li>Install GSView
<pre lang="Lisp">      (when (and (string= (window-system) "w32") (file-exists-p "c:&#47;Program Files&#47;Ghostgum&#47;gsview&#47;gsprint.exe"))<br />
      (progn<br />
      ;;  Windows printer<br />
      (setq-default ps-lpr-command (expand-file-name "c:&#47;Program Files&#47;Ghostgum&#47;gsview&#47;gsprint.exe"))<br />
      (setq-default ps-printer-name t)<br />
      (setq-default ps-printer-name-option nil)<br />
      (setq ps-lpr-switches '("-query")) ; show printer dialog<br />
      (setq ps-right-header '("&#47;pagenumberstring load" ps-time-stamp-mon-dd-yyyy))))<br />
      (if (eq window-system 'x)<br />
      (setq ps-lpr-command "gtklp"))<&#47;pre><br />
<&#47;li><br />
<&#47;ul></p>
<h2>Tip #10: Some things Just Work&trade;: Nifty Emacs 23 features that work "out of the box"<&#47;h2><br />
Bonus tip &mdash; some things work already, no fiddling required!</p>
<h3>Select any font you want<&#47;h3></p>
<ul>
<li>M-x menu-set-font (choose something lovely like Consolas or Inconsolata ... or Comic Sans MS)<&#47;li>
<li>Example font selection, cross-OS
<pre lang="Lisp">      ;;* Font selection<br />
      (cond ((or (eq window-system 'mac) (eq window-system 'ns))<br />
      (set-face-font 'default '"-apple-inconsolata-medium-r-normal--16-0-72-72-m-0-iso10646-1"))<br />
      ((eq window-system 'w32)<br />
      (set-face-font 'default '"-outline-Inconsolata-normal-normal-normal-mono-16-*-*-*-c-*-iso8859-1"))<br />
      ((and (eq window-system 'x) (eq emacs-major-version 23))<br />
      (set-face-font 'default '"-unknown-Inconsolata-normal-normal-normal-*-16-*-*-*-m-0-iso10646-1")<br />
      (add-to-list 'default-frame-alist '(font . "-unknown-Inconsolata-normal-normal-normal-*-16-*-*-*-m-0-iso10646-1"))<br />
      )<br />
      ((eq window-system 'x)<br />
      (set-face-font 'default '"10x20")))</p>
<p>      (add-hook 'before-make-frame-hook<br />
      (lambda ()<br />
      (set-frame-font "-unknown-Inconsolata-normal-normal-normal-*-16-*-*-*-m-0-iso10646-1")<br />
      ))<&#47;pre><br />
<&#47;li></p>
<li><code>M-x grep<&#47;code>, <code>M-x grep-find<&#47;code>, <code>M-x rgrep<&#47;code> and friends (as long as<br />
you have the <code>grep<&#47;code> and <code>find<&#47;code> commands installed!)<&#47;li></p>
<li><code>M-x tetris<&#47;code>, <code>M-x doctor<&#47;code>, <code>M-x yow<&#47;code>, <code>M-x butterfly<&#47;code><&#47;li><br />
<&#47;ul></p>
<h3>Frame transparency<&#47;h3></p>
<ul>
<li>Transparent windows are not my favorite thing, as they tend to<br />
hamper DFE (see above).  But there are occasions, like copying text from a<br />
web page into an Emacs buffer, where it can come in quite handy.</p>
<pre lang="Lisp">      (defun set-transparency (alpha-level)<br />
      (interactive "p")<br />
      (message (format "Alpha level passed in: %s" alpha-level))<br />
      (let ((alpha-level (if (< alpha-level 2)<br />
				(read-number "Opacity percentage: " 85)<br />
				alpha-level))<br />
				(myalpha (frame-parameter nil 'alpha)))<br />
				(set-frame-parameter nil 'alpha alpha-level))<br />
				(message (format "Alpha level is %d" (frame-parameter nil 'alpha))))<&#47;pre><br />
<&#47;li><br />
<&#47;ul></p>
