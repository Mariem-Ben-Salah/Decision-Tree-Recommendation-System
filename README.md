 
<img src="https://img.shields.io/badge/-Python-blue?style=for-the-badge&logo=python&logoColor=white" alt="PYTHON" /> [<img src="https://img.shields.io/github/contributors/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="CONTRIBUTORS" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/graphs/contributors) [<img src="https://img.shields.io/github/stars/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="STARS" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/stargazers) [<img src="https://img.shields.io/github/forks/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="FORKS" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/network/members) [<img src="https://img.shields.io/github/issues/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="ISSUES" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/issues)

# Table of contents

- [Introduction](#Decision-Tree-Recommendation-System)
- [Repository Structure](#Repository Structure)
- [Requirements](#Requirements)
- [Preprocessing](#Preprocessing)
- [Data Collection](#Data Collection)
- [Data Filtering](#Data Filtering)
- [Data Transformation](#Data Transformation)
- [Labeling and Annotation](#Labeling and Annotation)


🌳 # Decision-Tree-Recommendation-System 🌳

This project is aimed at developing an image recommendation system based on user preferences, using Decision Trees as the main machine learning model. The project was completed as a part of a Data Mining course and implemented in Python.

📂 # Repository Structure

* `project_report` : The final report of the project.
* `project.ipynb`: contains the whole code for the project.

📝 # Requirements

The packages required to run this project are mentioned in the `project.ipynb` file.

The code for this project is divided into three main parts: preprocessing, training and prediction.

# 1. Preprocessing

The preprocessing part contains functions for collection, cleaning and preprocessing the required data.

## - 🐱 🐶 🐵 Data Collection 

The project uses Kaggle, an open-licensed image platform, as the source of the dataset. The main criteria for selecting the dataset was finding relevant metadata stored in a separate CSV file along with the pictures. After careful consideration, we chose a collection of cat, dog, and monkey pictures.

The dataset is divided into two main folders : 
- Train : contains the 1309 images used for the training phase
- Test : contains the images used for the testing phase

After the cleaning, we remained with 469 rows and 8 columns in the csv file :

```
- filename 
- Width 
- Height
- Class : cat, dog, monkey
- xmin
- ymin
- xmax
- ymax
```
## -  🧹 Data Filtering

After Preprocessing the dataset, we filtered the relevant information by dropping duplicates in the csv file (using *.drop_duplicate()) and removing ".xml" files that were irrelevant for our goal (we made sure to include only the *.jpg* files in our _for_ loop)

# 2. Training

The training phase uses the cleaned data to train the machine learning models. It contains functions for transforming and labeling the data.

# 🔄 Data Transformation 

The Transformation part consisted of extracting more useful information from the training set. In order to do that, we had to :
1. Convert the filtered csv file to a json
2. Create a data frame from the loaded json information
3. Choose the informations that we want to extract : we decided ended up choosing `the animal's size inside the image` and `the dominating colors in the picture`. 

*Animal's size inside the image*
For that, we created two new columns in the dataframe :
■ tailleX = xmax - xmin.
■ tailleY = ymax - ymin.

This 

*Dominant Colors*
For that, we performed clustering algorithms :
■ Mini Batch K-means, with 3 clusters.
--> we imported conversion functions from webcolors, mainly css3_hex_to_names and hex_to_rgb.

*Likes*
the `likes` column was generated, which contains the value "favorite" (1) or "not favorite" (0), randomly assigned to simulate user preferences. A user preference profile was then built.

🔍 # Labeling and Annotation: 
The labeling part was mainly regarding the first transformation we did (the size of the animal). In fact, we compared both the height and the weight of the animal with the weigth and height of the picture and if :
```
■ Object size < 30% image size then height/weight = small ⇒ 0.
■ 70% image size > Object size > 30% image size then height/weight = medium ⇒ 1.
■ Object size > 70% image size then height/weight = large ⇒2.
```

The column "couleur1" was created to storage the dominant color in every picture

At the end of this step, the dataframe contained the following columns :  width | height | class | tailleX | tailleY | couleur1 |

📈 # Data Analysis: 

A "likes" column was generated to simulate user preferences, and the team built a user-preference profile.

📊 # Data Visualization: The team used bar plots to visualize relevant information like image size, object size, and dominant color.

🤖💡🔍🌳 #  Recommendation System: The main objective of the project was to build a recommendation system based on user preferences. The team used Decision Trees as the main machine learning model for classification and regression.

Overall, the project was successful in building an image recommendation system that could recommend images based on user preferences.
## 🤖 Introduction

The demo is a process that typically occurs once a month. During this meeting, team members and product owners showcase what they've been working on during the previous period. Despite its simplicity, this process can sometimes take up a significant amount of time on the agenda, which is why we have decided to automate it.


In this project, a recommendation system was implemented using a decision tree. The decision tree is a non-parametric supervised learning method used for classification and regression tasks. The goal is to create a model that can predict the value of a target variable by considering the rules of simple decisions derived from the given characteristics. The deeper the tree, the more complex the decision-making rules, and the better the model.






Overall, this project demonstrates the effectiveness of decision trees as a tool for building recommendation systems, as well as the importance of careful feature selection and data preprocessing for achieving accurate predictions.


## 👤 Author

- Mariem Ben Salah 
