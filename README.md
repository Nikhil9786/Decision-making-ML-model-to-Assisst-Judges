# Decision Making Machine Learning model to Assisst Judges
This project was completed under the course Introduction to Machine Learning(CSE574) in University at Buffalo

**Problem Setup**

In 2016 the independent non-profit news organization ProPublica released a report evaluating Northpointe’s COMPAS system, which is an algorithm widely used across the country for considerations in pretrial detention and sentence determination.
  * [Propublica Story](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing)
  * [Northpointe's Response](https://www.documentcloud.org/documents/2998391-ProPublica -Commentary-Final-070616.html)

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
