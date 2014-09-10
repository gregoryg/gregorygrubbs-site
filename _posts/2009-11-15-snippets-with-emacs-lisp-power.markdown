---
layout: post
status: publish
published: true
title: Snippets with Emacs Lisp Power
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 415
wordpress_url: http://gregorygrubbs.com/?p=415
date: '2009-11-15 00:00:51 -0800'
date_gmt: '2009-11-15 06:00:51 -0800'
categories:
- Development
- wordpress
- emacs
tags:
- wordpress
- php
- emacs
- TextMate
- Functional languages
- E Text Editor
- Snippet
- Mac OS X
- Lisp
- Emacs Lisp
- yasnippet
- Development
comments:
- id: 361
  author: joao
  author_email: joaotavora@gmail.com
  author_url: http://yasnippet.googlecode.com
  date: '2009-12-22 16:49:00 -0800'
  date_gmt: '2009-12-22 22:49:00 -0800'
  content: "Hi,\r\n\r\nNice to see someone using more yasnippet power! You might want
    to turn your snippet using gjg&#47;move-next-sexp-past-current-scope into a snippet-command,
    something that is available in the yasnippet trunk, and will be released in the
    upcoming 0.7.\r\n\r\nHave a look at this snippet\r\n\r\n# -*- mode: snippet -*-\r\n#
    type: command\r\n# key: marcc\r\n# contributor: Translated from TextMate Snippet\r\n#
    name: Add &#47; Remove Several Columns (marcc)\r\n# condition: (yas&#47;rails-intelligent-migration-snippet-condition-p)\r\n#
    --\r\n(yas&#47;rails-intelligent-migration-snippet :add_remove_column_continue)\r\n\r\nwith
    the supporting code available at\r\n\r\nhttp:&#47;&#47;yasnippet.googlecode.com&#47;svn&#47;trunk&#47;extras&#47;imported&#47;rails-mode&#47;.yas-setup.el\r\n\r\nor
    mail me for suggestions. I'm happy to give you support, with what I can, and I
    encourage you to create more complex snippets or contribute to the textmate-snippet-conversion
    effort. \r\n\r\nbye"
---
<p><a href="http:&#47;&#47;flickr.com&#47;photos&#47;26405526@N00&#47;2188203168" title="As RAW as Winter"><img src="http:&#47;&#47;farm3.static.flickr.com&#47;2165&#47;2188203168_86a4d818f4.jpg" &#47;><&#47;a> </p>
<p>The YASnippet package for Emacs has some pretty awesome power for the developer, especially when you utilize the power of Emacs Lisp.  </p>
<p><object width="425" height="344"><param name="movie" value="http:&#47;&#47;www.youtube.com&#47;v&#47;HPT7pm8ot8M&hl=en_US&fs=1&"><&#47;param><param name="allowFullScreen" value="true"><&#47;param><param name="allowscriptaccess" value="always"><&#47;param><embed src="http:&#47;&#47;www.youtube.com&#47;v&#47;HPT7pm8ot8M&hl=en_US&fs=1&" type="application&#47;x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="425" height="344"><&#47;embed><&#47;object></p>
<p>YASnippet was inspired by TextMate, which was inspired by Emacs, in a highly-out-of-equilibrium whirlwind of self-referential creativity.  </p>
<p>The screencast above uses a set of snippets I originally took from <a href="http:&#47;&#47;top-frog.com&#47;projects&#47;wordpress-textmate-bundle&#47;">this WordPress TextMate bundle<&#47;a>, created by Shawn Parker and Gordon Brander</p>
<p>The first snippet in the screencast illustrates YASnippet's mirrors with transformation, in a WordPress plugin template.  The snippet calls Emacs Lisp functions as the plugin name is filled in to create the plugin URI, the "namespace" (used here as a prefix for function and variable names), and the primary class name for the plugin. </p>
<p>The second snippet writes a function skeleton, then calls Emacs Lisp at the end to move the generated function outside the current scope into a correct position in the file.  This snippet uses YASnippet's fields with transformations syntax, but to do a sneaky thing: not transform the field, but move a region of generated text!</p>
<p>Following is the code for the snippets shown in the screencast, with no commentary.  So pipe up in the comments if you're curious about how something works!</p>
<pre lang="PHP">
# -*- mode: snippet -*-<br />
# name: WP Plugin<br />
# key: plugin<br />
# --<br />
&#47;*<br />
Plugin Name: ${1:Plugin Name}<br />
Plugin URI: http:&#47;&#47;${2:dynapse.com&#47;plugins&#47;}${1:$(gjg&#47;sanitize text)}&#47;<br />
Description: ${3:Description}<br />
Version: ${4:1.0}<br />
Author: ${5:Gregory Grubbs}<br />
Author URI: http:&#47;&#47;${6:gregorygrubbs.com&#47;}<br />
Namespace: ${1:$(gjg&#47;acronyminize text)}_<br />
*&#47;</p>
<p>class ${1:$(gjg&#47;whitespace-to-underscore text)} {<br />
	&#47;**<br />
	 * constructor for $1<br />
	 *<br />
	 * The constructor is responsible for registering all hooks used<br />
	 * by this class as as WordPress plugin<br />
	 *&#47;<br />
	function __construct() {<br />
		 $0<br />
	} &#47;&#47; constructor</p>
<p>}<br />
$${1:$(gjg&#47;acronyminize text)} = new ${1:$(gjg&#47;whitespace-to-underscore text)}();<br />
<&#47;pre></p>
<p>Next, the add_action snippet, which moves a generated function at the end:</p>
<pre lang="PHP">
# -*- mode: snippet -*-<br />
# name: add_action<br />
# key: add_action<br />
# --<br />
add_action('${1:init}', array($this, 'my_${2:$1}'));<br />
${3:$$(gjg&#47;move-next-sexp-past-current-scope)}<br />
function my_$1 () {<br />
}<br />
<&#47;pre></p>
<p>And finally, (some of) the Emacs Lisp functions that the snippets call:</p>
<pre lang="Lisp">
(defun gjg&#47;acronyminize (text &optional do-capitalize)<br />
  "Make an acronym from the text<br />
do-capitalize: t means run text through capitalize function, nil will respect CamelCase<br />
"<br />
  (save-excursion<br />
    (setq case-fold-search nil)<br />
    (downcase<br />
     (replace-regexp-in-string<br />
      "[^A-Z]" ""<br />
      (if do-capitalize (capitalize text) text) nil t))))<br />
(defun gjg&#47;move-next-sexp-past-current-scope ()<br />
  "kill sexp following point, move past current scope&#47;sexp&#47;function"<br />
  (beginning-of-line)<br />
  (let ((beg (point)))<br />
    (re-search-forward "^[ \t]*function[ \t]+[^}]+?}" (point-max) nil)<br />
    (mark-defun)<br />
	(kill-region (point) (mark)))<br />
  (forward-line)<br />
  (yank)<br />
  (indent-region (mark) (point)))<br />
<&#47;pre></p>
