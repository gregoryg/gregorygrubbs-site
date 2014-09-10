---
layout: post
status: publish
published: true
title: One-button website publishing using WordPress-mu
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
excerpt: "<a title=\"Create many from the one\" href=\"http:&#47;&#47;flickr.com&#47;photos&#47;63989735@N00&#47;2431138923\"><img
  src=\"http:&#47;&#47;farm3.static.flickr.com&#47;2299&#47;2431138923_ff1f7aaa36.jpg\"
  alt=\"\" &#47;><&#47;a>\r\n\r\nI'm kinda loving on WordPress MU.  One of my recent
  projects required building web sites that pulled from a shared database.  WordPress
  MU allowed me to create a one-button website builder for my client.  WordPress MU
  calls them blogs, but my client will map a unique domain to each blog, and, well,
  doesn't use them as blogs at all.  So I'm calling them sites here.\r\n\r\nBy filling
  in three fields and clicking a button, my client creates a website that\r\n<ul>\r\n\t<li>
  Associates metadata with the site that specifies filter criteria to select records
  from the shared database<&#47;li>\r\n\t<li> Sets the permalink structure for the
  new site to a custom setting<&#47;li>\r\n\t<li> Creates a key category for the new
  site, one that is used for the posts generated in a later step<&#47;li>\r\n\t<li>
  Sets the theme<&#47;li>\r\n\t<li> All the initial pages are created, including content.
  \ The \"slug\" is set specifically to support the URL structure we want.  Page template
  is also set here because our design calls for a hierarchy of pages.<&#47;li>\r\n\t<li>
  If the PageMash plugin is active (it is auto-activated for all new blogs using Plugin
  Commander), certain pages are hidden, and a specific order is set so that page navigation
  comes out looking good<&#47;li>\r\n\t<li> The front page is set, because we are
  creating CMS sites, not blogs<&#47;li>\r\n\t<li>Several hundred posts are generated
  out of the underlying shared non-WPMU database tables<&#47;li>\r\n<&#47;ul>\r\nAll
  of this takes something like 20 seconds, at which point the admin can visit the
  new site as a subdomain.&nbsp; The theme has been applied, navigation works correctly,
  it is beauty.\r\n\r\n"
wordpress_id: 174
wordpress_url: http://gregorygrubbs.com/?p=174
date: '2009-03-30 18:50:48 -0700'
date_gmt: '2009-03-31 00:50:48 -0700'
categories:
- Development
- wordpress
- wordpress-mu
tags:
- wordpress
- plugin
- wordpress-mu
- automated
- website
- creation
comments:
- id: 139
  author: Fiona
  author_email: fiona@mulreany.ie
  author_url: http://www.mulreany.ie
  date: '2009-08-25 03:22:27 -0700'
  date_gmt: '2009-08-25 09:22:27 -0700'
  content: "Hi Greg,\r\nExcellent post! I'm doing something similar for 'instant'
    partially populated websites using WPMU. I've been making edits to wpmu-functions.php
    to create the initial pages but was having serious bother with hierarchy and child
    pages.\r\n\r\nI really like what you've done and I am going to give your method
    a try instead.\r\n\r\nFiona"
- id: 374
  author: Sumeet Chawla
  author_email: sumeet_chawla2005@yahoo.co.in
  author_url: http://www.code-pal.com
  date: '2010-05-24 02:19:46 -0700'
  date_gmt: '2010-05-24 08:19:46 -0700'
  content: "Hi Greg,\r\n              Even am working on a similar project. Am researching
    on how to use the e-commerce plugin so that the client can register and after
    registering, he can buy any particular theme, and then use it. Do you have any
    particular suggestions?\r\n\r\nThank you."
