---
layout: page
title: COSTER
description: Finding the Fully Qualified Name of the API Element in Online Code Snippets
img: assets/img/coster_costertool.png
importance: 3
category: work
---

Code snippets available in community question-answering sites (CQA) are a great source of learning how to use APIs. However, it is difficult to determine what APIs are discussed in those online code snippets because they often lack declaration and import statements. We introduce COSTER, a context-sensitive type solver that can find Fully Qualified Names (FQN) of API elements used in those code snippets. The tool uses three different similarity measures to rank the potential FQNs of query API elements. Our quantitative evaluation and user study demonstrate that the tool can help developers to reuse API usage examples by suggesting required import statements to compile the code. Inferring types of API elements that can help researchers and tool developers focus on developing techniques to precisely locate API usage examples.

The demonstration video describing our too is as follows:

Motivating Example
---
Consider the following example where a code snippet from a  Stack Overflow post (post id: 20157996) (on the top) is used by our tool to find the FQNs of the API elements in it (on the bottom).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_motivating.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Code snippet from a Stack Overflow post(https://stackoverflow.com/questions/20157996) (top) and the type annotated code snippet
</div>

The  Stack Overflow  code snippet on the top suffers from  declaration, external reference and name ambiguities. For example, API elements such as dFact, build, and doc do not have  declaration statements that cause the declaration ambiguity. API elements, such as DocumentBuilderFactory, Result, and Elemen do not have the import statements that are necessary to compile the code, causing the external reference ambiguity. The name Element matches with five different Element classes in JDK, causing the name ambiguity. Thus learning API usages from such an ambiguous code snippet is hard for developers and researchers. Resolving the FQNs of API elements can help to understand the API usages and also help to reuse the code snippet. To mitigate the problem, we build a tool named COSTER that finds Fully Qualified Names (FQNs) of API elements in the online code snippets. Our tool infers three types (i.e., FQNs) of API elements: Class objects, Field calls, and  Method calls. For example, COSTER identifies the FQN of the class object dfact (see line 2) as javax.xml.parsers.DocumentBuilderFactory. COSTER also determines the FQNs of method calls add.append(…) and doc.createTextNode(…) (see line 12) as org.w3c.dom.Element and org.w3c.dom.Document, respectively. Once the FQNs of API elements are determined, COSTER can identify the missing import statements also.

Feature of the Tool
---
COSTER  supports the following four features:

1. Infer Types: Determine types or FQNs of API elements. We use the term type or FQN interchangeably throughout the discussion.
2. Complete Import Statements: Add missing import statements
3. Training COSTER: This enables the tool to support type inference of new APIs
4. Evaluation: Researchers and tool developers can also use the tool to evaluate the performance of COSTER. This enables to compare COSTER with other type inference techniques.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_costertool.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Architecture of COSTER
</div>

The tool consists of five major components (shown as orange colored rectangular box) and four features (shown as green colored diamond box). The model generator component extracts the API elements present in the subject systems at the codebase based on the jar files present at the Jar repository. It then collects the context of each API element and sends the context to the model manager. The model manager calculates the occurrence likelihood score for each Fully Qualified Name (FQN) and stores the context along with the score in an inverted index we called it as a model. Our tool supports the feature training and retraining the model using the model generator component.  By retraining we mean, the user can update Occurrence Likelihood Dictionary supporting new APIs and subject systems.

Query generator collects the API elements and associated contexts from the online forums’ code snippets. The context of each API element is passed into the candidate list processor that takes the trained model as input and generates the candidate list for each test case and refines the candidates based on the likelihood, context similarity, and name similarity scores.  The top-k recommendations returns a ranked list of top-k FQNs(s) for each case that provide three features: inferring types of API element, completing the import statements and evaluating the tool. Infer types feature annotate the API elements within the code snippet and output the code along with the annotation in a file (similar to the right side of the motivating example). Import statement completions is done through an Eclipse plugin that includes the import statements before the code snippet upon pasting it in the Eclipse IDE. Evaluation features enables the user to recreate our evaluation results and uses them for future studies.

Download
The tool is available in two forms: a) Command line tool b) Eclipse plugin

Command line tool provides three features: Infer types, Training COSTER and Evaluation and Eclipse Plugin provides three features: Complete Import Statement, Infer Types and Training COSTER.

Command line tool:
Our command line tool can be downloaded through the following GitHub repository:

GitHub Repository: https://github.com/khaledkucse/COSTER

Additionally, the user needs to have data and model for executing all three features of command line tool. Those can be downloaded from the following links:

Data: http://bit.ly/costerData

Model: http://bit.ly/costerModel

Installing
To install the tool, following requirements need to be fulfilled.

Oracle Java 8
Maven
For installing the tool from GitHub repository run the following command to clone the repository:

