---
title: Reveal.js Based DITA-OT Transformation
layout: post
---

Today I wont to share my first DITA-OT plugin with you. This plugin ships a new transformation scenario, called **reveal**, that transforms DITA maps into reveal.js based web presentations. Currently, the functionality is very limited. Later, the transformation scenario will be able to generate two dimensional (nested) presentations. I'll implement this feature in an upcoming release.

You can take a look at a very simple reveal.js presentation generated with the DITA-OT here:

I develop and test the plugin on a Linux machine, but it should work on Mac OSX and Microsoft Windows as well. If you have any issues, or suggestions for improvements, please write me an E-mail or raise an issue on Github.

## Installation
The plugin is hosted on Github. To install the plugin, you have to clone its repository and invoke the DITA-OT integrator. It is assumed, that you have a DITA-OT 1.8.+ installed and have the path variables set via the ˋstartcmd.batˋ or ˋstartcmd.shˋ command.

1. Open a terminal and move to the ˋpluginsˋ folder of your DITA-OT.
2. To clone the plugin repository, invoke the following command:
   `git clone https://github.com/xephon2/com.github.xephon2.revealjs`
3. Move to the root folder for of your DITA-OT.
4. To integrate the plugin into the DITA-OT, call the integrator:
   `ant -f integrator.xml`
Now the plugin should be successfully installed. Now you should be able to transform DITA maps into reveal.js based presentation using the new Ant target `reveal`.

## Usage
To show the usage of the plugin, I'll give you a small example including a DITA map and two topics. Further on, I explain you how to generate the presentation with a single command and how to setup a simple Ant ˋbuild.xmlˋ file to make the transformation even simpler.

### Create the DITA map
It is required that the presentation resides in a single HTML file. To force the DITA-OT to do that, we have to change the default chunking method. To change the chunking, set the ˋchunkˋ attribute of the ˋmapˋ element to the value ˋto-contentˋ. I assume, that the ditamap and the topics reside in the same folder.

```xml
<map chunk="to-content">
<topicref href="topic1.dita"/>
<topicref href="topic2.dita"/>
</map>
```

Now, create two topics.

**topic1.dita**
```xml
<topic>
<title>Title of First Topic</topic>
<p>A short paragraph.</p>
<ul>
<li>First list element</li>
<li>Second list element</li>
</ul>
</topic>
```

**topic2.dita**
```xml
<topic>
<title>Title of Second Topic</topic>
<!-- Add an image here. Try to reference an image via HTTP, e.g. from Wikimedia. -->
</topic>
```

Now you can start the build process by calling the command ˋant revealˋ in the same folder.

**Build Command (Without build.xml)**
ˋant <!-- Create the command and add it here. -->ˋ


Optionally, if you do not want to remember such a complex command, create a ˋbuild.xmlˋ file that calls the new Ant target for you.

**build.xml**
```xml
<!-- Ant file -->
```
