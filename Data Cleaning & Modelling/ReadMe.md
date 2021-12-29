# Data Cleaning and Modelling
## Background Information
You have been given a set of data sets, all containing different columns and values, as well as a data model. A data model shows the relationships between all of the data sets, as well as any links that you can use to merge tables.

It is your job to use these data sets as well as the data model, to create your own data set that you can use to fulfill the requirements of this task. 

This task is essential because it is one of the specific requirements that the client has asked for, so we are relying on the data analyst to work with the data and create accurate, reliable insights that can be backed up during the final presentation.

## Task
1. Requirements gathering

To complete this task, you’ll first want to look at the task that you’ve been assigned and think about which available data sets may be useful to fulfill the requirements. It may be helpful for you to write the data sets down that you think will be best for the task. You should take time to fully understand the data model and how the tables link together. Then you should think about which tables are most relevant.

2. Data cleaning

Before we begin to work with the relevant data sets, we’ll need to ensure that the data is clean and ready for analysis. Data cleaning is a common and very important task when working with data. This includes removing columns that have a high number of missing values, removing rows that have values which are erroneous, changing the data type of some values within a column and also removing columns which are not relevant to this task. Your end result should be a set of relevant data sets that are clean with each data set containing only the columns which are relevant to the completion of this task.

Think about how each column that you choose can be used to fulfill the requirements of this task. If you can’t think of why a column may be useful, it may not be worth including it. It may be helpful to write down which columns you think would be important to keep. 

3. Data modeling

Finally, use this knowledge to create a final data set containing all of the columns that you will need to complete the task. You can use Excel or any other tool of your choice to create your final data set. Based on which columns you think will be most useful, you may be required to merge tables together by using the Unique Keys within tables. You should spend some time modeling the data to create your final data set for this task.

All of the data sets will be provided as CSV files and you can do the data modeling in Excel or any other tool that you wish. Your final submission should be a single CSV or Excel spreadsheet containing the columns and data that you think will fulfill the requirements of this task best.

### Resources for your task

* [Data Set - Content](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790270/Data.Set.-.Content.csv/ "Data Set - Content title")

* [Data Set - Location](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790274/Data.Set.-.Location.csv/ "Data Set - Location title")

* [Data Set - Profile](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790286/Data.Set.-.Profile.csv/ "Data Set - Profile title")

* [Data Set - Reactions](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790287/Data.Set.-.Reactions.csv/ "Data Set - Reactions title")

* [Data Set - ReactionTypes](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790288/Data.Set.-.ReactionTypes.csv/ "Data Set - ReactionTypes")

* [Data Set - Session](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790290/Data.Set.-.Session.csv/ "Data Set - Session")

* [Data Set - User](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790291/Data.Set.-.User.csv/ "Data Set - User")

## 🚀 Solution
### Understand each Data Set
#### Entity Relationship Diagram
<p align = "center">
  <img width="450" alt="Acc Capture" src="https://user-images.githubusercontent.com/94797745/147696574-30d43838-fa4b-44e4-94dc-12d601ff1040.PNG">

**User**
* ID: Unique ID of the user (automatically generated)
* Name: Full name of user
* Email: Email address of user
  
**Profile**
* User ID: Unique ID of a user that exists in the User table
* Interests: Interests of the associated user
* Age: Age of the associated user
  
**Location**
* User ID: Unique ID of a user that exists in the User table
* Address: Full address of the user

**Session**
* User ID: Unique ID of a user that exists in the User table
* Device: Mobile device that they used for this session on the application
* Duration: Amount of time in minutes that this user stayed active on the application during this session

**Content**
* ID: Unique ID of the content that was uploaded (automatically generated)
* User ID: Unique ID of a user that exists in the User table
* Type: A string detailing the type of content that was uploaded
* Category: A string detailing the category that this content is relevant to
* URL: Link to the location where this content is stored

**Reaction**
* Content ID: Unique ID of a piece of content that was uploaded
* User ID: Unique ID of a user that exists in the User table who reacted to this piece of content
* Type: A string detailing the type of reaction this user gave
* Datetime: The date and time of this reaction

**ReactionTypes**
* Type: A string detailing the type of reaction this user gave
* Sentiment: A string detailing whether this type of reaction is considered as positive, negative or neutral
* Score: This is a number calculated by Social Buzz that quantifies how “popular” each reaction is. A reaction type with a higher score should be considered as a more popular reaction.
  
# Merging the Data Sets to form the model dataset
The model dataset after merging relevant tables is provided in [this file](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790412/Social.Buzz.Data.Set.xlsx/ "this file title")
  
This dataset combined the following columns from the following data sets:
* **Profile**
    * Interests: Interests of the associated user
    * Age: Age of the associated user
* **Location**
    * Address: Full address of the user
* **Session**
    * Duration: Amount of time in minutes that this user stayed active on the application during this session
* **Content**
    * ID: Unique ID of the content that was uploaded (automatically generated)
    * Type: A string detailing the type of content that was uploaded
    * Category: A string detailing the category that this content is relevant to
  
* **Reaction**
    * Type: A string detailing the type of reaction this user gave
  
* **ReactionTypes**
    * Sentiment: A string detailing whether this type of reaction is considered as positive, negative or neutral
    * Score: This is a number calculated by Social Buzz that quantifies how “popular” each reaction is. A reaction type with a higher score should be considered as a more popular reaction.
 
The [Client Brief](https://github.com/WuraAderele/Accenture-Data-Analytics-Virtual-Experience/files/7790223/Data_Analytics.Client.Brief.pdf/ "Client Brief title") states that the client wanted to see “An analysis of their content categories showing the top 5 categories with the largest aggregate popularity”.
This meant that the client wants to know which categories of their content had yielded the greatest popularity out of all their content. 
According to the data model, Popularity is quantified by the “Score” given to each reaction type, as a numeric value. Therefore each reaction gives a weighting to how popular a piece of content may become.
To find the categories with the greatest popularity, the data analyst must sum up which content categories have the largest aggregate Score.

To create the model dataset, we used the User table as the base table. I merged the respective tables together using “left” join in Power Query and merging on the corresponding columns for each data set. 
To finally calculate the top 5 categories with respect to popularity,we use a Pivot Table in Excel to group these transactions by Category, sum the Score for each Category, and sort the data by Score in descending order and take the top 5.
