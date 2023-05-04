Download Link: https://assignmentchef.com/product/solved-cs412-homework-4
<br>
<h2>The Big Picture</h2>

In this assignment, we will build a general purpose classification framework from scratch. This framework contains two classification methods: a basic method and an ensemble method. More specifically, decision tree and random forest. Given certain training dataset following a specific data format, your classification framework should be able to generate a classifier and use this classifier to assign labels to unseen test data instances.

We will then test our classification framework with several datasets using both the basic method and the ensemble method, and evaluate the quality of the classifiers with different metrics.

In order to build this classification framework, we need to finish four steps as follows.

<ul>

 <li>Step 1: Read in training dataset and test dataset, and store them in memory.</li>

 <li>Step 2: Implement a basic classification method, which includes both training process and test process. Given a training dataset, the classification method should be able to construct a classifier correctly and efficiently. Given a test dataset, the classification method should be able to predict the label of the unseen test instances with the aforementioned classifier.</li>

 <li>Step 3: Implement an ensemble method using the basic classification method in Step 2. The ensemble classification method should also be able to train a classifier and predict labels for unseen data instances.</li>

 <li>Step 4: Test both the basic classification method and the ensemble method with different datasets. Evaluate their performances and write a report.</li>

</ul>

We introduced many classification methods in the lecture. However, in this assignment, we pick the following basic classifier and ensemble classifier.

<ul>

 <li>Decision Tree (gini-index) as the basic method, Random Forest as the ensemble version of the classification method. Note 1: Other classifiers can also fit into this basic-ensemble framework. For example, Naive Bayes as the basic method, and AdaBoost as ensemble method. We do not cover them in this assignment.</li>

</ul>

Note 2: Different Random Forest methods can be found online (we introduced two in the lecture notes). You can choose either one but Forest-RI might be easier to implement.

Note 3: Many off-the-shelf ML tools can be found online for our classification tasks, e.g., sklearn. Since the purpose of this assignment is to go through the basic classifier and ensemble classifier step by step, it is not allowed to use any third-party library in your code.

Note 4: The classification tasks we are handling here can be either <strong>binary classification </strong>or <strong>multi-class classification. </strong>Please make your code robust enough to handle both cases.

<h2>Step 1: Data I/O and Data Format</h2>

The classification framework should be able to parse training and test files, load these datasets into memory. We use the popular LIBSVM format in this assignment.

The format of

&lt;label&gt; &lt;index1&gt;:&lt;value1&gt; &lt;index2&gt;:&lt;value2&gt; …

…… ……

Each line contains an instance and is ended by a ‘
’ character. &lt;label&gt; is an integer indicating the class label. The pair &lt;index&gt;:&lt;value&gt; gives a feature (attribute) value: &lt;index&gt; is a non-negative integer and &lt;value&gt; is a number (we only consider categorical attributes in this assignment). Note that one attribute may have more than 2 possible values, meaning it is a multi-value categorical attribute.

You need to be careful about not using label information as an attribute when you build the classifier, in which case you can get 100% precision easily, but you will get 0 pts for Step 2 and Step 3.

<h2>Step 2: Implement the Basic Classification Method</h2>

In this step, you will implement the basic classification method, i.e., decision tree with <strong>gini-index</strong> as the attribute selection measure (note: the gini-index score is computed by considering every possible categorical value of the feature as a branch). Your classification method should contain two steps, training (build a classifier) and test (assign labels to unseen data instances). Many existing classification or prediction packages have the feature to save the learned classifier as a file so that users can load the classifier into the framework later and apply the same classifier on different test datasets asynchronously. However, in this assignment, we are going to skip this save-classifiers-as-files feature, and assume that the training and test processes happen in the same run.

Before you begin with your implementation, please first read the Project Organization and Submission section at the end of the assignment to get a general idea on how to organize your project and how to name your programs so the auto-grading system can compile and execute your programs correctly.

The classification method you implemented should be able to take both training file and test file as input parameters from the command line, use training dataset to build a classifier and test dataset with labeling information to evaluate the quality of the classifier. For example, if you are implementing Decision Tree using C/C++, your program should be able to finish the entire classification process when you type this command: ./DecisionTree train_file test_file If you use Java:

java classification.DecisionTree train_file test_file If you use Python: python2 DecisionTree.py train_file test_file (or python3 DecisionTree.py train_file test_file)

