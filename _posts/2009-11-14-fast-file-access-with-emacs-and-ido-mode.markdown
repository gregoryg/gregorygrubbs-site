---
layout: post
status: publish
published: true
title: FAST file access with Emacs and ido-mode
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 411
wordpress_url: http://gregorygrubbs.com/?p=411
date: '2009-11-14 22:44:15 -0800'
date_gmt: '2009-11-15 04:44:15 -0800'
categories:
- Development
- emacs
tags:
- emacs
- Technology&#47;Internet
- Vi
- Ido
- fast access
comments:
- id: 292
  author: adolfo
  author_email: adolfo.benedetti@gmail.com
  author_url: ''
  date: '2009-11-18 18:51:50 -0800'
  date_gmt: '2009-11-19 00:51:50 -0800'
  content: Great post very usefull , could you plz share your .emacs folder?
- id: 363
  author: pt
  author_email: ptpttt@gmail.com
  author_url: ''
  date: '2010-01-06 18:18:57 -0800'
  date_gmt: '2010-01-07 00:18:57 -0800'
  content: Hi, I configured ido-mode as you said, but C-h v and M-x don't invoke ido.
- id: 455
  author: 'Getting started: RoR + SICP | sayem islam &#47; blog'
  author_email: ''
  author_url: http://sayemislam.com/blog/?p=137
  date: '2011-03-15 21:11:22 -0700'
  date_gmt: '2011-03-16 03:11:22 -0700'
  content: "[...] looking forward to using on the next few projects. And in the process,
    I was also introduced to ido-mode in Emacs too &#8211; ido-mode fucking rocks.
    \    Uncategorized   &larr; 2011 training          blog [...]"
---
<p><a href="http:&#47;&#47;flickr.com&#47;photos&#47;10226264@N04&#47;2097587325" title="18 ampolles"><img src="http:&#47;&#47;farm3.static.flickr.com&#47;2254&#47;2097587325_5861cc68ea.jpg" &#47;><&#47;a></p>
<p>One of the things that makes daily Emacs use so enjoyable is the availability of brilliant add-ons designed to make you work faster.  </p>
<p>Emacs with ido-mode fuzzy matching (or flex matching) makes it incredibly quick to navigate the file system using only the keyboard. But it does far more than that, allowing the emacs pilot to quickly find help, commands, variables and much more. This video shows the finer points of using ido-mode with flex matching.</p>
<p>It's all in the video - enjoy.</p>
<p><object width="425" height="344"><param name="movie" value="http:&#47;&#47;www.youtube.com&#47;v&#47;lsgPNVIMkIE&hl=en_US&fs=1&"><&#47;param><param name="allowFullScreen" value="true"><&#47;param><param name="allowscriptaccess" value="always"><&#47;param><embed src="http:&#47;&#47;www.youtube.com&#47;v&#47;lsgPNVIMkIE&hl=en_US&fs=1&" type="application&#47;x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="425" height="344"><&#47;embed><&#47;object></p>
<p>Here are my current settings for ido-mode</p>
<pre lang="lisp">
;; do not confirm a new file or buffer<br />
(setq confirm-nonexistent-file-or-buffer nil)<br />
(require 'ido)<br />
(ido-mode 1)<br />
(ido-everywhere 1)<br />
(setq ido-enable-flex-matching t)<br />
(setq ido-create-new-buffer 'always)<br />
(setq ido-enable-tramp-completion nil)<br />
(setq ido-enable-last-directory-history nil)<br />
(setq ido-confirm-unique-completion nil) ;; wait for RET, even for unique?<br />
(setq ido-show-dot-for-dired t) ;; put . as the first item<br />
(setq ido-use-filename-at-point t) ;; prefer file names near point<br />
<&#47;pre></p>
