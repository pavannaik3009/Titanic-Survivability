# Titanic: Machine learning from the disaster
The sinking of the Titanic is one of the most infamous shipwrecks in history.

On April 15, 1912, during her maiden voyage, the widely considered “unsinkable” RMS Titanic sank after colliding with an iceberg. Unfortunately, there weren’t enough lifeboats for everyone onboard, resulting in the death of 1502 out of 2224 passengers and crew.

While there was some element of luck involved in surviving, it seems some groups of people were more likely to survive than others.

#### Data 
Using the Titanic dataset from [this](https://www.kaggle.com/c/titanic/overview) Kaggle competition.

This dataset contains information about 891 people who were on board the ship when departed on April 15th, 1912. As noted in the description on Kaggle's website, some people aboard the ship were more likely to survive the wreck than others. There were not enough lifeboats for everybody so women, children, and the upper-class were prioritized. Using the information about these 891 passengers, try to build a model to predict which people would survive based on the following fields:

- **Name** (str) - Name of the passenger
- **Pclass** (int) - Ticket class
- **Sex** (str) - Sex of the passenger
- **Age** (float) - Age in years
- **SibSp** (int) - Number of siblings and spouses aboard
- **Parch** (int) - Number of parents and children aboard
- **Ticket** (str) - Ticket number
- **Fare** (float) - Passenger fare
- **Cabin** (str) - Cabin number
- **Embarked** (str) - Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)

## EDA: Exploratory Data Analysis
Tool: Python(numpy, pandas, matpotlib.pyplot, seaborn)

Objective: Finding reasons and trends for which people were more likely to survive the wreck than others.
 
#### Plot continuous features

Histogram for people who survived or did not survive based on their Age
<img width="500" alt="Screen Shot 2019-11-13 at 4 39 48 PM" src="https://user-images.githubusercontent.com/43712046/68810623-40982400-0634-11ea-806f-7f9c1d85216e.png">

Histogram for people who survived or did not survive based on the fare price they paid
<img width="500" alt="Screen Shot 2019-11-13 at 4 40 27 PM" src="https://user-images.githubusercontent.com/43712046/68810641-4f7ed680-0634-11ea-9bfa-ba3ab6dbbc7f.png">

Categorical plot ofpeople who survived based on the ticket class
<img width="500" alt="Screen Shot 2019-11-13 at 4 44 18 PM" src="https://user-images.githubusercontent.com/43712046/68810877-f2cfeb80-0634-11ea-80fe-0372e3bba2d0.png">

**It can be clearly seen that people with ticket class 1 were more likely to survive than 2 or 3**

Combining the SibSp and Parch and, plotting a Catplot of people who survived based on the Family Count
<img width="500" alt="Screen Shot 2019-11-13 at 4 49 14 PM" src="https://user-images.githubusercontent.com/43712046/68811138-873a4e00-0635-11ea-8773-189b305f019a.png">

**It can be incurred that the lesser the family size the more likely to survive**

#### Plot categorical features

<img width="275" alt="Screen Shot 2019-11-13 at 4 55 54 PM" src="https://user-images.githubusercontent.com/43712046/68811515-7807d000-0636-11ea-8641-e38746cc83aa.png"><img width="275" alt="Screen Shot 2019-11-13 at 4 56 20 PM" src="https://user-images.githubusercontent.com/43712046/68811537-85bd5580-0636-11ea-9f90-296cd5bc448a.png"><img width="275" alt="Screen Shot 2019-11-13 at 4 56 45 PM" src="https://user-images.githubusercontent.com/43712046/68811572-95d53500-0636-11ea-9a05-5d4e52c87abb.png">

**Female and people with cabins(probably with better class ticket) are more likely to suvive.**

