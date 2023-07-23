---
layout: page
title: PARC
description: Recommending API Methods Parameters
img: assets/img/parc_example.jpeg
importance: 3
category: work
---

APIs have grown considerably in size. To free developers from remembering every detail of an API, code completion has become an integral part of modern IDEs. Most work on code completion targets completing API method calls and leaves the task of completing method parameters to the developers. However, parameter completion is also a non-trivial task. We present an Eclipse plugin, called PARC, that supports automatic completion of API method parameters. The tool is based on the localness property of source code, which states that developers tend to put related code fragments close together. PARC combines contextual and static type analysis to support a wide range of parameter expression types.

Required Files
---
The tool is available as an Eclipse plugin.  Currently, the plugin is available for the Eclipse Kepler SR2 packages. The following table lists the platforms supported with the platform-specific plugin jar files that need to be downloaded.

The plugin requires a model database with API code examples and it downloads/upgrades the model database automatically. However, you can also download the model database manually, placing the downloaded file in the active workspace of your Eclipse IDE.

To test the model download and unzip this project, and then import it into the Eclipse IDE.


Installation Instructions
---
[1] Download the Eclipse IDE (Eclipse Kepler release SR2 packages) and the required two jar files. Make sure that you download the correct jar files.

[2] Now, go to the Plugins folder located inside your Eclipse installation folder. Remove the jar file whose name starts with org.eclipse.jdt.ui_. Now put the plugin jar files (downloaded in the previous step) inside the plugin folder and start Eclipse IDE.

[3] To verify that the plugin has been installed correctly, open the preference page of Eclipse IDE. If the installation is successful, you will see the PARC Preferences menu on the left-hand side of the window as shown in the following figure.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/parc_preference_page.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

[4] Allow Eclipse content assist inserts method parameters automatically on method completion.
To do this follow the following steps:
Open the preferences of your Eclipse IDE and go to the content assist preferences (Java > Editor > Content Assist). Enable method argument filling  (see Fill method arguments and show guessed arguments checkbox). Next, enable sorting proposals by relevance (see Sort Proposals combobox). These are highlighted in the following figure.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/parc_sort.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
[5] Import the previously downloaded project in the Eclipse IDE. To use PARC, type dot(.) after a receiver name to open a popup menu for method call completion and select the target method call by pressing enter key. PARC will activate automatically and provide suggestions that are integrated with Eclipse JDT proposals.


Download the Model Database
---
PARC leverages previous code examples to make recommendations. Thus, it requires a model database that contains those code examples. We are happy to inform you that a model database is already available for you that contains code examples for Java AWT and Swing libraries. This means that PARC can recommend method parameters for method calls of those libraries and we plan to update the database for you with more libraries. The database will be downloaded automatically during the first use of the PARC and will be updated automatically.

If you face any difficulty, download the model file in your own computer and put that in your Eclipse workspace. For example, if Alice set the workspace of her Eclipse IDE to /Users/alice/Documents/alice_workspace, she needs to put the downloaded model file inside the alice_workspace folder. To learn more about workspace and switching workspace click here.

Create Your Own Model Database
---
If you have already developed code examples, you can use them to build your own model database. Simply select the project in the Project Explorer window of Eclipse, Right click to bring the context menu and select the model generation command under the  menuitem PARC. The created model database will be stored in the workspace of your Eclipse IDE, the name will be same as your selected project. An example of this is shown in the following figure.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/parc_model_creation.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Example of Using PARC in the Eclipse IDE
---
The following figure shows an example of using the plugin. A developer requests for method call completion by pressing the dot after typing the variable name (see part A of the figure). Eclipse shows the possible completion proposals through a popup menu. The developer selects the add method with String and Component parameter types. As soon as the developer makes the selection by pressing the enter key, PARC activates and recommends completion proposals through another popup menu starting from the first parameter (see part B of the figure). The suggestions made by PARC are highlighted with a different icon. The developer can cycle through the remaining parameters by pressing the tab key (see part C of the figure).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/parc_example.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