---
<p><a title="Create many from the one" href="http:&#47;&#47;flickr.com&#47;photos&#47;63989735@N00&#47;2431138923"><img src="http:&#47;&#47;farm3.static.flickr.com&#47;2299&#47;2431138923_ff1f7aaa36.jpg" alt="" &#47;><&#47;a></p>
<p>I'm kinda loving on WordPress MU.  One of my recent projects required building web sites that pulled from a shared database.  WordPress MU allowed me to create a one-button website builder for my client.  WordPress MU calls them blogs, but my client will map a unique domain to each blog, and, well, doesn't use them as blogs at all.  So I'm calling them sites here.</p>
<p>By filling in three fields and clicking a button, my client creates a website that</p>
<ul>
<li> Associates metadata with the site that specifies filter criteria to select records from the shared database<&#47;li>
<li> Sets the permalink structure for the new site to a custom setting<&#47;li>
<li> Creates a key category for the new site, one that is used for the posts generated in a later step<&#47;li>
<li> Sets the theme<&#47;li>
<li> All the initial pages are created, including content.  The "slug" is set specifically to support the URL structure we want.  Page template is also set here because our design calls for a hierarchy of pages.<&#47;li>
<li> If the PageMash plugin is active (it is auto-activated for all new blogs using Plugin Commander), certain pages are hidden, and a specific order is set so that page navigation comes out looking good<&#47;li>
<li> The front page is set, because we are creating CMS sites, not blogs<&#47;li>
<li>Several hundred posts are generated out of the underlying shared non-WPMU database tables<&#47;li><br />
<&#47;ul><br />
All of this takes something like 20 seconds, at which point the admin can visit the new site as a subdomain.&nbsp; The theme has been applied, navigation works correctly, it is beauty.</p>
<p><a id="more"></a><a id="more-174"></a></p>
<p>Here's how it is done in code.&nbsp; All you need to do is register a function for the action hook that WordPress MU runs when a new blog is created.</p>
<pre lang="PHP">function mypp_initialize_blog($blog_id) {<br />
  global $wp_rewrite;</p>
<p>  &#47;&#47; first, switch to the new blog; we will undo this at the<br />
  &#47;&#47; end of the function with restore_current_blog()<br />
  switch_to_blog($blog_id);<br />
  &#47;&#47; add a blog option, here a filter with a default value<br />
  add_option($blog_id, 'campus_selection_criteria', "CampusStateID='CA'");<br />
  &#47;&#47; Set a custom permalink structure<br />
  $wp_rewrite->set_permalink_structure('&#47;%category%&#47;%postname%');<br />
  $wp_rewrite->flush_rules();<br />
  if (function_exists('wp_create_category')) {<br />
      wp_create_category('schools');<br />
  }</p>
<p>  &#47;&#47; switch theme - this one specifies a child theme<br />
  switch_theme('corporate', 'tweaked-corporate');<br />
  &#47;&#47; Prepare options used by the pageMash plugin, auto-activated for new sites<br />
  if(!is_array(get_option('exclude_pages')))<br />
    $excludePagesList=array();<br />
  else<br />
    $excludePagesList = get_option('exclude_pages'); &#47;&#47;if it's empty set as an empty array<br />
  &#47;&#47; add pages to support the basic page structure<br />
  &#47;&#47; NOTE: the full code is not shown, standard use of wp_insert post<br />
  &#47;&#47; for each page:<br />
  $newid = wp_insert_post($postdata);<br />
  if ($newid &amp;&amp; !is_wp_error($newid)) {<br />
    add_meta($newid);<br />
    if ( IWANTOEXCLUDETHISPARTICULARPAGEFROMNAVIGATION )<br />
      $excludePagesList[] = $newid;<br />
    if (THISPARTICULARPAGE == 'home') {<br />
      update_option('show_on_front', 'page');<br />
      update_option('page_on_front', $newid);<br />
    }<br />
  } else {<br />
    &#47;&#47; error handling if insert post failed<br />
  }<br />
  &#47;&#47; end for each page<br />
  update_option('exclude_pages', $excludePagesList);<br />
  &#47;&#47; now generate posts for schools from the shared database<br />
  createSchoolAsPost('', $blog_id);<br />
  &#47;&#47; we're done! restore our initial blog<br />
  restore_current_blog();<br />
} &#47;&#47; function mypp_initialize_blog</p>
<p>add_action('wpmu_new_blog', 'mypp_initialize_blog');<&#47;pre></p>
