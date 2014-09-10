---
layout: post
status: publish
published: true
title: 'Emacs Power: remote servers and shell commands'
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
excerpt: "<a href=\"http:&#47;&#47;flickr.com&#47;photos&#47;16230215@N08&#47;2898797929\"
  title=\"Come Together\"><img src=\"http:&#47;&#47;farm4.static.flickr.com&#47;3282&#47;2898797929_f209eeb4a4.jpg\"
  &#47;><&#47;a>\r\n<h4 id=\"sec-1\">Emacs file and directory browsing <&#47;h4>\r\n\r\nEmacs
  has Dired, a great method for browsing directories; especially in combination with
  ido-mode, I prefer it to Windows Explorer, OS X Finder, Gnome Nautilus, or anything
  else I've used over the decades to browse file systems. You can quickly begin entering
  paths, and Dired helps you with directory and file name completion.\r\n"
wordpress_id: 372
wordpress_url: http://gregorygrubbs.com/?p=372
date: '2009-10-02 11:26:40 -0700'
date_gmt: '2009-10-02 17:26:40 -0700'
categories:
- Development
- wordpress
- emacs
tags:
- wordpress
- secure shell
- remote server
- emacs
- tramp
- geekhood
- power
comments:
- id: 145
  author: 29 most trending topics in webdesign, tech and seo. Illustrator tutorials!
    &laquo; Adrian Zyzik&#8217;s Weblog
  author_email: ''
  author_url: http://zyzik.wordpress.com/2009/10/05/29-most-trending-topics-in-webdesign-tech-and-seo-illustrator-tutorials/
  date: '2009-10-05 04:15:06 -0700'
  date_gmt: '2009-10-05 10:15:06 -0700'
  content: "[...] Emacs Power: remote servers and shell commands [...]"
- id: 146
  author: Susan Pinochet (sdp) 's status on Monday, 05-Oct-09 13:07:47 UTC - Identi.ca
  author_email: ''
  author_url: http://identi.ca/notice/11367782
  date: '2009-10-05 07:07:51 -0700'
  date_gmt: '2009-10-05 13:07:51 -0700'
  content: "[...] !emacs power: remote servers and shell commands http:&#47;&#47;gregorygrubbs.com&#47;wordpress&#47;emacs-power-remote-servers-and-shell-commands&#47;
    [...]"
- id: 147
  author: Jason
  author_email: jro@codegrinder.com
  author_url: http://jro.codegrinder.com
  date: '2009-10-05 21:27:38 -0700'
  date_gmt: '2009-10-06 03:27:38 -0700'
  content: Great post!  Just out of curiosity what versions of emacs&#47;ido&#47;etc
    are you running this on.  I'm seeing some different behavior in mine when I try
    to get a shell on the remote server from within dired.
- id: 148
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2009-10-06 15:52:28 -0700'
  date_gmt: '2009-10-06 21:52:28 -0700'
  content: "Thanks, Jason.  \r\n\r\nLet's see, I'm running primarily on Ubuntu 9.10
    (karmic alpha-6); GNU Emacs 23.1.50.1; ido 1.57-ish that was included in this
    release of Emacs.\r\n\r\nI have noticed that some system process modes do not
    heed the TRAMP file syntax.  Flymake-mode comes to mind as one.  I think the solution
    is for the mode to call 'start-file-process instead of  'start-process.  I'm guessing
    that more modes are using 'start-file-process, and perhaps they did not do so
    in earlier versions."
- id: 1998
  author: Mike
  author_email: michaelr.hansen@gmail.com
  author_url: ''
  date: '2014-02-26 20:35:25 -0800'
  date_gmt: '2014-02-27 02:35:25 -0800'
  content: "Hi Greg,\r\n\r\nI am working with FTPS (Implicit over TLS specifically)
    and I am wondering how I can easily connect using TRAMP. Any thoughts?\r\n\r\nthanks
    - Mike"
