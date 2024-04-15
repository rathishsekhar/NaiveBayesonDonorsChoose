# Naives Bayes on Donors Choose
# Table of Contents
1. Overview
2. About the DonorsChoose Data set
3. Code acttivity

# Overview
In this project, we used the Naive Bayes algorithm to analyze data from Donor's Choose a platform where teachers can request resources for their schools and classrooms. There were several steps involved in our analysis of just executing the model. First we split the data into subsets for training and cross-validation and testing. We then appliced the Nive Bayes alogrithm to different sets of features, including the conten of the project essays, various categorical details like teacher's prefix and project's grade category, as well as numerical information such as project's price. The hyperparameters were then tuned to optimize the model's performance. We ebaluated the model's performance using techniques like k-fold cross-validation, which helps ensure that our results are reliable and not just due to chance. Finally we summarized our findings in a clear and easy format to draw meaningufl conclusions from the data. 

The preliminary and intermediary steps, such as exploratory data analysis (EDA), data preprocessing, and feature engineering, are not presented here. Instead, we focus solely on demonstrating the final application of the Sci-kit Learn's Multinomial Naive Bayes model so as to showcase the author's learning process effectively.

# About the DonorsChoose Data Set
The following is the description of the data taken from 
https://www.kaggle.com/competitions/donorschoose-application-screening/data :


The `train.csv` data set provided by DonorsChoose contains the following features:

