---
layout: post
status: publish
published: true
title: How to upgrade Wordpress SAFELY using Subversion and Rsync
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 5
wordpress_url: http://gregorygrubbs.magichome/?p=5
date: '2008-09-10 11:01:20 -0700'
date_gmt: '2008-09-10 17:01:20 -0700'
categories:
- Development
- wordpress
tags:
- subversion
- repository
- wordpress
- upgrading
- upgrade
- rsync
- hacks
comments:
- id: 208
  author: forkmantis
  author_email: ggrubbs.user@forkmantis.com
  author_url: http://friendfeed.com/forkmantis
  date: '2009-11-05 23:29:09 -0800'
  date_gmt: '2009-11-06 05:29:09 -0800'
  content: Excellent.  Thanks for this.
- id: 362
  author: Andrew Hopper
  author_email: hopperab@gmail.com
  author_url: http://www.andrewhopper.com
  date: '2009-12-24 06:44:56 -0800'
  date_gmt: '2009-12-24 12:44:56 -0800'
  content: Thanks for the great article.  This is very helpful.
---
<p>I keep all my Wordpress projects in a Subversion repository.  I also have a snapshot of unmodified 'vanilla' releases kept in the same repository.</p>
<p>Now theoretically I should simply be able to use the svn merge command in a working directory.  But I have encountered serious problems, including file corruption warnings, when using svn merge in an actively developed working directory.  Additionally, svn merge will delete files and directories that you added to the core Wordpress install.</p>
<p>The method outlined here will be safe <strong>even if you have hacked core    Wordpress files<&#47;strong>, as long as you are very careful in constructing your rsync command.</p>
<ol>
<li> Import and tag the latest Wordpress release into the repository
<pre class="src"><span style="color: #da70d6;">cd<&#47;span> &#47;tmp<br />
tar zxf &#47;path&#47;to&#47;archive&#47;wordpress-2.6.2.tar.gz<br />
    OR<br />
