# Tanzania Water Point Classification

The purpose of this project is to take data provided by the Tanzania goverment about numerous water source points in the country and create a classifier that categorize new waterpoint data into three categories which are -

**'functional'** - waterpoint is operational

**'non functional'** - waterpoint is not operational and needs repair 

**'functional needs repair'** - waterpoint is operational but needs maintainence repair

### Repository Files
The following are folders and files you can find in this repository and their discription

1. content

        1.training_set_labels      - The dataset target

        2.training_set_values      - The dataset features

        3.test_set_values          - The features for prediction

        4.column_descriptions.txt  -  Discription of the features

    
 2. images            - images used in this README.md


 3. README.md         - discription of the project and repository


 4. presentation.pdf  - pdf of a powerpoint presentation meant for non-technical audience


### Process
For this project I followed OSEMN framework of-

1. Obtain the data

2. Scrub the data

3. Explore the data

4. Model the data

5. iNterpret the data


## Method
For this project I took an iterative process of trying out six diffrent classifier models which were

1. Logistic Regression
2. K-Nearest Neighbour
3. Decision Tree Classifier
4. Random Forest Classifier
5. eXtreme Gradient Boosting (XGBoost)
6. Support Vector Machines (SVM)

I also made use of GridSearchCV from sklearn to search out the best values for the parameters. For the metrics comparison, I mainly paid attention to accuracy and F1-score. Below is a graph of model scores and table.

![model_scores_table](images/model_scores_table.PNG)


![model_scores](images/model_scores.PNG)

The accuracy and F1 scores for Random Forest and XGBoost are extremely similar with a slight edge to XGBoost but I chose to go with Random Forest as my final model. The reason for this is because Random Forest had slightly better recall score for the 'funtional needs repair' category which I believe is more important than the precision score for our purpose. 

Another model that I also considered is Logistic Regression since it had a much better recall score for 'functional needs repair' category. Since the purpose of this project is help identify water points that need to be repair having a high recall score for the the 'non functional' and 'functional needs repair' categories allows us to do that. High recall score means we be able to identify more of the category but the downside is there will also be more false positive, which in our case means identifying functional water points as needing repair.

Ultimately I chose to priotize the accuracy and F1 score over the recall score since having a lot of false positive would waste manpower and budget for the Tanzanian goverment.




![confusion_matrix_randomforest](images/confusion_matrix_randomforest.PNG)

![Classification_report_rf](images/Classification_report_rf.PNG)

The accuracy score for the test data drop to 0.74 from 0.88 of the training data. The F1- score for the three categories is much lower for the testing dataset than the training dataset, especially for the 'functional needs repair' category. This is a category that all six classifier struggles with. The reason for this might be because of class imbalance problem. I used SMOTE to fixed the class imbalance but other methods might prove to be more effective.

### Interpreting the Model


To interpret the model I took a look at the top 20 most important features for our model. A lot of the features seems to be correct judging intuitively.

The second most important feature is shown to be the altitude of the well. It seems that the average altitude of nonfunctional waterpoints are lower than the functional ones.  It could be possible that the reason for this is because rural area in Tanzania are located at lower altitudes. Therefore, its not the altitude that is directly affecting the condition of the water point.

The quantity_dry, quantity_insufficient, and quantity_enough features are dummy variables are obvious why they are important. A dry well or one without insufficient water would obviously be classifed as non functional.

Whether the waterpoint has a permit or not is also important in classifying the condition. 

Several waterpoint types and some extraction types also seems to be important in determining the condition. Perhaps the types that falls under some of these categories are not durable and should be avoided in the future.

A few District and regions are also included in the top twenty features. This warrants a closer inspection to see which districts have more nonfunctional water points and the reason why this might be.


![features_importance](images/features_importance.PNG)


### Improvements To Make

- Since using GridSearchCV take up a lot of computational time, I couldn't put in more parameters like I wanted. Searching out more parameters might improve the model performance.

- The model ability to predict functional needs repair is still lacking. I could try scrubbing the data in a diffrent way to make the model better.

- Try out diffrent types of filling missing values to see if it improve the model.

- Try using a diffrent method of fixing class imbalance to see if it improve our model performance for the 'functional needs repair' category.
