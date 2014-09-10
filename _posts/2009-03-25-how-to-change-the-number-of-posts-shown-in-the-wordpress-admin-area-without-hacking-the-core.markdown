---
layout: post
status: publish
published: true
title: How to change the number of posts shown in the WordPress admin area without
  hacking the core
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 142
wordpress_url: http://gregorygrubbs.com/?p=142
date: '2009-03-25 07:24:49 -0700'
date_gmt: '2009-03-25 13:24:49 -0700'
categories:
- Development
- wordpress
tags:
- wordpress
- plugin
- hook
- filter
- admin
- edit posts
comments:
- id: 106
  author: Shawn Parker
  author_email: shawn@topfroggraphics.com
  author_url: http://top-frog.com
  date: '2009-03-25 09:14:40 -0700'
  date_gmt: '2009-03-25 15:14:40 -0700'
  content: You got me thinking - I think there's at least 3 ways to skin this cat
    with hooks or filters... I might have to write something up on that now that you
    got my brain churning.
- id: 107
  author: Rashmi Ranjan
  author_email: rashmi@gooval.com
  author_url: http://www.rashmiranjanpadhy.com
  date: '2009-03-27 21:59:03 -0700'
  date_gmt: '2009-03-28 03:59:03 -0700'
  content: That helped a lot ... thanks a ton
- id: 137
  author: Andrew
  author_email: andrew.mccluskey@gmail.com
  author_url: http://music2work2.com
  date: '2009-06-30 10:49:59 -0700'
  date_gmt: '2009-06-30 16:49:59 -0700'
  content: "Hi Gregory - thank you for posting the solution to this one - please excuse
    my obvious ignorance, but - which file would I insert the code into?\r\n\r\nmany
    thanks\r\n\r\nAndrew"
- id: 142
  author: Andrew
  author_email: andrew.mccluskey@gmail.com
  author_url: http://music2work2.com
  date: '2009-09-26 15:03:53 -0700'
  date_gmt: '2009-09-26 21:03:53 -0700'
  content: "Big thank you to Gregory - I just successfully created my first plugin
    with your code - and of course understand a little more about the whole wordpress
    platform.\r\n\r\nThank you for taking the time to follow up - I very much appreciate
    it.\r\n\r\nAndrew"
---
<p>[caption id="attachment_154" align="alignnone" width="500" caption="use the hook!"]<img class="size-full wp-image-154" title="use the hook!" src="http:&#47;&#47;gregorygrubbs.com&#47;wp-content&#47;uploads&#47;2009&#47;03&#47;2921148701_6d1985e27f-cropped.jpg" alt="use the hook!" width="500" height="248" &#47;>[&#47;caption]</p>
<p>It is easy to go in and hack the core WordPress files to change the hard-coded number, but I wanted to find a way to do it with a hook. &nbsp;That way, I could one day change the number of posts shown using controls in the interface.</p>
<p>Though there is no filter provided for the number of posts displayed, I hit upon a method of doing this which I would like to share. &nbsp;Perhaps someone will point out a better way, but for now this is making me happy</p>
<p>The trick is to hijack the query string just for the query that produces the table of posts. &nbsp;Here's what I did:</p>
<pre lang="PHP">
&#47;**  * Extend the number of posts displayed in the Edit Posts  *&#47;<br />
function dapl_query_string($query_string) {<br />
    global $pagenow;<br />
    if (is_admin() && $pagenow == 'edit.php') {<br />
        $query_string = str_replace('posts_per_page=15', 'posts_per_page=100', $query_string);<br />
    }<br />
    return $query_string;<br />
}<br />
add_filter('query_string', 'dapl_query_string');<br />
<&#47;pre></p>