git clone https://github.com/khaledkucse/COSTER.git
Running the command line tool:
To run the command line tool from Code, the user needs to import all dependency of the tool using Maven and download the coster_data and coster_model. Next (s)he extracts the files into data and model directories respectively and runs the following class file:

src/main/java/org/srlab/coster/COSTER.java

N.B: User needs to provide some program arguments (discussed later).

To run the command line tool using executable jar file, user needs to download the above mentioned Data and Model files and extracts them in respective places and run the following command to run the jar file

java -jar COSTER.jar <program arguments>
Let us see some examples of executing all three features of command line tool.

1. Infer Types: A user wants to learn the FQNs of APIs used in a SO code. (s)He can puts the code into a file named input.java, place the file within the tool directory and run the following command:

java -jar COSTER.jar -f infer -i input.java -o output.java -j data/jars/so/ -m model/ -t 1 -c cosine -n levenshtein
Here functionality is chosen as infer, path to input file is input.java and path to output file is output.java, path to the jar files repository at data/jars/so/, path to the models model/, number of top-k suggestions 1, method for context similarity is Cosine and method for name similarity is Levenshtein distance. An execution trace of the following figure will appear.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_infer.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Usage example of Infer Type feature
</div>



First some info related to the tool are shown. Next, the tool collects jar files, trained model files and input code snippet form input.java. It then extracts the code, collects potential API elements and infers them. Finally the annotated API elements along with the full code snippet is generated in output.java file.

2. Train: A user can reproduce our model and add new APIs with our trained model using train feature. To do that user needs to run the following command:

java -jar COSTER.java -f train -r data/GitHubDataset/subjectSystem/ -j data/jars/github/ -d data/GitHubDataset/dataset/ -m model/ -q 50 -k 0
Following execution trace will appear once the command is executed successfully.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_train.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Usages example of Training of COSTER model feature
</div>

Similar to previous feature it will show some information related to the tool at first. Next it extracts new subject systems, create training dataset, retrieve the trained model, and retrain the model.

3. Evaluation: Evaluation of the tool is done so that the user can reproduce the result we reported in our papers.  Two types of evaluation is supported. Intrinsic evaluation where users can evaluate the tool for the subject system and extrinsic evaluation where user can evaluate COSTER for StackOverflow code snippets. Let us consider the intrinsic evaluation and to do that user needs to use the following command:

java -jar COSTER.jar -f eval -e intrinsic -r data/TestDataset/subjectSystem/ -j data/jars/github/ -d data/TestDataset/dataset/ -t 1 -m model/ -c cosine -n levenshtein
After the successful run of the command following execution trace will appear.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_eval.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Usages example of Training model feature
</div>

The tool collects the model files, code snippets for evaluation and jar files. Next it extracts the code snippets and prepares a dataset of all test cases. Finally it infers test cases, calculates the performance metrics and shows them.

The command line tool supports following porgram arguments.
```
<figure class="wp-block-table"><table><tbody><tr><td>Option</td><td>Description</td><td>Default Value</td></tr><tr><td>-c</td><td>Similarity Functions for Context Similarity</td><td>cosine (default), jaccard, lcs</td></tr><tr><td>-d</td><td>Path to the intermediate dataset</td><td>data/GitHubDataset/dataset/</td></tr><tr><td>-e</td><td>Types of evaluation</td><td>intrinsic, extrinsic</td></tr><tr><td>-f</td><td>Type of functionality</td><td>train, retrain, infer, eval</td></tr><tr><td>-h</td><td>Prints the usage information</td><td>disabled</td></tr><tr><td>-i</td><td>Input file path for infer functionality</td><td>required</td></tr><tr><td>-j</td><td>Pat to the Jar repository</td><td>data/jars/github</td></tr><tr><td>-m</td><td>Path to the Model directory</td><td>model/</td></tr><tr><td>-n</td><td>Similarity functions for Name similarity</td><td>levenshtein (default), hamming, lcs</td></tr><tr><td>-o</td><td>Output filepath for infer functionality</td><td>required</td></tr><tr><td>-q</td><td>A threshold value of the minimum number of contexts for an FQN to be trained</td><td>50</td></tr><tr><td>-r</td><td>Path to the repository/code base</td><td>data/GIthybDataset/subjectSytem</td></tr><tr><td>-t</td><td>Integer representing the k in Top-k recommendation</td><td>1</td></tr></tbody></table></figure>

```

The arguments are very straightforward to use. For example “-c” means the similarity method for context similarity. In our proposed technique, we use Cosine similarity that calculates the cosine distance between context of the test case and each candidate. However, the user can use other string similarity metrics such as Jaccard similarity index or Longest Common Subsequence (LCS) similarity methods. Similarly, user can use Hamming distance or LCS for name similarity rather than the default Levenshtein distance in case of name similarity using “-n” argument.

DOCKER IMAGE:
To ease the user hassles of creating similar environment, we also provide a docker image that has a similar environment will all dependencies and files. Docker image can be found in the following docker hub repository.