unzip &#47;path&#47;to&#47;archive&#47;wordpress-2.6.2.zip<br />
svn import -m <span style="color: #0000ff;">"Vanilla 2.6.2"<&#47;span> wordpress file:&#47;&#47;&#47;repository&#47;wordpress&#47;tags&#47;2.6.2<&#47;pre><br />
<&#47;li></p>
<li> Remove the directory in &#47;tmp
<pre class="src">rm -rf &#47;tmp&#47;wordpress<&#47;pre><br />
<&#47;li></p>
<li> Check out a fresh copy of your Wordpress project, and export a copy of the latest vanilla Wordpress
<pre class="src"><span style="color: #da70d6;">cd<&#47;span> &#47;tmp<br />
svn co --ignore-externals file:&#47;&#47;&#47;repository&#47;wordpress&#47;projects&#47;myhappyblog<br />
svn export file:&#47;&#47;&#47;repository&#47;wordpress&#47;tags&#47;2.6.2 wordpress-2.6.2<&#47;pre><br />
<&#47;li></p>
<li> Do a <strong>dry run<&#47;strong> of rsync, starting with something like the following
<pre class="src">rsync --dry-run -av --delete --svn-exclude --exclude <span style="color: #0000ff;">'.svn&#47;'<&#47;span> --exclude favicon.ico wordpress-2.6.2&#47; myhappyblog&#47;|less -SiX<&#47;pre><br />
<&#47;li></p>
<li> Now begins an iterative process &ndash; carefully examine the output from the above rsync dry run, <strong>paying special attention to files       that will be deleted<&#47;strong>, since those will show you directories and files you have added.  Add those directories or files as required using multiple '&ndash;exclude' options.  Here is an example from a recent upgrade I did:
<pre class="src">rsync --dry-run -av --delete --svn-exclude --exclude <span style="color: #0000ff;">'.svn&#47;'<&#47;span> --exclude favicon.ico --exclude <span style="color: #0000ff;">'images&#47;'<&#47;span> --exclude <span style="color: #0000ff;">'wp-content&#47;plugins&#47;podpress'<&#47;span> --exclude <span style="color: #0000ff;">'wp-content&#47;themes&#47;sandbox'<&#47;span> --exclude <span style="color: #0000ff;">'wp-content&#47;uploads'<&#47;span> wordpress-2.6.2&#47; myhappyblog&#47;|less -SiX<&#47;pre><br />
<&#47;li></p>
<li> Once you are satisfied that you are not asking rsync to delete files and directories you need, run the command without '&ndash;dry-run'
<pre class="src">rsync -av --delete --svn-exclude --exclude <span style="color: #0000ff;">'.svn&#47;'<&#47;span> --exclude favicon.ico --exclude <span style="color: #0000ff;">'images&#47;'<&#47;span> --exclude <span style="color: #0000ff;">'wp-content&#47;plugins&#47;podpress'<&#47;span> --exclude <span style="color: #0000ff;">'wp-content&#47;themes&#47;sandbox'<&#47;span> --exclude <span style="color: #0000ff;">'wp-content&#47;uploads'<&#47;span> wordpress-2.6.2&#47; myhappyblog&#47;<&#47;pre><br />
<&#47;li></p>
<li> Now change to your project working directory and look at the output of 'svn stat', here including sample output:
<pre class="src">svn stat</p>
<p>M      wp-login.php<br />
M      wp-includes&#47;post.php<br />
M      wp-includes&#47;version.php<br />
M      wp-includes&#47;query.php<br />
M      wp-includes&#47;formatting.php<br />
M      wp-includes&#47;pluggable.php<br />
M      wp-includes&#47;widgets.php<br />
M      wp-settings.php<br />
M      wp-admin&#47;includes&#47;template.php<br />
M      wp-admin&#47;includes&#47;image.php<br />
M      wp-admin&#47;import&#47;textpattern.php<br />
M      wp-admin&#47;css&#47;press-this-ie.css<&#47;pre><br />
<&#47;li></p>
<li> (conditional) In major upgrades, there will be Wordpress core file deletions and additions.  Handling these will require an extra couple commands, shown below.  These commands are only necessary if there are additions and deletions.
<pre class="src"><span style="color: #b22222;"># <&#47;span><span style="color: #b22222;">tell repository about deleted files that were removed by rsync<br />
<&#47;span>svn remove --force <span style="color: #ff00ff;">`svn stat |egrep '^\!' | cut -d' ' -f2-999`<&#47;span><br />
<span style="color: #b22222;"># <&#47;span><span style="color: #b22222;">add new files to repository<br />
<&#47;span>svn add <span style="color: #ff00ff;">`svn stat|egrep '^\?' | cut -d' ' -f2-999`<&#47;span><&#47;pre><br />
<&#47;li></p>
<li> You may choose to look through all the changes, or you may decide that the files that have been changed are safe (ie, unhacked Wordpress core files).Now you are ready to commit the changes to the repository.
<pre class="src">svn diff | less <span style="color: #b22222;"># <&#47;span><span style="color: #b22222;">optional<br />
<&#47;span>svn commit -m <span style="color: #0000ff;">"Upgraded to Wordpress 2.6.2"<&#47;span><&#47;pre><br />
<&#47;li></p>
<li> At long last, you can go to the working directory where you are actively developing, and update that.  Once you have tested thoroughly, you will be ready to update your live site (possibly with the same 'svn update' command).
<pre class="src"><span style="color: #da70d6;">cd<&#47;span> &#47;path&#47;to&#47;my&#47;development&#47;myhappyblog<br />
svn up<&#47;pre><br />
<&#47;li></p>
<li> Repeat from Step 3 for each of your SVN-managed Wordpress projects!<&#47;li>
<li> Drink.  Pray that Wordpress is not upgraded for at least another 6 months.<&#47;li><br />
<&#47;ol></p>
