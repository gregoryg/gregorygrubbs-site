---
layout: post
status: publish
published: true
title: Tips on Android Development Using Emacs
author:
  display_name: Gregory Grubbs
  login: gortsleigh
  email: Gregory@Dynapse.com
  url: http://gregorygrubbs.com
author_login: gortsleigh
author_email: Gregory@Dynapse.com
author_url: http://gregorygrubbs.com
wordpress_id: 485
wordpress_url: http://gregorygrubbs.com/?p=485
date: '2010-09-11 10:32:32 -0700'
date_gmt: '2010-09-11 16:32:32 -0700'
categories:
- Development
- emacs
- Android
tags:
- emacs
- Technology&#47;Internet
- Android
- Mobile development
- java
comments:
- id: 428
  author: Risto
  author_email: risto.mononen@gmail.com
  author_url: ''
  date: '2010-11-13 10:47:24 -0800'
  date_gmt: '2010-11-13 16:47:24 -0800'
  content: "Thanks, these were great tips!\r\nCompilation error message refer to missing
    includes. How should I set the classpath? I'm experienced with C and Emacs but
    new to Java, and trying the Android GoogleMaps tutorial from the developer site.\r\n\r\n
    \ BR, Risto\r\n\r\n\r\nThe emacs equivalent is found in jde-mode: M-x jde-import-find-and-import
    (C-c C-v C-z). Make sure the classpath is set correctly prior to starting jde-mode"
- id: 436
  author: Justinhj
  author_email: justinhj@gmail.com
  author_url: http://www.heyes-jones.com
  date: '2011-02-04 22:07:48 -0800'
  date_gmt: '2011-02-05 04:07:48 -0800'
  content: Thanks this saved me a lot of time I think! BTW android-ant-install fails
    with the message that I have two devices, my phone, and the emulator. How do I
    tell it which to use?
- id: 439
  author: Gregory Grubbs
  author_email: Gregory@Dynapse.com
  author_url: http://gregorygrubbs.com
  date: '2011-02-18 14:14:44 -0800'
  date_gmt: '2011-02-18 20:14:44 -0800'
  content: "@Justinhj: I resolve it by directly going to the command line.  adb has
    handy parameters:  -d for device, -e for emulator.  \n\nSo, for example, I use
    <code>M-x android-ant-compile<&#47;code>, but drop to the shell to install: <code>adb
    -e bin&#47;MyApp-debug.apk<&#47;code>"
- id: 453
  author: Justinhj
  author_email: justinhj@gmail.com
  author_url: http://www.heyes-jones.com
  date: '2011-03-13 22:54:07 -0700'
  date_gmt: '2011-03-14 04:54:07 -0700'
  content: Perfect thanks!
- id: 501
  author: Android Development Without Eclipse &laquo; realmike.org
  author_email: ''
  author_url: http://realmike.org/blog/2010/10/31/android-development-without-eclipse/
  date: '2011-06-13 10:08:21 -0700'
  date_gmt: '2011-06-13 16:08:21 -0700'
  content: "[...] also Gregory Grubbs&#8217;s site for more tips on Android development
    without [...]"
