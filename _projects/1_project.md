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
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/lhdiff_configurations.png" title="available configurations in lhdiff" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Usage Example
---
```
    usage: java -jar lhdiff.jar [-i] [-k candidateSetSize] [-p contextWeight Threshold] 
    [-cnm contentMetric][-cxm contextMetric] [-cxs contextSize] [-ls lineSplit] 
    [-ob outputBoth] oldfile newfile
```

You can also type help in the command line to learn details about different options available within LHDiff.
```
    usage: java -jar lhdiff.jar help
```
