 
<img src="https://img.shields.io/badge/-Python-blue?style=for-the-badge&logo=python&logoColor=white" alt="PYTHON" /> [<img src="https://img.shields.io/github/contributors/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="CONTRIBUTORS" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/graphs/contributors) [<img src="https://img.shields.io/github/stars/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="STARS" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/stargazers) [<img src="https://img.shields.io/github/forks/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="FORKS" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/network/members) [<img src="https://img.shields.io/github/issues/Mariem-Ben-Salah/Demo-Automation?style=for-the-badge" alt="ISSUES" />](https://github.com/Mariem-Ben-Salah/Demo-Automation/issues)

# I. Introduction

## 1. 🌳 Decision-Tree RecommendationSystem 🌳

This project is aimed at developing an image recommendation system based on user preferences, using Decision Trees as the main machine learning model. The project was completed as a part of a Data Mining course and implemented in Python.

## 2. 📂 Repository Structure

* `project_report` : The final report of the project.
* `project.ipynb`: contains the whole code for the project.

## 3. 📝 Requirements

The packages required to run this project are mentioned in the `project.ipynb` file.

# II. What you need to know

The code for this project is divided into three main parts: preprocessing, training and prediction.

## 1. Preprocessing

The preprocessing part contains functions for collection, cleaning and preprocessing the required data.

### 🐱 🐶 🐵 Data Collection 

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

### 🧹 Data Filtering

After Preprocessing the dataset, we filtered the relevant information by dropping duplicates in the csv file (using *.drop_duplicate()) and removing ".xml" files that were irrelevant for our case (we made sure to include only the *.jpg* files in our _for_ loop)

## 2. Training

The training phase uses the cleaned data to train the machine learning models. It contains functions for transforming and labeling the data.

### 🔄 Data Transformation 

The Transformation part consisted of extracting more useful information from the training set. In order to do that, we had to :

1. Convert the filtered csv file to a json
2. Create a data frame from the loaded json information
3. Choose the informations that we want to extract : we decided ended up choosing `the animal's size inside the image` and `the dominating colors in the picture`. 

`Animal's size inside the image

For that, we created two new columns in the dataframe :

■ tailleX = xmax - xmin.

■ tailleY = ymax - ymin.

This processing gave us a lot of distinct values, and we realized that they would be difficult to manage with label encoding. Therefore, we found it judicious to divide the *tailleX* and *tailleY* sizes into 3 categories:

■ Object size less than 30% of the image size: small ⇒ value 0 assigned.

■ Object size between 30% and 70% of the image size: medium ⇒ value 1 assigned.

■ Object size greater than 70% of the image size: large ⇒ value 2 assigned.

`Dominant Colors`

For that, we performed clustering algorithms :

■ Mini Batch K-means, with 3 clusters.

--> we imported conversion functions from webcolors, mainly css3_hex_to_names and hex_to_rgb.

This processing resulted on creating a *couleur1* column where we stored the dominant color for every image in the training set.

![colour column](https://i.ibb.co/hD4fF9D/Screenshot-2023-05-02-at-12-04-03.png)

*Likes*

the `likes` column was generated, which contains the value "favorite" (1) or "not favorite" (0), randomly assigned to simulate user preferences. A user preference profile was then built.

![Likes column](https://i.ibb.co/ZN52BQ6/Screenshot-2023-05-02-at-12-03-53.png)

At the end of these steps, the dataframe contained the following columns : 

![dataframe after the added columns](https://i.ibb.co/xhyQ5d5/Screenshot-2023-05-02-at-12-04-20.png)


### 🔍 Labeling and Annotation: 

Before continuing our analysis, we annotated our data using the LabelEncoder imported from sklearn.preprocessing. 
``` python
le1 = LabelEncoder()
dataframe["width"] = le1.fit_transform(dataframe["width"])
```

These lines of code create a LabelEncoder object called le1 and applies it to the "width" column of the dataframe object.

A LabelEncoder is a class from the sklearn.preprocessing module that can transform categorical data (i.e. text data) into numerical data that machine learning algorithms can work with. It does this by assigning a unique integer value to each unique category in the data.

In this specific case, the "width" column likely contains text data (e.g. "small", "medium", "large"), so le1.fit_transform() is being used to transform this data into numerical values. The fit_transform() method first fits the encoder to the data (i.e. learns the unique categories in the data) and then transforms the data into numerical values using the learned categories. The resulting transformed data is then assigned back to the "width" column in the original dataframe object.

The same process was done for the other columns in the dataframe.

### 📈 Data Analysis: 

To simulate a user who has chosen their favorite images, we generated a "likes" column containing either "favorite" or "not favorite," which we later inserted into our resultframe. This column was created by randomly generating an integer 0 or 1. If the integer is equal to 1, then we add "favorite" to the column and vice versa.

### 📊 Data Visualization: 

We tried to visualize the most relevant information. To do this, we implemented:

➔ A plot.bar to visualize the 2 properties "width" and "height"

➔ A plot.bar to visualize the 2 properties "tailleX" and "tailleY"

➔ A plot.bar to visualize the most frequently occurring dominant color

![results of the plot.bar](https://i.ibb.co/Jn3YqXT/Screenshot-2023-05-02-at-12-05-35.png)

➔ In this example, the user tends to like images with medium width and medium height.

➔ The user tends to like objects that are medium-sized in width (tailleX) as well as objects that are either medium-sized or too tall in height (tailleY).

➔ The user likes images with the dominant color code 12.


## 🎉 3. Testing

This final step aims to fulfill the initial objective of this project, which is to recommend to users images that they will appreciate, based on the processing already done and especially on their preferences. To do this, we decided to work with decision trees.

Indeed, decision trees are a non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules deduced from the data characteristics.

In our case, decision trees learn from the data to approximate the set of data to propose to a user. The deeper the tree, the more complex the decision rules are, and the more adapted the model is.

Why did we choose to work with this method ?
- It is easy to understand and interpret. Trees can be visualized.
- It requires little data preparation. Other techniques often require data normalization, dummy variables creation, and empty values removal.
- It can handle multi-output problems.

Implementation of this method in the project

We first imported DecisionTreeClassifier with these two lines:
``` python
from sklearn import tree
Xxx = tree.DecisionTreeClassifier()
```
Then, we applied this classifier to our data with `xxxx = xxxx.fit()`


Overall, this project demonstrates the effectiveness of decision trees as a tool for building recommendation systems, as well as the importance of careful feature selection and data preprocessing for achieving accurate predictions.


## 👤 Author

- Mariem Ben Salah 
