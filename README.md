# Decision Making Machine Learning model to Assisst Judges
This project was completed under the course Introduction to Machine Learning(CSE574) in University at Buffalo

**Team Members**
 * Nikhil Arora
 * Jacquelyn Dufresne
 * Mridula Rao

**Problem Setup**

In 2016 the independent non-profit news organization ProPublica released a report evaluating Northpointe’s COMPAS system, which is an algorithm widely used across the country for considerations in pretrial detention and sentence determination.
  * [Propublica Story](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing)
  * [Northpointe's Response](https://www.documentcloud.org/documents/2998391-ProPublica-Commentary-Final-070616.html)

COMPAS evaluates criminals on over 100 factors and outputs a risk score which indicates how likely it is that someone will recidivate (go on to commit another crime in the future). These scores are then taken into consideration by judges when assigning sentences, determining bail/parole eligibility, etc. Critically, race is not one of the factors used in by COMPAS.
ProPublica reviewed the output of COMPAS on a dataset of over 7000 individuals from Broward County, Florida. They found that the algorithm correctly predicted recidivism at similar rates for both white (59%) and black defendants (63%). However, when the algorithm was incorrect it tended to skew very differently for each of these groups. White defendants who re-offended within two years were mistakenly labelled low-risk almost twice as often as their black counterparts. Additionally, black defendants who did not recidivate were rated as high-risk at twice the rate of comparable white defendants.
Northpointe submitted a rebuttal of ProPublica’s evaluation, claiming that PP misrepresented certain statistical values. They assert that their model is entirely fair across racial lines when base rate recidivism levels are taken into account.
On the heels of these reports our group has been given a task to release a new system as a potential candidate for replacing COMPAS. We will be working as a part of NGO so we would have to justify all the measures we take in detail. 3 machine learning models have been designed by your development team and trained on the Broward County data. These include:
  * A linear support vector regressor
  * A feed forward neural network
  * A naïve Bayes classifier

In addition, team has been scanning machine learning research papers and have determined 5 potential post-processing methods that enforce various constraints in attempts to reflect different measures of fairness. These include:
  * Maximum profit / maximum accuracy
  * Single threshold
  * Predictive parity
  * Demographic parity
  * Equal Opportunity

**Models and Data**

There are 3 machine learning models: **a linear support vector regressor (Compas_SVM.py), a feed-forward neural network (Compas_NN.py), and a naïve Bayes classifier (Compas_Naive_Bayes.py)**. Each of these models has a single function which loads the data, builds and runs the model, and outputs a set of predictions alongside the rest of the useful data needed for evaluation. The data consists of 4 files: **Compas_train_data.npy, Compas_train_labels.npy, Compas_test_data.npy, and Compas_test_labels.npy**, all of which are contained within **Broward_Data.zip**. All files should be extracted/downloaded into the same directory for them to run properly.
Running one of the model files will load the data, classify the data, separate all relevant predictions and labels into groups based on race, and call the report_results function from **Report_Results.py**. This function calls each of the 5 post-processing methods and prints out some useful metrics that can be used to determine if your functions are working correctly. Additionally, there is **utils.py**, a collection of functions used to gather various metrics from the classified data.

**PostProcessing**

Each function in postproceesing takes categorical_results as an input. This is a dictionary - the keys are the 5 different racial groups, and the entry for each key is a list of (prediction, label) tuples for all people within that racial group.
Some functions also take epsilon as an additional parameter, which acts as a tolerance for enforcing some of the fairness constraints. **NOTE: The listed epsilon values must be consistently upheld for the SVM and Naïve Bayes Classifier. The neural network may occasionally fail or provide trivial solutions using these values.**
While COMPAS gives a recidivist rating of 1-10, with additional labels of low, medium, and high risk, the models this project all output a list of real-valued predictions between [0, 1]. The postprocessing methods determines threshold values for these predictions; anything above the value will be a 1, and anything below the value will be a 0. This gives a final result of a list of binary decisions. Some functions give different threshold values for each racial group.
These functions return the two things: the classified data which has been thresholded to meet the requirements of the function, and the thresholds themselves. The output data is in the same form as the input data. The thresholds is also a dictionary with racial groups as the keys, but the entries are the scalar threshold value for that racial group.
Definitions of necessary terms and a few basic pros/cons of each method are provided in the supplementary handout, **Machine_Learning_Fairness_Primer.pdf.**

For the detailed findings and outcome that our team has found, you can read our [Final Report](574_7_report.pdf)