Your program should output (to stdout) k*k numbers (k number per line, separated by space, k lines total) to represent the confusion matrix of the classifier on testing data, where k is the count of class labels. These lines are sorted by the label id. In i-th line, the j-th numbers are the number of data points in test where the actual label is i and predicted label is j. And you will be needing these values in Step 4.

An example output can be found as follows (when k=4):

50 30 16 23

12 43 21 9 0 21 71 12

1 23 11 67

Note that if k=2, the output is a 2×2 matrix, which is similar to the table where the numbers represent true/false positive/negative. For more information about the confusion matrix and how to evaluate performance based on it, please read https://en.wikipedia.org/wiki/Confusion_matrix or watch the video.

To sanity check your output format, we provide a script, accuracy.py (Edit on Nov 26: this is clickable), for computing overall accuracy. You can pipe your output to this script using command line and check if it can generates the correct overall accuracy. For example, if C/C++ is used as the coding language, you may append ” | python2 accuracy.py” at the end and execute:

./DecisionTree train_file test_file | python2 accuracy.py The same also applies for java and python.

<h2>Step 3: Implement Ensemble Classification Method</h2>

In this step, you will implement an ensemble classification method using the basic classification method in Step 2, i.e., random forest. Very similarly, your ensemble classification method should take train_file and test_file as input, and output k*k values in k lines as the confusion matrix so that you can use these numbers to evaluate classifier quality in Step 4. For example, you are implementing random forest using C/C++, and the command line of running your program should look like this: ./RandomForest train_file test_file If you use Java: java classification.RandomForest train_file test_file If you use Python: python RandomForest.py train_file test_file

<h2>Step 4: Model Evaluation and Report</h2>

In this step, you will apply both methods you implemented in Step 2 and Step 3 on three real-world datasets and a synthetic dataset. Note that we preprocessed these datasets and partitioned them into training and test for you (click on the numbers in the table to download), so please do not use the original datasets directly.

<table width="671">

 <tbody>

  <tr>

   <td width="93"><strong>Name</strong></td>

   <td width="75"><strong>Num of Attributes</strong></td>

   <td width="66"><strong>Training Set Size</strong></td>

   <td width="45"><strong>Test Set </strong><strong>Size</strong></td>

   <td width="312"><strong>Source Link</strong></td>

   <td width="80"><strong>Labels</strong></td>

  </tr>

  <tr>

   <td width="93">balance.scale</td>

   <td width="75">4</td>

   <td width="66">400</td>

   <td width="45">225</td>

   <td width="312">http://archive.ics.uci.edu/ml/datasets/Balance+Scale</td>

   <td width="80">1 isBalanced, 2is Right, 3 is Left</td>

  </tr>

  <tr>

   <td width="93">nursery</td>

   <td width="75">8</td>

   <td width="66">8093</td>

   <td width="45">4867</td>

   <td width="312">http://archive.ics.uci.edu/ml/datasets/Nursery</td>

   <td width="80">1  is priority,2  isvery_recom,3  isspec_prior, 4 is not recom, 5 is recommend.</td>

  </tr>

  <tr>

   <td width="93">led</td>

   <td width="75">7</td>

   <td width="66">2087</td>

   <td width="45">1134</td>

   <td width="312">http://archive.ics.uci.edu/ml/datasets/LED+Display+Domain</td>

   <td width="80">1 is three, 2 is othernumbers</td>

  </tr>

  <tr>

   <td width="93">synthetic.social</td>

   <td width="75">128</td>

   <td width="66">3000</td>

   <td width="45">1000</td>

   <td width="312">N/A</td>

   <td width="80">1, 2, 3, and 4 represent four social groups respectively</td>

  </tr>

 </tbody>

</table>

If you are curious about the semantic meaning of each attribute or labels, please read the source links associated with the first three datasets. The fourth dataset is generated via distributed representation learning on a synthetic social network (a.k.a, network embedding), where binning is further performed to generate categorical attributes. You do not need to know these details in order to finish this assignment.

The main difference between the fourth dataset and the other three is that the former has a significantly larger number of attributes.

