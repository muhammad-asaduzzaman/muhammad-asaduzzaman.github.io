---
layout: page
title: LHDiff
description: A Language-Independent Technique for Tracking Source Code Lines
img: assets/img/lhdiff_line_tracking_examples.png
importance: 1
category: work
related_publications: einstein1956investigations, einstein1950meaning
---

Tracking source code lines between two different versions of a file is a fundamental step for solving several important problems in software maintenance, such as locating bug-introducing changes, tracking code fragments or defects across versions, merging file versions, and software evolution analysis. LHDiff is a language-independent technique for tracking source code lines across versions. It leverages SimHash technique to speed up the line mapping process. Our evaluation of LHDiff with three state-of-the-art techniques using test suites containing different degrees of changes and also with a mutation-based strategy shows a high potential return of our lightweight technique.


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

Consider the following two versions of a source file. Popular file differencing programs (such as Unix diff utility) cannot track lines that are changed or reordered, instead report that those lines are deleted from the old file and new lines are added in the next version of the file. For the above example, diff cannot detect that line 4 of the old file is moved to line 8 in the new file. Instead, reports line 4 as deleted and line 8 as added. LHDiff can correctly establish the mapping between lines 4 and 8. While the above example is a toy example, it shows the importance of LHDiff. If line 4 contains a bug, you can use LHDiff to track the buggy line in the next version to fix it.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/lhdiff_code_example.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Two different versions of the same file.
</div>

A command-line version of the tool is now available to download. Please download the jar file and run this from the command line using the following instructions:
java -jar lhdiff.jar

The tool requires Java runtime environment which can be downloaded from here.

The following command line options are available to work with LHdiff:

Usage Example
---
    usage: java -jar lhdiff.jar [-i] [-k candidateSetSize] [-p contextWeight Threshold] 
    [-cnm contentMetric][-cxm contextMetric] [-cxs contextSize] [-ls lineSplit] 
    [-ob outputBoth] oldfile newfile
---

You can also type help in the command line to learn details about different options available withing LHDiff.
---
usage: java -jar lhdiff.jar help
---

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
