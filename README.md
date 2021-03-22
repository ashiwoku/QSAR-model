![](https://github.com/ashiwoku/QSAR-model/blob/main/qsar%20flowchart.png)

# Building a QSAR MOdel to predict molecule's ability to inhibit the target protein linked to Alheimer's, Beta_Secratese 1
### By Abolaji Shiwoku 

## Background 
  Drug discovery is a long process with high costs, on average taking 12 years and $10 billion dollars. The old process relied on a scientist or pharmaceutical companies expertise
or past knowledge of experiments to design chemical compounds that may or may not exhibit the desired characteristics on thier target gene or protein. Now with decades of past
expermimental data, we can apply machine learning to build predictive models that can predict a compound's biological activity to help speed up the selection of the drug targets. 
These tools can be supremely benefiecial in reducing reserach costs and speeding up clinical reserach to bring more helpful drugs to those afflicted. Pharmacuitical companies are
realising the power of using past experiment data to to better predict the compund's chemical characteristics. As powerful machine learning tools are applied to chemical data, we 
can use these models for onitoring important chemical- protein activities, especially as advances are made to manufacturing novel compounds. 

  A QSAR (quantitaive-structured activity relationship) model helps researhcers predict whether a given chemical compound's potentila activity on a target protein. If a 
reseracrher is studying the effects of inhibition of a disease causing target protein, they can use past experimental compunds to train a model to predict the biological activity 
of a unseen compund. This model will use the derived features of over 9000 compunds preciously tested for thier ability to inhibit the target protein, Beta Secratese 1, which is 
measured by pIC50. The descriptors, 1-D and 2-D descriptors that desribe the molecules' physical composition, will be drived using 3rd party software, PaDEL and will be modeled 
in 2 seperate ways: a model to predict whether a compound will be active (inhibits protein) or inactive (displays no significant effect on a protein), as well as a regression 
model that would predict the actual pIC50 value of the supplied compound. 

## Method
  This machine learning application starts off with over 9000 chemical compounds that have been tested to inhibit the Beta Secratese 1 protein from the Chembl database. It is
important whenver one uses wants to derive conclusions of significance on a dataset, we use valid observations to train our model. In this instance, we must make sure that the 
compounds we use for training meet requirements for viable drug candidiates. To ensure this, we use the **Lipinksi Rule of 5**:

* Moleculr mass less than 500 daltons
* No more than 5 hydrogen bond donors
* No more than 10 hydrogen bond acceptors 
* Log P (Octogonal water partition coeffecient) is no greater than 5 

When it comes to feature engineering, or descriptors that modeled physical attrivutes of the molecules, we used the PaDel descriptor software to construct a library of molecular descriptors. The library was quite large a feature selection process wa used to choose the final subset of descriptors:

* Remove descriptors that have a low variance threshold (less than 15%)
* Remove desciptors that show strong collinearity with other descriptors (will help with overfitting)
* Utilize backward elimnination to choose the best subset of features that minimize overfitting in the model 

After the feature selection process, a slight correction was needed for the classification model: **removal of chemical compounds that where neither active or inactive**. This will make the clssification task easier on the model, as the model will need only to predict the 2 classes.

## Model Building and Performance
  After obtaining our model ready data, it was time to find the best model for both datasets: the classification and regresion model. For reach model type, 4 models were compared: for regression, we used MLR (Multiple Linear Regresion), Polynomial Regression, Support vector Regression, and a deep neural network; for classification, the models 
used were support vector machine, Logistic Regression, deep neural network, and Random Forest. During the training for these models, we made sure to withhold a portion of the 
data to validate model results. We also used SMOTE analysis to generate samples of the minority class to improve predictability of the minority class. For regression, making 
sure that all features are scaled to fit a standard normal distribution was very importan for achieving opptimal model performance. adnwas achieved by using sklearn's 
*StandardScaler*. After running the models, thier results were as follows: 

| Classification Model | Precison (Majority) | Recall (Majority) | Precision (Minority) | Recall (Minority) |
| -------------------- |        :----:       |      :----:       |          :----:      |       :----:      |
| Logistic Regression  |       0.87         |       0.96         |     0.39             |         0.16      |
| Support Vector Machine |        0.94      |     0.92           |       0.58           |         0.65       |
| **Random Forest**         |      **0.95**          |        **0.96**       |         **0.78**          |         **0.7**        |
| Deep Neural Netwrok   |         0.91        |       0.97         |       0.71           |       0.41          |


| Regression Model | Mean Absolute Error     | Root Mean Sqaured error | 
| ---------------- |          :----:         |        :----:           |       
| Multiple Linear Regression  |       0.781       |              0.986           |                  
| Polynomial Regression |       0.926           |            64.276              |                  
| **Support Vector Regression**    |     **0.608**      |       **0.821**        |               
| Deep Neural Netwrok   |        0.845            |        1.225                 |                     

## Conclusion
  As you can see the models that perfomed the best don't rely on a linear relationship. The random forest is a powerful algorithm that makes it easy to achieve favorbale 
preditatbility in most cases with limited optimization required. They fit well to the training data, but like the support vector regression model chosen, they are "black box" 
algorithms: they don't allow researchers to see how the model adjusts as the training data changes. Due to this fact, further improvement of the feature selection may allow for 
better fit with less powerful algorithms such as multiple linear regression models. These models allow for us to better monitor how the model changes as the training data is further updated. 

## Further Improvements 
  Making improvements for the feature engineering process, such as analyzing the class of descriptors rather than individual descriptors which may improve the explanability of 
the model. During the data collection, only one public database, ChemBl, was looked at. There are several databases that contain biological activity data, and they can be 
searched to build our training model. Even including compunds that will increase compunds of the inactive class will be helpful in improving perfomance. The ultimate goal for an 
application such as this is for the scientific commmunity to be able to use this model, so a future update will be to host this model within a web application so that 
researchers can apply this to thier research. This project utilised descriptors that descriped the stuctural components of the compunds. Future improvements may perform 
experiments that utilise descriptors that describe the electro-magnetic nature of the compounds. These descriptors fall into the class of descriptors labeled 3D descriptors. 

## Credit & Contact 
  This model was inspired by a youtube series led by Dr. Chanin Nantasenamat, Ph.D. A link to his channel is [here](https://www.youtube.com/c/DataProfessor/featured)
  
  I would love to hear feedback from anyone who discovers this project to learn on other improvements I could make or if you have questions on my though process. Please forward 
  your thoughts to my email:  **abolajishiwoku@yahoo.com**