Feature | Description 
----------|---------------
**`project_id`** | A unique identifier for the proposed project. **Example:** `p036502`   
**`project_title`**    | Title of the project. **Examples:**<br><ul><li><code>Art Will Make You Happy!</code></li><li><code>First Grade Fun</code></li></ul> 
**`project_grade_category`** | Grade level of students for which the project is targeted. One of the following enumerated values: <br/><ul><li><code>Grades PreK-2</code></li><li><code>Grades 3-5</code></li><li><code>Grades 6-8</code></li><li><code>Grades 9-12</code></li></ul>  
 **`project_subject_categories`** | One or more (comma-separated) subject categories for the project from the following enumerated list of values:  <br/><ul><li><code>Applied Learning</code></li><li><code>Care &amp; Hunger</code></li><li><code>Health &amp; Sports</code></li><li><code>History &amp; Civics</code></li><li><code>Literacy &amp; Language</code></li><li><code>Math &amp; Science</code></li><li><code>Music &amp; The Arts</code></li><li><code>Special Needs</code></li><li><code>Warmth</code></li></ul><br/> **Examples:** <br/><ul><li><code>Music &amp; The Arts</code></li><li><code>Literacy &amp; Language, Math &amp; Science</code></li>  
  **`school_state`** | State where school is located ([Two-letter U.S. postal code](https://en.wikipedia.org/wiki/List_of_U.S._state_abbreviations#Postal_codes)). **Example:** `WY`
**`project_subject_subcategories`** | One or more (comma-separated) subject subcategories for the project. **Examples:** <br/><ul><li><code>Literacy</code></li><li><code>Literature &amp; Writing, Social Sciences</code></li></ul> 
**`project_resource_summary`** | An explanation of the resources needed for the project. **Example:** <br/><ul><li><code>My students need hands on literacy materials to manage sensory needs!</code</li></ul> 
**`project_essay_1`**    | First application essay<sup>*</sup>  
**`project_essay_2`**    | Second application essay<sup>*</sup> 
**`project_essay_3`**    | Third application essay<sup>*</sup> 
**`project_essay_4`**    | Fourth application essay<sup>*</sup> 
**`project_submitted_datetime`** | Datetime when project application was submitted. **Example:** `2016-04-28 12:43:56.245`   
**`teacher_id`** | A unique identifier for the teacher of the proposed project. **Example:** `bdf8baa8fedef6bfeec7ae4ff1c15c56`  
**`teacher_prefix`** | Teacher's title. One of the following enumerated values: <br/><ul><li><code>nan</code></li><li><code>Dr.</code></li><li><code>Mr.</code></li><li><code>Mrs.</code></li><li><code>Ms.</code></li><li><code>Teacher.</code></li></ul>  
**`teacher_number_of_previously_posted_projects`** | Number of project applications previously submitted by the same teacher. **Example:** `2` 

<sup>*</sup> See the section <b>Notes on the Essay Data</b> for more details about these features.

Additionally, the `resources.csv` data set provides more data about the resources required for each project. Each line in this file represents a resource required by a project:

Feature | Description 
----------|---------------
**`id`** | A `project_id` value from the `train.csv` file.  **Example:** `p036502`   
**`description`** | Desciption of the resource. **Example:** `Tenor Saxophone Reeds, Box of 25`   
**`quantity`** | Quantity of the resource required. **Example:** `3`   
**`price`** | Price of the resource required. **Example:** `9.95`   

**Note:** Many projects require multiple resources. The `id` value corresponds to a `project_id` in train.csv, so you use it as a key to retrieve all resources needed for a project:

The data set contains the following label (the value you will attempt to predict):

Label | Description
----------|---------------
`project_is_approved` | A binary flag indicating whether DonorsChoose approved the project. A value of `0` indicates the project was not approved, and a value of `1` indicates the project was approved.


### Notes on the Essay Data

<ul>
Prior to May 17, 2016, the prompts for the essays were as follows:
<li>__project_essay_1:__ "Introduce us to your classroom"</li>
<li>__project_essay_2:__ "Tell us more about your students"</li>
<li>__project_essay_3:__ "Describe how your students will use the materials you're requesting"</li>
<li>__project_essay_3:__ "Close by sharing why your project will make a difference"</li>
</ul>


<ul>
Starting on May 17, 2016, the number of essays was reduced from 4 to 2, and the prompts for the first 2 essays were changed to the following:<br>
<li>__project_essay_1:__ "Describe your students: What makes your students special? Specific details about their background, your neighborhood, and your school are all helpful."</li>
<li>__project_essay_2:__ "About your project: How will these materials make a difference in your students' learning and improve their school lives?"</li>
<br>

Proposals also include resources requested. Each project may include multiple requested resources. Each row in resources.csv corresponds to a resource, so multiple rows may tie to the same project by id.

</br>

<li>id - unique id of the project application; joins with test.csv. and train.csv on id </li>

<li>description - description of the resource requested </li>
<li>quantity - quantity fo resource requested </li>
<li>price - price of resource requested </l>

# Code activity
1. Create minimum data points required, not entire data was used so as to maintain focus on algorithm setup rather than redundant problem-solving, selective data utilization was prioritized. The primary objective is to enhance understanding and proficiency in the field. Users can adjust data volume as needed.
2. Split data for ramdomsearchcv or gridsearchcv, suggesting not to split into X_train, X_cv, X_test as these methods use k-fold cross-validation.
Clarified the need to split data into training, cross-validation, and test sets when using for loops to tune the model.
3. Emphasized the importance of exploring the stratify parameter while splitting the data.
4. Applied Multinomial Naive Bayes on specific feature sets, including essay, categorical features (teacher_prefix, project_grade_category, school_state, clean_categories, clean_subcategories), and numerical features (price, teacher_number_of_previously_posted_projects).
5. Conducted hyperparameter tuning to find the best alpha (smoothing parameter) by considering a range of alpha values and exploring the class_prior parameter.
6. Utilized k-fold cross-validation for hyperparameter tuning and plotted the performance of the model on both training and cross-validation data for each hyperparameter.
7. Trained the model with the best hyperparameters found and evaluated its performance on test data by calculating the AUC and plotting the ROC curve.
8. Printed the confusion matrix with predicted and original labels of test data points and plotted it in heatmaps.
9. Identified the top 20 features from either feature Set 1 or feature Set 2 using the feature_log_prob_ parameter of MultinomialNB and printed both positive and negative corresponding feature names.
10. Summarized the results at the end of the notebook in a table format.