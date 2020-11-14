# Predicting Protester Violence

___

This project was a collaborative effort between Adrian Chapman, Jennifer Hofer, Sonali Bhatia, and Steve Hydzik.

All data was originally gathered from the [Mass Mobilization Data Project](https://massmobilization.github.io/).

### Problem Statement
We wanted to understand the components that were most likely to lead to protestors becoming violent in a demonstration. We would give this information to local government officials so they could be better prepared to minimize violence in future protests.

### Methodology:
Methods were chosen to maximize inferential ability rather than predictive power.  TFIDF vectorizer was used to understand the text features that differentiated violent vs nonviolent protests.  Ada-boost classifier was used to predict protester violence, and feature important scores were extracted to determine the variables most predictive of violence.

### EDA:

With initial data exploration, there were a few observations that stood out.

Countries with the most protests:
    1. United Kingdom
    2. France
    3. Ireland

Countries with the most violence on both sides of protests:
    1. Bangladesh
    2. South Korea
    3. France

![](https://git.generalassemb.ly/adrianchap/project_5/blob/master/figs/uk_bangladesh.png)

Digging deeper into the top countries for each of these scenarios, we can really see how the state response differs in Bangladesh compared to the UK and other countries with large protest numbers. The main state response for the UK is to ignore, whereas Bangladesh’s main response is crowd dispersal. A method the Mass Mobilisation Project describes as:
	“Any attempt to move the protesters from their location and break up the protest… Examples might include the use of tear gas, issuing warnings, moving troops into positions and pushing protesters off their positions.”


Protests with the most Protester Violence (on average):
    1. Police Brutality
    2. Tax Policy
    3. Land - Farm Issue

Average Participants (on average):
    - With Protester Violence: 14,505.36
    - Without Protester Violence: 22,138.14

### Data Preprocessing 

For our preprocessing, we took the following initial steps:

    - Creation of Start date and End Date from existing Start day , Start month , Start Year , End date , End month and End Year fields to create  features for calculating protest duration.
    - Preprocessing for Notes column using Lemmatizer and TfiDFVectorizer to create dataframe with features from text.
    - Participants column was cleaned to change it to all numeric data. There were many discrepancies in the initial data, so they were standardized. All NaN values to 50 (the minimum number of people to be a protest), chose the higher number in a range, and if the number was 100’s, 1000’s etc. they were changed to 300, and 3000 respectively.

### Modeling:
 Modeling with text and Numeric features 
Modeling for text and numeric data using ensemble model Adaboost combined with DecisionTreeClassifier for target variable protesterviolence, which gave below results.
    | Train Score : 0.86 | Test Score : 0.83 |
    | Specificity : 0.92 | Sensitivity : 0.60 |
Model for text and numeric data using SVM to check  if we get better results. 
	SVM model resulted with :
Train Score : 0.94  Test Score : 0.83 
Which is a overfit model with 
Specificity : 0.89  Sensitivity : 0.67
##### Modeling without text

Though the text descriptions were useful in describing violent and non-violent protests, we were interested to see what numeric and categorical features were most predictive of protester violence without a natural language description of the event. 

Ada boost classifier was chosen for its predictive and explanatory power, with its ability to produce feature importance scores. The best model after grid search produced a train score of 85.6% and a test score of 81.1%


### Results:

Feature importance scores from the Ada Boost model without text revealed key insights that could be useful to governments in planning for non-violent protests.  Several state-controlled variables proved to be predictive features in modeling, including the State Responses: crowd dispersal, ignore, and arrests.  Participant number, duration, and the number of protests were also predictive.  

![](https://git.generalassemb.ly/adrianchap/project_5/blob/master/figs/feature_importance.png)

Correlation with the protester violence variable revealed a strong positive correlation between state sponsored violence, such as crowd dispersal, arrests, and killings.  While there is no way to show causation here, and it remains clear whether protester violence begets state violence or the other way around, it is important to note that the strongest negative correlation with protester violence was the state strategy to ignore the protests.  This means that simply ignoring a protest significantly reduces the chance of there being violence in a demonstration.  Europe also had a negative correlation coefficient with protester violence, making Europe a potentially useful model for understanding state strategies to ensure non-violent protests. 



### Recommendations:
What this project has highlighted the most, is that violence brings violence. Because the state violence and protester violence are so heavily correlated (and because we cannot tell who incites violence each time) all options for a non violent response should be taken first.
For government police forces preparing, they should also pay attention to the type of protest happening:
    - Protests are more likely to happen on the 1st or the 15th of the month.
    - Larger protests tend to be less violent.
    - Protests regarding police brutality tend to be the most volatile.
By preparing in advance, and having an understanding of the situation they are walking into, police forces have more of an opportunity to minimize the violence happening globally.



