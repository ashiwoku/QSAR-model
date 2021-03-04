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
measured by pIC50. The descriptors, 1-D and 2-D descriptors that desribe the molecules' physical composition, will be drived using 3rd party software, PaDEL and will be modeled in 
2 seperate ways: a model to predict whether a compound will be active (inhibits protein) or inactive (displays no significant effect on a protein), as well as a regression model 
that would predict the actual pIC50 value of the supplied compound. 

## Method
  This machine learning application 