Docker Image: https://hub.docker.com/r/khaledkucse/coster

To run our docker image the user only need to install Docker Engine, a lightweight operating system over the host operating system to store docker images, create docker containers form the images and running the containers using operating system virtualization technology. Detailed documentation about Docker and how to install the Docker Engine can be found here

For installing the docker image of COSTER, run the following command to pull the image from docker hub into the docker engine:

docker pull khaledkucse/coster:1.0.0
Next, use the following command to run the docker image

docker run -it --name coster khaledkucse/coster:1.0.0
The command creates a docker container named coster and run the container.  Inside the container, use the following command to execute the features of command line tool.

java -jar COSTER.jar <program arguments>

Eclipse Plugin
---
Our Eclipse plugin is available at the Eclipse Marketplace. Simply click Help -> Eclipse Marketplace and a window will appear. Write COSTER in the search text and click Go button. Following search result will appear.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_plugin_install.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    COSTER in Eclipse Marketplace
</div>

Installing
---
Hit the Install button to integrate COSTER plugin in the Eclipse Editor. The user needs to accept the APache 2.0 License. Additionally we did not include the security certificate inside the plugin and thus an warning message will show up telling the plugin is not certified. The user needs to click Install Anyway in order to complete the installWe will update the ation process. Acquiring Security Certificate is under process. We will update the plugin as soon as we get the certificate. After installing and restarting the IDE, COSTER menu will be seen in the menu bar like the following figure.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_installfirst.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
</div>

Running Eclipse Plugin
---
Before running any of the feature of the plugin, the user must explore the plugin’s preference page. To do that, select Windows -> Preferences -> COSTER. Following window will appear.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_prefernece.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
</div>

Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

The most important option is the first one “Directory Path to supporting files for plugin”. The user needs to point where (s)he keeps the supplementary files to run the plugin. The supplementary files can be found here: https://drive.google.com/file/d/1dB0_PkW4Ad72RIBAxuVgWnRPQnFoA_gY/view?usp=sharing.

Download the file and unzip at any location of the computer. Then using the Browse… button select the unziped directory. Other options give the user some flexibility to test the tool in different combination of settings. To get the effect of the options, the user needs to click Apply and Close button.

1. Fix Imports: Whenever a user copied a code snippet from the online forum, one important way to make the code compilable is to complete the import statements. Using our plugin, the user can do that. To do that, paste the code snippet within a method body in the editor and click the Fix Import command in the COSTER menu. The following changes will occur.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_plugin_complete.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Usages example of Fix Import feature of COSTER Eclipse Plugin
</div>

The plugin takes the code from the active editor and will run the complete feature on them and will return a list of import statements that are included after the package statement.

2. Infer Types: Similar to command line tool, the user can see the FQNs of the API element of a code snippet with this feature. Click Infer Types command in the COSTER menu and the following window will appear.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_plugin_infer.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Usages Example of Infer Types Feature of COSTER Eclipse Plugin
</div>

The user has the flexibility to browse the Java file containing the online code snippet or paste the code snippet in the Text Box denoted as 2 in the above figure. Next, the user will click the infer button and the FQNs returned by the tool will appear as the annotation before the API elements in the text box. Thus the user can learn the participating FQNs of the code snippet using our plugin.

3. Training COSTER: Users can also train the COSTER model using the plugin. To do that click Train Model command and the following window will appear.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/coster_plugin_train.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   Usages example of Train Model of COSTER Eclipse Plugin
</div>

The user needs to input the path of the repository that contains the subject systems though the Browse… button. Additionally, the user can include a new library by giving the path of the Jar repository. Upon clicking the Train button the plugin will train the COSTER model using the subject system and the jar repositories.

Publication
Our paper on COSTER has been accepted as a full technical paper in ASE 2019, where we not only explain the technique in detail but also compare the technique with other state-of-the-art techniques and analyze why our technique is comparatively better the compared technique using five different analyses. The data, model, and code used in our experiment are available to download. In case you want to use those to replicate the study or in a different study please feel free to contact us.

You can find more details on our technique in the following link:

COSTER Paper: http://bit.ly/costerPaper

C M Khaled Saifullah, M. Asaduzzaman, Chanchal K. Roy. Learning from Examples to Find Fully Qualified Names of API Elements in Code Snippets, Accepted to be published in 34th IEEE/ACM International Conference on Automated Software Engineering, 243-254., 2019.

CITATION
@inproceedings{coster,
  title={Learning from Examples to Find Fully Qualified Names of API Elements in Code Snippets},
  author={Saifullah, C M Khaled and Asaduzzaman, Muhammad and Roy, Chanchal K.},
  booktitle={Proceedings of the 34th International Conference on Automated Software Engineering (ASE)},
  pages={243--254},
  year={2019}
}
