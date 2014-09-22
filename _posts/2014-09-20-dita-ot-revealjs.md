---
title: Reveal.js Based DITA-OT Transformation
layout: post
tags: [DITA,Documentation]
---

Today I want to share my first DITA-OT plugin with you. This plugin ships a new transformation scenario, called `reveal`, that transforms DITA maps into 
[reveal.js](http://lab.hakim.se/reveal-js) based web presentations. Currently, the functionality is very limited. Later, the transformation scenario will be able to generate two dimensional (nested) presentations. I'll implement this feature in an upcoming release.

You can take a look at a [reveal.js](http://lab.hakim.se/reveal-js) based presentation here: [lab.hakim.se/reveal-js](http://lab.hakim.se/reveal-js/)

I develop and test the plugin on a Linux machine, but it should work on Mac OSX and Microsoft Windows as well. If you have any issues, or suggestions for improvements, please add a comment or raise an issue on [Github](https://github.com/xephon2/com.github.xephon2.revealjs).

## Requirements
You need to have Git and a DITA-OT 1.8.+ installed and the path variables set via the `startcmd.bat` or `startcmd.sh` command.

## Installation
The plugin is hosted on Github. To install the plugin, you have to clone its repository and invoke the DITA-OT integrator.

1. Open a terminal and move to the `plugins` directory of your DITA-OT.
2. To clone the plugin repository, invoke the following command:

   ```
   git clone https://github.com/xephon2/com.github.xephon2.revealjs
   ```
3. Move to the root directory of your DITA-OT.
4. To integrate the plugin into the DITA-OT, call the integrator:

   ```
   ant -f integrator.xml
   ```
   
   Now the plugin should be successfully installed. Now you should be able to transform DITA maps into presentations using the new Ant target `reveal`.

## Testing the Installation
Test the new transformation scenario by typing `ant reveal`.
Because you did not specify an input file, the following output should appear:
{% highlight bash %}
BUILD FAILED
Input file is not specified, or is specified using the wrong parameter.
{% endhighlight %}
If the target has not been found, the following output indicates, that the plugin has not been successfully installed:
{% highlight bash %}
BUILD FAILED
Target "reveal" does not exist in the project "DOST".
{% endhighlight %}

## Using the Plugin
To show the usage of the plugin, let's create a DITA map with two topics and transform these files into a presentation.

### Create the DITA Map
1. Create a `reveal` directory in the `samples` directory of your DITA-OT.
2. Create a DITA map `map.ditamap` in this directory and add the following content:
{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE map PUBLIC "-//OASIS//DTD DITA Map//EN" "map.dtd">
<map chunk="to-content">
  <topicref href="topic1.dita"/>
  <topicref href="topic2.dita"/>
</map>
   {% endhighlight %}
   It is required that the presentation resides in a single HTML file. To force the DITA-OT to do that, the `chunk` attribute of the `map` element must be set to the value `to-content`.

### Create the First Topic
1. Create a topic `topic1.dita` in the same directory.
2. Add the following content:
{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE topic PUBLIC "-//OASIS//DTD DITA Topic//EN" "topic.dtd">
<topic id="topic-1">
  <title>Title of First Topic</title>
  <body>
    <p>A short paragraph.</p>
    <ul>
      <li>First list element</li>
      <li>Second list element</li>
    </ul>
  </body>
</topic>
{% endhighlight %}

### Create the Second Topic
1. Create a topic `topic2.dita` in the same directory.
2. Add the following content:
{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE topic PUBLIC "-//OASIS//DTD DITA Topic//EN" "topic.dtd">
<topic id="topic-2">
  <title>Title of Second Topic</title>
  <body>
    <image href="http://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Coat_of_arms_of_Hamburg.svg/343px-Coat_of_arms_of_Hamburg.svg.png" id="image_flx_4rl_mp" alt="Coat of Arms Hamburg"/>
  </body>
</topic>
{% endhighlight %}

### Start the Build Process
Start the build process by calling the following command in the root directory of the DITA-OT.
{% highlight bash %}
java -jar lib/dost.jar /i:samples/reveal/map.ditamap /outdir:out/reveal /transtype:reveal
{% endhighlight %}
If the output shows `BUILD SUCCESSFUL`, the transformation was successful.

### Launch the Presentation
Open the `index.html` file in the directory `out/reveal` with your browser.