---
<p><a href="http:&#47;&#47;flickr.com&#47;photos&#47;16230215@N08&#47;2898797929" title="Come Together"><img src="http:&#47;&#47;farm4.static.flickr.com&#47;3282&#47;2898797929_f209eeb4a4.jpg" &#47;><&#47;a></p>
<h4 id="sec-1">Emacs file and directory browsing <&#47;h4></p>
<p>Emacs has Dired, a great method for browsing directories; especially in combination with ido-mode, I prefer it to Windows Explorer, OS X Finder, Gnome Nautilus, or anything else I've used over the decades to browse file systems. You can quickly begin entering paths, and Dired helps you with directory and file name completion.<br />
<a id="more"></a><a id="more-372"></a></p>
<p>  As you browse directories, emacs lets you bookmark any path you may visit again. A very cool feature of emacs is the wide variety of shell-based modes: shell, term, interactive SQL, version control, recursive grep, and more.  When you are looking at a Dired buffer and invoke any of those commands, the shell is started in the directory you are looking at.</p>
<h4 id="sec-2">TRAMP: powerful remote file server access <&#47;h4></p>
<p>An emacs user will eventually discover that Dired becomes even more powerful with the built-in power of TRAMP (Transparent Remote (file) Access, Multiple Protocol).  This extends directory path syntax to include FTP, SSH, Rsync and other protocols for accessing remote files.</p>
<p>  An example of accessing a remote file on my development server <code>smeagol<&#47;code> from my laptop:</p>
<pre class="example">&#47;ssh:gregj@smeagol:work&#47;client1&#47;web&#47;index.php<br />
<&#47;pre></p>
<p>  A directory on an FTP server is accessed the same way:</p>
<pre class="example">&#47;ftp:ftpuser@ftp.example.com:<br />
<&#47;pre></p>
<p>  Even sudo is considered a 'protocol'; so to gain root access without leaving the comfort of your emacs session, use</p>
<pre class="example">&#47;sudo::&#47;etc&#47;hosts<br />
<&#47;pre></p>
<p>  Emacs even helps you browse remote servers, providing the same name completion you get on your local directories.</p>
<h4 id="sec-1">The amazing combo of TRAMP and shell commands<&#47;h4></p>
<p>  As wonderful as all this is, we are still in the realm of "mere" GUI editors that can browse remote servers. But we are dealing with emacs, the superset of all editors, so we expect even more.</p>
<p>  Imagine we are looking at a directory on a remote server at <code>&#47;ssh:myuser@remote.com:web&#47;public_html<&#47;code>, and decide to type</p>
<pre class="example">M-x shell<br />
<&#47;pre></p>
<p>  What happens? Why, emacs looks at our current directory, sees that it is a TRAMP remote path, and just does the Right Thing&trade;: in this case, invokes ssh, sets the directory on the remote server to ~myuser&#47;web&#47;public_html, and sets us at the shell prompt.</p>
<p>  Similarly, if we invoke version control (<code>vc-dir<&#47;code>, for example), or recursive grep (<code>rgrep<&#47;code>), or most other shell-based commands, emacs will open a secure shell first, then run the vc command (<code>svn<&#47;code>, <code>git<&#47;code>, etc) or <code>grep<&#47;code> <b>on the remote server!!<&#47;b> So for example, if I innocently invoke <code>rgrep<&#47;code> at the root of a remote WordPress installation, the grep command looks through all the files from the remote server. If on the other hand I were accessing the server using something like <a href="http:&#47;&#47;fuse.sourceforge.net&#47;sshfs.html">SSHFS<&#47;a>, all those files would be transferred to my local machine first and then searched!</p>
<h4 id="sec-3">Some examples <&#47;h4></p>
<p>  I'll save my favorite uses of this magic called Dired with TRAMP for last.  I often need to access a development system or a live WordPress installation remotely. To access the SQL client, I found I often had to browse for the WordPress config file, open it, search for the database access info, open a SQL session using <code>M-x sql-mysql<&#47;code> and fill in all the prompts to authenticate to the MySQL server.  It's great that emacs with TRAMP starts a shell on the remote machine, and initiates the mysql client on that machine.  But emacs allows you to do damn near anything you can imagine, so I realized I could write a function that does the following:</p>
<ol>
<li>
	Looks for wp-config.php in the current directory<br />
  <&#47;li></p>
<li>
	If not found, moves up a directory until it either finds the file or reaches the root of the filesystem<br />
  <&#47;li></p>
<li>
	If found, opens the config file and parses the database authentication parameters<br />
  <&#47;li></p>
<li>
	Feeds those parameters to the sql-mysql function and<br />
  <&#47;li></p>
<li>
	plops me into the MySQL prompt all logged in and ready to go!</p>
<p>  <&#47;li><br />
<&#47;ol></p>
<p>Another example: my iPod Touch has an SSH server running on it (don't ask me how it got there). I have discovered that many apps use SQLite to store their data.  I have been losing weight lately, and have been using the excellent <a href="http:&#47;&#47;www.loseit.com&#47;">Lose It!<&#47;a> app to track my meals and exercise.  The app gives me nice weekly summaries of my caloric intake, but does not give a weekly summary of my aerobic exercise.  Here's how I get that information now:</p>
<ol>
<li>
	I have a nice bookmark to the Lose It! application directory at<br />
	<code>&#47;scpc:mobile@172.16.17.118:&#47;var&#47;mobile&#47;Applications&#47;C6503545-700B-4395-9C8B-FE5B75CF6CD8&#47;<&#47;code>,<br />
	so I hit the Return key on that bookmark and wait for Dired to show me the files there.<br />
  <&#47;li></p>
<li>
	Browse to the Documents directory, wherein is stored the database for my personal history<br />
  <&#47;li></p>
<li>
	Invoke <code>M-x sql-sqlite<&#47;code> and enter the database file <code>UserDatabaseV1.sql<&#47;code> (using dabbrev as a shortcut)<br />
  <&#47;li></p>
<li>
	Wait for the SQLite prompt to appear, and run a lovely little SQL query using a YASnippets shortcut: </p>
<p>  <&#47;li><br />
<&#47;ol></p>
<pre class="src src-sql"><span style="color: #a020f0;">SELECT<&#47;span> <span style="color: #228b22;">date<&#47;span>(<span style="color: #0000ff;">'2001-01-01'<&#47;span>, <span style="color: #0000ff;">'+'<&#47;span> || <span style="color: #228b22;">Date<&#47;span> || <span style="color: #0000ff;">' day'<&#47;span>, <span style="color: #0000ff;">'-1 day'<&#47;span>, <span style="color: #0000ff;">'weekday 1'<&#47;span>, <span style="color: #0000ff;">'-7 day'<&#47;span>) <span style="color: #a020f0;">AS<&#47;span> Weekdate, strftime(<span style="color: #0000ff;">'%W'<&#47;span>,<span style="color: #228b22;">date<&#47;span>(<span style="color: #0000ff;">'2001-01-01'<&#47;span>, <span style="color: #0000ff;">'+'<&#47;span> || <span style="color: #228b22;">Date<&#47;span> || <span style="color: #0000ff;">' day'<&#47;span>, <span style="color: #0000ff;">'-1 day'<&#47;span>)) <span style="color: #a020f0;">AS<&#47;span> Week,   ExerciseName, ExerciseCategoryId, <span style="color: #da70d6;">SUM<&#47;span>(Minutes), <span style="color: #da70d6;">SUM<&#47;span>(CaloriesBurned)   <span style="color: #a020f0;">FROM<&#47;span> ExerciseLogEntries  <span style="color: #a020f0;">GROUP<&#47;span> <span style="color: #a020f0;">BY<&#47;span> Week;<br />
<&#47;pre></p>
<h4 id="sec-4">Summary <&#47;h4></p>
<p>I hope that this post gives an idea of the power of TRAMP on emacs.  It should at least explain the occasional ecstatic post you may see from your geekier tweeps.</p>
<p>As a bonus, here's what the above examples look like in use: it's unbelievable how fast emacs makes you after a quick 15 years of study.</p>
<p><object width="640" height="505"><param name="movie" value="http:&#47;&#47;www.youtube.com&#47;v&#47;UjPasLGWzD0&hl=en&fs=1&color1=0x5d1719&color2=0xcd311b"><&#47;param><param name="allowFullScreen" value="true"><&#47;param><param name="allowscriptaccess" value="always"><&#47;param><embed src="http:&#47;&#47;www.youtube.com&#47;v&#47;UjPasLGWzD0&hl=en&fs=1&color1=0x5d1719&color2=0xcd311b" type="application&#47;x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="640" height="505"><&#47;embed><&#47;object></p>
<p>  And here's my emacs lisp code that opens up a SQL prompt for any WordPress installation.  To use, eval the code and invoke <code>M-x gjg&#47;sql-mysql-wordpress<&#47;code></p>
<pre class="src src-emacs-lisp">(<span style="color: #a020f0;">defun<&#47;span> <span style="color: #0000ff;">gjg&#47;parse-wp-config-db<&#47;span> (wpconfig-path)<br />
  <span style="color: #0000ff;">"Read in and parse the DB settings from a WordPress config file; binds 'global' vars for use by sql-mode"<&#47;span><br />
  (<span style="color: #a020f0;">save-excursion<&#47;span> <span style="color: #b22222;">;; <&#47;span><span style="color: #b22222;">will restore current buffer and default dir afterwards<br />
  <&#47;span>    (set-buffer (get-buffer-create (generate-new-buffer-name <span style="color: #0000ff;">" wp-config.php"<&#47;span>)))<br />
  (insert-file-contents wpconfig-path)<br />
  <span style="color: #b22222;">;; <&#47;span><span style="color: #b22222;">in regex: subexpr 1 is variable name, subexpr 3 is value: DB_{HOST,NAME,PASSWORD,USER}<br />
  <&#47;span>    (<span style="color: #a020f0;">while<&#47;span> (search-forward-regexp <span style="color: #0000ff;">"define\s*(\s*['\"]<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">(<&#47;span><span style="color: #0000ff;">DB_<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">(<&#47;span><span style="color: #0000ff;">HOST<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">|<&#47;span><span style="color: #0000ff;">NAME<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">|<&#47;span><span style="color: #0000ff;">PASSWORD<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">|<&#47;span><span style="color: #0000ff;">USER<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">)<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">)<&#47;span><span style="color: #0000ff;">['\"]\s*,\s*['\"]<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">(<&#47;span><span style="color: #0000ff;">[<&#47;span><span style="color: #0000ff;">^<&#47;span><span style="color: #0000ff;">'\"]*<&#47;span><span style="color: #0000ff; font-weight: bold;">\\<&#47;span><span style="color: #0000ff; font-weight: bold;">)<&#47;span><span style="color: #0000ff;">['\"]\s*)"<&#47;span> (point-max) 42   )<br />
  (<span style="color: #a020f0;">cond<&#47;span><br />
  ((equal <span style="color: #0000ff;">"DB_HOST"<&#47;span> (match-string-no-properties 1))<br />
  (setq sql-server (match-string-no-properties 3)))<br />
  ((equal <span style="color: #0000ff;">"DB_NAME"<&#47;span> (match-string-no-properties 1))<br />
  (setq sql-database (match-string-no-properties 3)))<br />
  ((equal <span style="color: #0000ff;">"DB_PASSWORD"<&#47;span> (match-string-no-properties 1))<br />
  (setq sql-password (match-string-no-properties 3)))<br />
  ((equal <span style="color: #0000ff;">"DB_USER"<&#47;span> (match-string-no-properties 1))<br />
  (setq sql-user (match-string-no-properties 3)))))<br />
  (kill-buffer )))</p>
<p>  (<span style="color: #a020f0;">defun<&#47;span> <span style="color: #0000ff;">gjg&#47;sql-mysql-wordpress<&#47;span> ()<br />
  <span style="color: #0000ff;">"Find WordPress config file in current tree, log into WP database if found."<&#47;span><br />
  (interactive)<br />
  (<span style="color: #a020f0;">let<&#47;span> ((mypath (locate-dominating-file default-directory <span style="color: #0000ff;">"wp-config.php"<&#47;span>)))<br />
  (<span style="color: #a020f0;">if<&#47;span> mypath<br />
  (<span style="color: #a020f0;">progn<&#47;span><br />
  (gjg&#47;parse-wp-config-db (concat mypath <span style="color: #0000ff;">"wp-config.php"<&#47;span>))<br />
  (pop-to-buffer (sql-connect-mysql))<br />
  (setq sql-interactive-product 'mysql)<br />
  (setq sql-buffer (current-buffer))<br />
  (sql-interactive-mode)<br />
  (<span style="color: #a020f0;">let*<&#47;span> ((match (string-match (nth 0 tramp-file-name-structure) mypath))<br />
  (myformat (<span style="color: #a020f0;">if<&#47;span> (eq nil match)<br />
  (format <span style="color: #0000ff;">" WordPress: local; %s; dbhost %s "<&#47;span><br />
  mypath<br />
  sql-server<br />
  )<br />
  (format <span style="color: #0000ff;">" WordPress: Remote %s@%s %s; dbhost %s "<&#47;span><br />
  (match-string (nth 2 tramp-file-name-structure) mypath)<br />
  (match-string (nth 3 tramp-file-name-structure) mypath)<br />
  (match-string (nth 4 tramp-file-name-structure) mypath)<br />
  sql-server))))<br />
  (setq header-line-format myformat))<br />
  )<br />
  (message <span style="color: #0000ff;">"Did not find wp-config.php in current path"<&#47;span>))<br />
  ))<br />
<&#47;pre></p>
<p> LocalWords:  Dired emacs SQL Rsync smeagol pre rgrep WordPress MySQL iPod<br />
 LocalWords:  SQLite</p>