You need to apply both your basic classification method and your ensemble classification method on each dataset, and calculate the following model evaluation metrics using the output of your classification methods for both training and test datasets. Please do this manually or write a separate program (you do not need to turn this in), by taking the k*k numbers as input. Do not output these metrics from your classifiers directly since the auto-grader won’t be able to recognize them.

For overall performance, output:

Accuracy (overall accuracy = sum of the diagonal of your output matrix / sum of all entries in your output matrix) For each class, output:

F-1 Score.

<strong>Note 1: </strong>To evaluate the performance on each class, we regard the target class as positive and all others as negative. <strong>Note 2: </strong>The detailed equations of the above measures based on Confusion Matrix can be found in https://en.wikipedia.org/wiki/Confusion_matrix.

<strong>Parameter settings for each dataset in your submission</strong>

Please hardcode your choice of parameters (depth of decision tree, number of trees in random forest, etc.) <strong>for each dataset</strong> into your program. In other words, your program should choose the corresponding parameters according to the input datasets. Specifically, if <strong>train_file</strong> (the path to the training set) <strong>contains</strong> the string “balance.scale” the parameters tuned for the provided balance.scale dataset are used in this round of execution. The same goes for nursery, led, and synthetic.social.

Besides the four provided pairs of training-test files, we also hold some hidden datasets for the auto-grader to evaluate your implementation. The hidden datasets differ from the provided datasets in that the training-test files are resampled, while the raw data used to generate the hidden datasets are the same as those used to generate the provided datasets. The filename of

any hidden datasets would also contain balance.scale, nursery, led, or synthetic.social. As a result, the parameters you selected for the provided datasets will also work fine with the hidden datasets.

<strong>Report</strong>

Now you are ready to write your report. You should include the following sections in your report:

<ul>

 <li>At the very beginning of the report, summary of the overall accuracy on the test dataset for each dataset (2 methods * 4 datasets</li>

</ul>

= 8 numbers). These metrics are used to score the performance of the model, which is to be detailed in the next two sections;

<ul>

 <li>Brief introduction of the classification methods in your classification framework;</li>

 <li>All model evaluation measures you calculated above ((1 overall metric + # class * 1 per-class metric) * (1 on training set + 1 on test set) * 2 methods * 4 datasets);</li>

 <li>Parameters you chose during implementation and why you chose these parameters;</li>

 <li>Your conclusion on whether the ensemble method improves the performance of the basic classification method you chose, why or why not.</li>

</ul>

<h2>Competition (5 pts)</h2>

To add just a little competition, we test your random forest implementation on a hidden dataset very similar to the

provided synthetic.social. Ranking by the overall accuracy the implementation achieves on the test data, the person ranks first receives 5 points, the person ranks last receives 0 points, and everyone else in between receives a score linearly interpolated according to their rank. In the unfortunate case, an implementation does not finish within three minutes or does not generate results, the person would receive 0 points.

<h2>Homework Scoring Criterion</h2>

The total score for this homework is 100 points, including 80 points for implementation, 15 points for the report, and 5 points for the competition.

For implementation, one receives 10 points for each model that outperforms the (very lenient) cut-off score on each hidden dataset. The performance is solely determined by overall accuracy on the test dataset. We provide the cut-off scores as follows. Since the hidden datasets have distributions very similar to the provided ones, one can assume they would pass on the hidden datasets as long as they can pass on the provided datasets.

<table width="290">

 <tbody>

  <tr>

   <td width="97"> </td>

   <td width="92"><strong>DecisionTree</strong></td>

   <td width="101"><strong>RandomForest</strong></td>

  </tr>

  <tr>

   <td width="97">balance.scale</td>

   <td width="92">0.50</td>

   <td width="101">0.60</td>

  </tr>

  <tr>

   <td width="97">nursery</td>

   <td width="92">0.80</td>

   <td width="101">0.80</td>

  </tr>

  <tr>

   <td width="97">led</td>

   <td width="92">0.80</td>

   <td width="101">0.80</td>

  </tr>

  <tr>

   <td width="97">synthetic.social</td>

   <td width="92">0.40</td>

   <td width="101">0.50</td>

  </tr>

 </tbody>

</table>

Note that plagiarism would result in 0 points. In the past, we have also identified codes that generate fake confusion matrix as output, instead of implementing the algorithms. In this case, 0 points would also be given, since the models were not actually implemented. We grade the report based on its completeness and grade the competition as described in the previous section.