![](https://github.com/ashiwoku/QSAR-model/blob/main/qsar%20flowchart.png)

# Building a QSAR MOdel to predict molecule's ability to inhibit the target protein linked to Alheimer's, Beta_Secratese 1
### By Abolaji Shiwoku 

## Background 
  Drug discovery is a long process associated with high costs, on average taking 12 years and $10 billion dollars. The old process relied on a scientist or pharmaceutical companies’ expertise
or past knowledge of experiments to predict chemical compounds that may or may not exhibit the desired inhibition on their target protein. Now with decades of past
experimental data, we can apply machine learning to build predictive models that can predict a compound's biological activity to help speed up the selection of valid drug candidates. 
These tools can be supremely beneficial in reducing experimental costs and speed up clinical research to bring more helpful drugs to those afflicted. Pharmaceutical companies are
realizing the power of using past experiment data to better predict the compound’s chemical characteristics. As powerful machine learning tools are applied to chemical data, we 
can use these models for monitoring important chemical- protein activities, especially as advances are made to manufacturing novel compounds. 

  A QSAR (quantitative-structured activity relationship) model helps researchers predict whether a given chemical compound's potential activity on a target protein. If a 
researcher is studying the effects of inhibition of a disease causing target protein, they can use past experimental compounds to train a model to predict the biological activity 
of an unseen compound. This model will use the derived features of over 9000 compounds previously tested for their ability to inhibit the target protein, Beta Secretase 1, which is 
measured by pIC50. The descriptors, 1-D and 2-D descriptors that describe the molecules' physical composition, will be derived using 3rd party software, PaDEL and will be modeled 
in 2 separate ways: a model to predict whether a compound will be active (inhibits protein) or inactive (displays no significant effect on a protein), as well as a regression 
model that would predict the actual pIC50 value of the supplied compound.


## Method
  This machine learning application starts off with over 9000 chemical compounds that have been tested to inhibit the Beta Secretase 1 protein from the Chembl database. It is
important whenever one uses wants to derive conclusions of significance on a dataset, we use valid observations to train our model. In this instance, we must make sure that the 
compounds we use for training meet requirements for viable drug candidates. To ensure this, we use the **Lipinski Rule of 5**:

* Molecular mass less than 500 Daltons
* No more than 5 hydrogen bond donors
* No more than 10 hydrogen bond acceptors 
* Log P (Octagonal water partition coefficient) is no greater than 5 

When it comes to feature engineering, or descriptors that modeled physical attributes of the molecules, we used the PaDel descriptor software to construct a library of molecular descriptors. The library was quite large, so a feature selection process was used to choose the final subset of descriptors:

* Remove descriptors that have a low variance threshold (less than 15%)
* Remove descriptors that show strong collinearity with other descriptors (will help with overfitting)
* Utilize backward elimination to choose the best subset of features that minimize overfitting in the model 

After the feature selection process, a slight correction was needed for the classification model: **removal of chemical compounds that where neither active or inactive**. This will make the classification task easier on the model, as the model will need only to predict the 2 classes. Numerically this was represented as 1 (active) or 0(inactive). 

## Model Building and Performance
  After obtaining our model ready data, it was time to find the best model for both datasets: the classification and regression model. For reach model type, 4 models were compared: for regression, we used MLR (Multiple Linear Regression), Polynomial Regression, Support vector Regression, and a deep neural network; for classification, the models 
used were support vector machine, Logistic Regression, deep neural network, and Random Forest. During the training for these models, we made sure to withhold a portion of the 
data to validate model results. We also used SMOTE analysis to generate samples of the minority class to improve predictability of the minority class. For regression, making 
sure that all features are scaled to fit a standard normal distribution was very important for achieving optimal model performance, and was achieved by using sklearn's 
*StandardScaler* tool. After running the models, their results were as followed: 

| Classification Model | Precision (Majority) | Recall (Majority) | Precision (Minority) | Recall (Minority) |
| -------------------- |        :----:       |      :----:       |          :----:      |       :----:      |
| Logistic Regression  |       0.87         |       0.96         |     0.39             |         0.16      |
| Support Vector Machine |        0.94      |     0.92           |       0.58           |         0.65       |
| **Random Forest**         |      **0.95**          |        **0.96**       |         **0.78**          |         **0.7**        |
| Deep Neural Network   |         0.91        |       0.97         |       0.71           |       0.41          |


| Regression Model | Mean Absolute Error     | Root Mean Squared error | 
| ---------------- |          :----:         |        :----:           |       
| Multiple Linear Regression  |       0.781       |              0.986           |                  
| Polynomial Regression |       0.926           |            64.276              |                  
| **Support Vector Regression**    |     **0.608**      |       **0.821**        |               
| Deep Neural Network   |        0.845            |        1.225                 |        

## Conclusion
  As you can see the models that performed the best don't rely on a linear relationship. This could be a sign that further experimentation with the features may be required to achieve a more model ready data set, but due to this non-linear relationship, random forest is a perfect application for this form of data.
The random forest is a powerful algorithm that makes it easy to achieve favorable 
predictability in most cases with limited optimization required. They fit well to the training data, but like the support vector regression model chosen, they are "black box" 
algorithms: they don't allow researchers to see how the model adjusts as the training data changes. Due to this fact, further improvement of the feature selection may allow for 
better fit with less powerful algorithms such as multiple linear regression models. These models allow for us to better monitor how the model changes as the training data is further updated.           


## Further Improvements 
  Making improvements for the feature engineering process, such as analyzing the class of descriptors rather than individual descriptors which may improve the interpretation of 
the model. During the data collection, only one public database, ChemBl, was looked at. There are several databases that contain biological activity data, and they can be 
searched to build our training model. The more data the model is trained on, the better chances that all aspects of the chemical space is accounted for, and the model will not suffer when encountering novel compunds.The ultimate goal for an application such as this is for the scientific community to be able to use this model to inform their research into this target protein, so a future update will be to host this model within a web application so that researchers can apply this to their research. This project utilized descriptors that described the structural components of the compounds. Future improvements may perform experiments that utilize descriptors that describe the electro-magnetic nature of the compounds. These descriptors fall into the class of descriptors labeled 3D descriptors

## Credit & Contact 
  This model was inspired by a youtube series led by Dr. Chanin Nantasenamat, Ph.D. A link to his channel is [here](https://www.youtube.com/c/DataProfessor/featured)
  
  I would love to hear feedback from anyone who discovers this project to learn on other improvements I could make or if you have questions on my though process. Please forward 
  your thoughts to my email:  **abolajishiwoku@yahoo.com**