The EDA notebook can be found [here](https://github.com/pavannaik3009/Titanic/blob/master/EDA.ipynb)

## Data Cleaning

Data cleansing or data cleaning is the process of detecting and correcting (or removing) corrupt or inaccurate records from a record set, table, or database and refers to identifying incomplete, incorrect, inaccurate or irrelevant parts of the data and then replacing, modifying, or deleting the dirty or coarse data.

PassengerID and Name are irrelevant and can be dropped.

### Continuous Features
A naive approach for missing values is to substitute the missing values with the average of the values. 
Age has 177 missing values and we can use fillna() from the pandas library and fill the missing values of the age by calculating the average Age of people. 

SibSp and Parch individually do not give meaningful insights and also, are related to the size of a family. Thus, we can combine these two features to get the Family count. Thus, dropping the SibSp and Parch feature.

### Categorical features

Converting the sex(categorical) to numeric by using dictionary.

Using np.where() we can convert Cabin with Nan values to numeric as where() acts as a if condition (if number present:1, else:0)

The notebook for Data cleaning of Continuous variables can be found [here](https://github.com/pavannaik3009/Titanic/blob/master/DataCleaningCont.ipynb)

The notebook for Data cleaning of Categorical variables can be found [here](https://github.com/pavannaik3009/Titanic/blob/master/DataCleaningCat.ipynb)

## Splitting Data
Tool: Python(Scikitlearn, Pandas)

Training dataset: To learn the general pattern

Validation set: To select the best model (Optimal algorithm and hyperparameter settings)

Tesing set: Data for unbiased evaluation

<img width="896" alt="Screen Shot 2019-11-13 at 5 38 15 PM" src="https://user-images.githubusercontent.com/43712046/68813755-6de8d000-063c-11ea-8a66-cb58787d3ad9.png">

I have divided the dataset into 60%, 20%, 20% for training, validation and test.
The notebook can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/DataSplit.ipynb)

## k-fold cross-validation 

**Cross Validation** is a very useful technique for assessing the performance of machine learning models. It helps in knowing how the machine learning model would generalize to an independent data set. k-fold cross-validation randomly divides the data into k blocks of roughly equal size. Each of the blocks is left out in turn and the other k-1 blocks are used to train the model.

## Model

### Logistic Regression
**Regression** is a process for estimating the relationships among variables (often to make a prediction about some outcome). **Logistic Regression** is used to build a model with Binary target. I n this case the target is to 'survived' and the model fits data to predict a person survived or not. 

#### Hyperparameters

**C** is a regularization parameter in Logistic regression that controls how closely the model fits to the trianing data. If c tends to infinity then, it is a low regularization with high complexity and the model is more likely to overfit. Whereas if C tends to zero the it is a high regularization with low complexity and the model is more likely to underfit. 

Therefore, tuning this hyperparameter we get the best model with **C** = 1 with an accuracy of **79.8%**.

<img width="307" alt="Screen Shot 2019-11-18 at 1 27 48 PM" src="https://user-images.githubusercontent.com/43712046/69083191-406aa080-0a07-11ea-9d7e-c0b528823079.png">

The notebook for Logistic regression can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/LogReg.ipynb)

### Support Vector Machine

**SVM** is a classifier that finds an optimal hyperplane that maximizes the margin between two classes. 

**Goal:** Maximize the length of the support vector (the perpendicular line from the decision boundary to the closest points in both classes).

#### Hyperparameters

**C** is a regularization parameter. As C tends to infinity, it is a low regularization with large penalty for misclassification in training. If C tends to zero, it is a high regularization with small penalty for misclassification in training. 

**Kernel trick/Kernel method** is a process that transforms data that is not linearly seperable in n-dimensional space to a higher dimension where it is linearly seperable. 

Therefore, tuning these SVM hyperparameters we get the best model with **C** = 0.1 and **linear** kernel with an accuracy of **79.6%**.

<img width="452" alt="Screen Shot 2019-11-18 at 1 39 17 PM" src="https://user-images.githubusercontent.com/43712046/69083995-e2d75380-0a08-11ea-93ae-b1d6f066cf61.png">

The notebook for SVM can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/SVM.ipynb)

### Multi-layer perceptron

**Multi-layer perceptron** is a classic feed forward Artificial Neural Network. It is a connected series of node (in the form of DAG) where each node represents a function or a model.

<img width="1240" alt="Screen Shot 2019-11-17 at 6 22 46 PM" src="https://user-images.githubusercontent.com/43712046/69084175-482b4480-0a09-11ea-924f-ddb6a18f3801.png">

#### Hyperparameters

**Activation Function** facilitates the type of non-linearity (sigmoid, tanH, ReLU) introduced in the model. 

**Hidden layer size** facilitates how many hidden layers and how many nodes in each layer is used to fit. 

**Learning Rate** facilitates how quickly and whether or not the algorithm will find the optimal solution.

Therefore, tuning these MLP hyperparameters we get the best model with tanH activation function, learning rate of 100, and a learning rate of invscaling with an accuracy of **80.9%**. 

<img width="937" alt="Screen Shot 2019-11-18 at 1 42 12 PM" src="https://user-images.githubusercontent.com/43712046/69084179-4c576200-0a09-11ea-98bb-dbcabdc7794a.png">

The notebook for MLP can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/MLP.ipynb)

### Random Forest Classifier

**Random Forest** is a ensemble method that merges a collection of independent decision trees to get a more accurate and stable prediction. 

#### Hyperparameters

**maximum depth** controls how deep each individual tree can go.

**n estimator** controls how many individual trees will be built. 

Therefore, tuning these RF hyperparameters we get the best model with **max depth** of 8 and 5 **estimators** with an accuracy of **83.1%**. 

<img width="560" alt="Screen Shot 2019-11-18 at 3 34 25 PM" src="https://user-images.githubusercontent.com/43712046/69102988-bd0e7680-0a29-11ea-8c5f-2e0603f58f43.png">

The notebook for Random Forest Classification can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/RandomForest.ipynb)

### Gradient Boosted Trees (Boosting)

**Boosting** is an ensemble method that aggregates a number of weak models to create one strong model. Boosting iteratively builds weak models where each model learns from the mistakes of the previous models.

#### Hyperparameters

**n estimators** controls how many individual trees will be built. 

**maximum depth** controls how deep each individual tree can go.

**Learning Rate** facilitates how quickly and whether or not the algorithm will find the optimal solution.

Therefore, tuning these GB hyperparameters we get the best model with a **learning rate** of 0.01, **max depth** of 3 and 500 **estimators** with an accuracy of **84.1%**. 
<img width="712" alt="Screen Shot 2019-11-18 at 4 30 35 PM" src="https://user-images.githubusercontent.com/43712046/69103308-ae748f00-0a2a-11ea-9a8f-2a4eb61afe95.png">

The notebook for Gradient Boosted Trees can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/GradientBoosting.ipynb)

## Best Model (Validation)

The best model of the different algorithms built can be tested on the validation test and the accuracy, precision, recall score and the latency can be used to determine the best model based on our requirement.

<img width="674" alt="Screen Shot 2019-11-18 at 5 37 00 PM" src="https://user-images.githubusercontent.com/43712046/69103586-699d2800-0a2b-11ea-8c42-ed38c29979b1.png">

Thus, from the above results it can be concurred that Gradient Boosting has a good accuracy and precision with very less latency and hence can be used for testing. 

## Testing

On implementing Gradient boosting on the titanic test set with a **learning rate** of 0.01, **max depth** of 3 and 500 **estimators** we get an accuracy of **81.5%** with **80.8%** precision. 

The jupyter notebook for validation and testing can be found [here.](https://github.com/pavannaik3009/Titanic/blob/master/Final.ipynb)
## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
