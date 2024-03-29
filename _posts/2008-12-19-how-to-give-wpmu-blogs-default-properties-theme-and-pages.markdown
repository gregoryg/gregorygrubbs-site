---
layout: post
status: publish
published: true
title: How to give all new WPMU blogs default properties, theme and pages
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 63
wordpress_url: http://gregorygrubbs.com/?p=63
date: '2008-12-19 13:22:54 -0800'
date_gmt: '2008-12-19 19:22:54 -0800'
categories:
- Development
- wordpress
tags:
- wordpress
- php
- wpmu
comments:
- id: 138
  author: Joel Adria
  author_email: joel.adria@gmail.com
  author_url: http://jole.ca/
  date: '2009-08-19 10:27:13 -0700'
  date_gmt: '2009-08-19 16:27:13 -0700'
  content: "Hi there,\r\n\r\n\x7FThis is just what I've been looking for! Where did
    you put this code exactly though? If it were placed in the functions.php file
    it wouldn't be called if that theme wasn't in use... can you just place it anywhere?
    Like wp-config.php or something?\r\n\r\nThanks,\r\n-Joel"
- id: 140
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2009-08-26 11:26:56 -0700'
  date_gmt: '2009-08-26 17:26:56 -0700'
  content: "@Joel: I wrote a plugin that has to be activated for the functionality
    to work."
- id: 141
  author: Jason
  author_email: jb5531@gmail.com
  author_url: ''
  date: '2009-08-31 12:57:43 -0700'
  date_gmt: '2009-08-31 18:57:43 -0700'
  content: "Cool, this will really help! I'm just a little confused about what add_blog_option($blog_id,
    \r\n\t        'campus_selection_criteria', \r\n                \"CampusStateID
    LIKE '%'\");\r\naccomplishes?"
- id: 149
  author: Padma
  author_email: padma@infineoninfotech.com
  author_url: ''
  date: '2009-10-07 06:19:14 -0700'
  date_gmt: '2009-10-07 12:19:14 -0700'
  content: As I am newbie I don't know how to write plugin for a function to work
    ,Can you give me some reference for that function to work ?
- id: 202
  author: Ninjaboy
  author_email: enquiries@photoshopninja.com
  author_url: ''
  date: '2009-11-04 10:28:53 -0800'
  date_gmt: '2009-11-04 16:28:53 -0800'
  content: Wow Gregory - you have just saved me so much work! Thank you for sharing
    this, just what I have spent a very long time researching... works a treat!
- id: 417
  author: aaron lamar
  author_email: aaron.lamar@yahoo.com
  author_url: http://www.stylesum.com
  date: '2010-09-26 16:21:08 -0700'
  date_gmt: '2010-09-26 22:21:08 -0700'
  content: "Hey just so you know the \r\n\r\n'page_template' => 'template-whatever.php',\r\n\r\nis
    no longer used as of 10&#47;1&#47;2009\r\n\r\nin stead you have to update the
    meta data using \r\n\r\n   here is a the wordpress page to learn how to use it
    \ \r\n\r\nhttp:&#47;&#47;codex.wordpress.org&#47;Function_Reference&#47;update_post_meta"
---
<p>I've been developing an application on Wordpress-MU and thought I'd share a cool tip.</p>
<p>When new web sites are generated by my client, I wanted the experience to be painless; a one-button ready-to-go web site.</p>
<p>It turns out there is an action hook (of course there is!) when a new blog is created.&nbsp; So let's get down to the nitty gritty and see how to implement it.</p>
<p>I wanted to create a property that would apply to the new web site, which would allow my client to limit what data gets displayed on that site.&nbsp; I also wanted to generate the basic set of pages that I am using to support the sites' URL structure.&nbsp; Each page has a unique template that gives it some special navigation and content mojo.</p>
<p>So first I set the site-global option:</p>
<pre lang="php">
add_blog_option($blog_id,<br />
	        'campus_selection_criteria',<br />
                "CampusStateID LIKE '%'");<br />
<&#47;pre></p>
<p>Now for the pages with their templates.&nbsp; In order to let wp_insert_post know which blog to use, we use a handy function call:</p>
<pre lang="php">
switch_to_blog($blog_id);<br />
<&#47;pre></p>
<p>We will also need to specify the theme we are using so that the starting theme will be selected and the templates will be correctly associated.</p>
<p>I can then create the pages as I would in Wordpress-non-MU.&nbsp; The final step is to call add_action() to hook this code into the blog creation event.</p>
<p>Here is the code in its entirety</p>
<pre lang="php">
function dscp_initialize_blog($blog_id) {<br />
   add_blog_option($blog_id,<br />
                   'campus_selection_criteria',<br />
                   "CampusStateID LIKE '%'");<br />
   switch_to_blog($blog_id);<br />
   &#47;&#47; switch theme<br />
   switch_theme('thematic', 'mychildtheme');<br />
   $postdata = array('post_parent' => 0,<br />
   'post_status' => 'publish',<br />
   'post_title'&nbsp;&nbsp; => 'DESCRIPTIVE TITLE',<br />
   'post_name'&nbsp; => 'descriptive-title', &#47;* the slug *&#47;<br />
   'page_template' => 'template-whatever.php',<br />
   'post_type'&nbsp;&nbsp; => 'page');<br />
   $newid = wp_insert_post($postdata);<br />
   if ($newid && !is_wp_error($newid)) {<br />
      add_meta($newid);<br />
   } else {<br />
      &#47;&#47; your error handling code<br />
   }<br />
}</p>
<p>add_action('wpmu_new_blog', 'dscp_initialize_blog');<br />
<&#47;pre></p>
