---
layout: page
title: CSCC
description: A Simple, Efficient, Context Sensitive Code Completion Tool
img: assets/img/cscc_example.jpeg
importance: 2
category: work
---
Developers depend on APIs of frameworks and libraries to support the development process. Due to the large number of APIs, it is difficult to learn, remember and use them during the development of software. To mitigate the problem modern integrated development environments provide a code completion facility that frees developers from remembering every detail. We introduce CSCC, a simple, efficient context-sensitive code completion tool that leverages previous code examples to support method completion. Compared to the existing code completion tools, CSCC uses new sources of information together with lightweight context-sensitive source code analysis to better recommend API method calls.

Installation
---
The tool is implemented as an Eclipse plugin. Please download the following file and put the file in the drop-ins folder of Eclipse. We recommend using Eclipse Kepler (Windows version) which can be downloaded from online.

Required Files
---
Click on the link to download the jar file.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cscc_plugin.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Download and copy the jar file in the drop-ins folder of your Eclipse. Now restart Eclipse. You can find CSCC configuration options in the Eclipse Preference Page.

Enable/Disable CSCC
---
You can also enable/disable CSCC by selecting or deselecting the check box associated with CSCC in the Advanced Content Assist preference page of Eclipse (see the above figure).
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cscc_selection.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

CSCC in Action
---
CSCC comes with code examples for Java SWING/AWT libraries. Therefore, the tool can provide method completion support after pressing any object from those libraries. For example, in the following figure, a developer is writing code to create a JFrame. Consider he is in the middle of his development and invoke CSCC by pressing dot (.) after the JFrame object. CSCC will show possible method calls that can be called within this context in a popup menu. Developers can select any one of them and the corresponding method call will be inserted in the source code.
You can also enable/disable CSCC by selecting or deselecting the check box associated with CSCC in the Advanced Content Assist preference page of Eclipse (see the above figure).
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cscc_example.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The completion proposals made by CSCC are highlighted with a different icon and font.

Creating Custom Model
---
CSCC supports creating custom models for your target framework code completion. To do that you need to first create a folder named “model” in a specific location in your computer. Next, you need to create a file (“framework.txt”) and put the file inside the model folder. The exact location of these files can be obtained by accessing the preference page of CSCC (select window->preferences, you can see the CSCC option on the left-hand side of the dialogue box, see also the following figure). The “framework.txt” file is a simple plain text file, where each line of the file should contain a framework name. For example, if you want to create a custom model for java SWING framework, you need to the path prefix (“javax.swing.”) in the file. If you also want to create a model for the AWT framework, simply add “java.awt.” in a line in the framework.txt file.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cscc_preference.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Now, you need to instruct CSCC to generate the model. Select a project in your Eclipse IDE, right-click to bring the popup menu (see figure below). Select the command “generate model” which can be found under the CSCC menu item. CSCC will ask you to select a folder to save the file. Remember, you need to save the file under the model folder.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cscc_generate_model.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
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
