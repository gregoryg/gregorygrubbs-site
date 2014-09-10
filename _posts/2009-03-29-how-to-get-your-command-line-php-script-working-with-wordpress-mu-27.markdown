---
layout: post
status: publish
published: true
title: How to get your command line PHP script working with WordPress-MU 2.7
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 160
wordpress_url: http://gregorygrubbs.com/?p=160
date: '2009-03-29 10:47:23 -0700'
date_gmt: '2009-03-29 16:47:23 -0700'
categories:
- Development
- wordpress
- wordpress-mu
tags:
- wordpress
- php
- wpmu
- Ajax
- web server
- wordpress-mu
- command line
comments:
- id: 375
  author: James
  author_email: james@rotacoo.com
  author_url: ''
  date: '2010-05-27 04:04:56 -0700'
  date_gmt: '2010-05-27 10:04:56 -0700'
  content: Even easier than this is to set $_SERVER['HTTP_HOST'] to the correct domain
    before loading wp-load.php - then your PHP cli scripts work as before.
- id: 421
  author: Nuno Morgadinho
  author_email: nuno.morgadinho@gmail.com
  author_url: http://www.morgadinho.org
  date: '2010-10-12 09:36:39 -0700'
  date_gmt: '2010-10-12 15:36:39 -0700'
  content: Greg, this was very useful. I was calling a script in the way you described
    and having the same problem. Searched for a good while before coming here and
    now it works. Thanks
- id: 424
  author: Richard
  author_email: freexe@gmail.com
  author_url: ''
  date: '2010-10-28 06:48:18 -0700'
  date_gmt: '2010-10-28 12:48:18 -0700'
  content: "I found the following to work on Wordpress 3.01:\r\n\r\n&#47;&#47;WP Functions
    that I'm overriding\r\n&#47;&#47;Don't Redirect\r\nfunction auth_redirect(){};\r\n\r\n&#47;&#47;Pretend
    to be a real user\r\nfunction wp_get_current_user() {\r\n\tglobal $current_user;\r\n\twp_set_current_user(1);\r\n\tget_currentuserinfo();\r\n\r\n\treturn
    $current_user;\r\n}\r\n\r\n$_SERVER['PHP_SELF'] = '&#47;wp-admin&#47;admin.php';\r\n$_SERVER['REQUEST_URI']
    = '&#47;wp-admin&#47;admin.php?page=page_to_fake';\r\n$_SERVER['HTTP_HOST'] =
    'domain';\r\n$_GET['page']='page_to_fake';\r\n\r\n&#47;&#47;Path to the admin
    file\r\ninclude('..&#47;..&#47;..&#47;..&#47;wp-admin&#47;admin.php');"
---
<p><a href="http:&#47;&#47;flickr.com&#47;photos&#47;86639396@N00&#47;125838823" title="To the moon, Ajax!"><img src="http:&#47;&#47;farm1.static.flickr.com&#47;48&#47;125838823_e1a4d43a62_m.jpg" &#47;><&#47;a></p>
<p>	OK, this one is obscure. I only post about what I can't find on Google!</p>
<p>Until recently it has been possible to run command-line PHP scripts that include wp-config.php or wpmu-settings.php, in order to give those scripts access to WordPress globals like $wpdb, functions such as wp_insert_post etc.  </p>
<p>These scripts worked with WordPress-MU until recently -- now the scripts just exit with no output.  </p>
<p>The reason?  WPMU now initiates a redirect in the bootstrap process (search for 'header( "Location: "'  in wpmu-settings.php).  A browser can follow that redirection, but a command line script cannot.  So, if you want to initiate scripts that run from the command line, you will have to get the web server involved by invoking a text browser such as curl, wget, or links.  </p>
<p>It's best not to force your scripts to figure out where to find wp-config.php anyway.  I have taken to using a method suggested in <a href="http:&#47;&#47;wordpress.org&#47;support&#47;topic&#47;190522">this thread<&#47;a>, as shown in the code sample below.  The good news is, you know that your script will work the same whether initiated from a plugin in a graphic browser, used in an Ajax call, or initiated from cron or the command line shell.</p>
<p>So instead of kicking your script off with something like </p>
<pre lang="Bash">
&#47;usr&#47;bin&#47;php -q myscript.php<br />
<&#47;pre></p>
<p>You will create the script as a proper plugin and do something like</p>
<pre lang="Bash">
&#47;usr&#47;bin&#47;curl -d mypp_cmd=status http:&#47;&#47;mywpmusite.com<br />
<&#47;pre></p>
<p>Sample plugin code used for the above example follows.  The prefix for the functions is 'mypp', which of course stands for 'MY Plugin Prefix' to create a unique namespace.  The code below returns results as JSON encoded, and calls die()&#47;exit() at the end to prevent an entire page being created.  For log files run from cron, you may choose to return plain text instead.</p>
<pre lang="PHP">
  &#47;**<br />
   * Add a query var for this plugin<br />
   * This allows Ajax programs to operate without requiring file paths<br />
   * Instead, Ajax functions look for the query var 'mypp_cmd'<br />
   *&#47;<br />
  function mypp_query_vars($qvars) {<br />
    $qvars[] = 'mypp_cmd';<br />
    return $qvars;<br />
  } &#47;&#47; function mypp_query_vars</p>
<p>  &#47;**<br />
   * Handle AJAX requests in the template_redirect action<br />
   * We recognize our requests from the query var 'mypp_cmd'<br />
   * Here we allow GET requests using $_REQUEST; to restrict to POST, use $_POST instead<br />
   *&#47;<br />
  function mypp_template_redirect() {<br />
    global $wpdb;<br />
    $cmd = get_query_var('mypp_cmd');<br />
    $response = array();<br />
    if ($cmd) {<br />
      switch($cmd) {<br />
      case 'status':<br />
	$response['status'] = array('success' => true,<br />
				    'message' => 'Sample status message');<br />
	break;<br />
      default:<br />
	$response['status'] = array('success' => false,<br />
				    'msg' => 'Unknown command',<br />
				    'cmd' => $cmd);<br />
	break;<br />
      } &#47;&#47; switch $cmd<br />
      header('Content-type: text&#47;x-json; charset=utf-8');<br />
      print utf8_encode(json_encode($response));<br />
      die();<br />
    } &#47;&#47; $cmd is set<br />
  } &#47;&#47; function mypp_template_redirect</p>
<p>add_filter('query_vars', array($this, 'mypp_query_vars'));<br />
add_action('template_redirect', array($this, 'mypp_template_redirect'));</p>
<p><&#47;pre></p>