---
<p>Android using Emacs</p>
<div id="content">
<div id="text-1">
<p>For the intrepid Emacs user, here are some tips for doing Android development without Eclipse. I am working on a follow-up post with some general Android SDK tips.</p>
<p><&#47;div></p>
<div id="outline-container-1_1">
<h3 id="sec-1_1">Emacs prerequisites<&#47;h3></p>
<div id="text-1_1">
<ol>
<li><a href="http:&#47;&#47;github.com&#47;remvee&#47;android-mode&#47;blob&#47;master&#47;android-mode.el">android-mode<&#47;a><br />
This mode gives you the following interactive commands:</p>
<ul>
<li><code>M-x android-start-emulator<&#47;code> Start the Android SDK emulator from emacs<&#47;li>
<li><code>M-x android-start-ddms<&#47;code> Start the Android debugger<&#47;li>
<li><code>M-x android-logcat<&#47;code> Like syslog for Android<&#47;li>
<li><code>M-x android-ant<&#47;code> Run any ant task in the current project directory<&#47;li><br />
<&#47;ul><br />
<&#47;li></p>
<li>android.el<br />
This is a file included in the Android SDK. It duplicates some of the functionality of android-mode, but adds <code>M-x android-jdb<&#47;code>, which starts the JDB debugger once you have DDMS running.Load it from {SDK dir}&#47;tools&#47;lib<&#47;li></p>
<li>JDE<br />
Optional, but it's great for java code. Required to use beanshell shortcuts like the import statement command below (Generate and insert import statements)<&#47;li></p>
<li>Typical emacs setup cruft<br />
Here's what I have in my init file for Android:</p>
<pre>(add-to-list 'load-path <span style="color: #bc8f8f;">"~&#47;emacs&#47;android-mode"<&#47;span>)<br />
	    (<span style="color: #a020f0;">require<&#47;span> '<span style="color: #5f9ea0;">android-mode<&#47;span>)<br />
	    (setq android-mode-sdk-dir <span style="color: #bc8f8f;">"~&#47;work&#47;android&#47;android"<&#47;span>)<br />
	    (add-hook 'gud-mode-hook<br />
            (<span style="color: #a020f0;">lambda<&#47;span> ()<br />
            (add-to-list 'gud-jdb-classpath <span style="color: #bc8f8f;">"&#47;home&#47;gregj&#47;work&#47;android-sdk-linux_86&#47;platforms&#47;android-7&#47;android.jar"<&#47;span>)<br />
            ))<&#47;pre><br />
<&#47;li><br />
<&#47;ol><br />
<&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_2">
<h3 id="sec-1_2">Launch the emulator<&#47;h3></p>
<div id="text-1_2">
<p>Although you can start the emulator from within emacs using android-mode: <code>M-x android-start-emulator<&#47;code></p>
<p>I prefer to launch from the shell, since this allows me to exit emacs without having to restart the emulator, e.g.:</p>
<pre>emulator -avd starter-21 -partition-size 128 >&#47;dev&#47;null &amp;<&#47;pre><br />
<&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_3">
<h3 id="sec-1_3">Create a project<&#47;h3></p>
<div id="text-1_3">
<p>Instead of using the New Project wizard in Eclipse, use these steps to create an Android project using the shell:</p>
<pre>cd {project directory}<br />
	mkdir HelloAndroid<br />
	cd HelloAndroid<br />
	android create project --name HelloAndroid --target android-7 --path . --package home.hoochiepep.HelloAndroid --activity HelloAndroid<&#47;pre><br />
Change =--target=, =--package=, and =--activity= parameters as appropriate.</p>
<p>To get a list of valid targets for your SDK, use</p>
<pre>android list<&#47;pre><br />
<&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_3_1">
<h3>Specify the application name<&#47;h3></p>
<div>To change the name of the application, edit {project root}&#47;res&#47;values&#47;strings.xml:</p>
<pre class="src src-xml"><<span style="color: #0000ff;">string<&#47;span> <span style="color: #b8860b;">name<&#47;span>=<span style="color: #bc8f8f;">"app_name"<&#47;span>>Hello, Android<&#47;<span style="color: #0000ff;">string<&#47;span>><br />
<&#47;pre><br />
<&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_3_2">
<h3>Specify a minimum SDK level<&#47;h3></p>
<div>The Eclipse New Project wizard includes a Min SDK Version field. To set this without the wizard, add a line to AndroidManifest.xml as a child of manifest:</p>
<pre class="src src-xml"><<span style="color: #0000ff;">uses-sdk<&#47;span> <span style="color: #da70d6;">android<&#47;span>:<span style="color: #b8860b;">minSdkVersion<&#47;span>=<span style="color: #bc8f8f;">"2"<&#47;span> &#47;><br />
<&#47;pre><br />
<&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_4">
<h3 id="sec-1_4">Make an eclipse project ant-ready (do also when moved to a new machine)<&#47;h3></p>
<div id="text-1_4">
<p>Projects you pull from online will have been created using Eclipse, and will not have a build.xml file for ant.</p>
<p>Another common problem is that the file <code>local.properties<&#47;code> will be missing. Running an update as shown here will fix both problems:</p>
<pre>android update project --path . --target android-7 --subprojects<&#47;pre><br />
<&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_5">
<h3 id="sec-1_5">Generate and insert import statements<&#47;h3></p>
<div id="text-1_5">
<p>You will see references to a handy Eclipse command (invoked by Control-Shift-O) which adds import statements for referenced classes.</p>
<p>The emacs equivalent is found in jde-mode: <code>M-x jde-import-find-and-import<&#47;code> (C-c C-v C-z). Make sure the classpath is set correctly prior to starting jde-mode</p>
<p><&#47;div><br />
<&#47;div></p>
<div id="outline-container-1_6">
<h3 id="sec-1_6">Use the debugger within Emacs<&#47;h3></p>
<div id="text-1_6">
<ul>
<li>Install the app on the emulator using <code>M-x android-ant-install<&#47;code> (the 'install' target uses the debug apk)<&#47;li>
<li>Start ddms. There are no cmdline args, so you might as well use <code>M-x android-start-ddms<&#47;code><&#47;li>
<li>In the emulator, go to Dev Tools -> Development Settings and select the app as the debug app<&#47;li>
<li>In the emulator, start the app<&#47;li>
<li>Look in the ddms window for the app's debug port (usu. 8700 if the Dev Settings step was done)<&#47;li>
<li>Start jdb by invoking <code>M-x android-jdb<&#47;code> from android.elYou can also start jdb directly using the following command line params as a guide
<pre>jdb -sourcepath&#47;home&#47;gregj&#47;work&#47;android&#47;projects&#47;NotepadCodeLab&#47;Notepadv3&#47;src -attach localhost:8700<&#47;pre><br />
Set breakpoints in JDB, like so</p>
<pre>stop in com.android.demo.notepad3.NoteEdit.onResume<&#47;pre><br />
If the project directory is set correctly in the jdb command, you will be able to set breakpoints by line using jde-mode's <code>M-x gud-break<&#47;code> (C-x space).<&#47;li><br />
<&#47;ul><br />
<&#47;div><br />
<&#47;div><br />
<&#47;div></p>
