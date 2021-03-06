What Kind of Person Goes to the Doctor:
========================================================
How the population represented in the Electronic Health Records database compares to the general U.S. population
------------------------------------------
<img src="http://i.imgur.com/SuPi8.jpg" width="100" align="left">

By [Yasmin Lucero][yasmin]
prepared for Kaggle competition: [Practice Fusion Analyze This! 2012---Open Challenge][Kaggle]
September 10, 2012



Practice Fusion has released a rich database of de-identified medical records from medical practices that participate in their Electronic Health Record (EHR) system. We would like to use this access to rich and abundant medical data to learn something new, or at least interesting. The first inferential step is puttting the EHR patient population into the context of the general population. What sort of people are these EHR patients?  

The EHR database includes a handful of hooks that we can use to understand the demographics of this population: year of birth, gender, smoking status, weight, BMI and state of residence. Here, I pull in various data from the census bureau and center for disease control (CDC) and compare the EHR population demographics to the general population demographics.

* [Overview](#overview)
* [Geographic Representativeness](#geographic)
* [Age Distribution](#age)
* [Diabetes and Obesity](#diabetes)
* [Smoking](#smoking)
* [Medical Utilization](#MU)
* [Sources](#sources)

### <a id="overview">Overview</a>
How well does the EHR population represent the general population? A quick summary tells us that EHR patients are more female, more diabetic, more obese and less likely to smoke than the general population.
![plot of chunk figOverview](figure/figOverview.png) 


### <a id="geographic">Geographic Representativeness</a>
First, I have made a plot of proportion of the EHR patient population in each state vs the proportion of the U.S. population in each state. The state of California is both the largest state and is strongly over-represented in the EHR patient population. As a result, most other states are under-represented by comparison. 
![Figure 1.](figs/figsSep5/figPop2.png)
Here is a map where the color shows the difference between the proportion of the poulation in the EHR popualtion minus the proportion in the general population---i.e. the distance between the two dots in the above plot. I have excluded Alaska and Hawaii here, but you can see above that both states are slightly under-represented in the EHR dataset. There are no patients from Rhode Island. 
![Figure 1.](figs/figsSep5/figMap.png)

### <a id="age">Age Distribution</a>
The EHR is generally older than the general population. This is partly because it excludes minors. The next two figures show a comparison of the age distributions of the EHR patient population versus the U.S. population in 2011, as estimated by the [U.S. Census][censusPops]. 

One major reason the EHR population is older on average is because it excludes minors. However, the distribution for those above 18 shows a marked hump around 58, while the U.S. population is quite flat until it starts to drop-off around 60. For those about 58 and older, the EHR population is probably pretty similar to the general population. But those between the ages of 18 and 55 are fairly under-represented here. 
![Figure 1.](figs/figsSep5/figAgeDist1.png)
![Figure 1.](figs/figsSep5/figAgeDist2.png)
If you really squint at the right side of the cumulative distribution plot, you will see that the inflection point for the drop-off in the age distribution comes a little younger in the general population than in the EHR population, which hardly shows any inflection at all. This suggests that the very oldest demographics are ever so slightly over-represented in the EHR population. Please note that I excluded the data for the 85+ category, to aid visualization. 

### <a id="diabetes">Diabetes and Obesity</a>
The EHR population is more overweight than the general population. Here is a state by state comparison of the rates of obesity for the EHR population and the general population. For reference, I have added the one to one line. Those states above the one to one line have higher rates of obesity in the EHR population than the general population, and vice-versa for those populations below the line.
![Figure 1.](figs/figsSep5/figObese.png)

The EHR population is more likely to be diabetic and more likely to be obese than the general population. In the first figure, I show the rate of diabetes in the EHR population versus the rate in the general population for each state.  

California has a slightly lower than average rate of diabetes, but this is not enough to pull the overall EHR population towards the national rate. EHR patients are more likely to be diabetic than average. 
![Figure 1.](figs/figsSep5/figdiabetes.png)
Now, let's get a look at the connection between diabetes and obesity in the EHR population. Here, we are comparing the distribution of BMI's for diabetics and non-diabetics broken out by age and gender.  
![Figure 1.](figs/figsSep5/figBMIb.png)
We see that the diabetics do have a higher BMI than the non-diabetics on average. The difference is starkest for the youngest demographic, while the older populations show more similar distributions of BMI between the two diabetics and non-diabetics. But keep in mind, diabetes is rare in the young and the boxplots for the younger demographic are based on relatively few patients.  

The next figure show the BMI distributions as a function of age bin and diabetes status. There are a number of things to notice here. 1) There are many more non-diabetics than diabetics. 2) The diabetic population is much older. 3) Almost no-one is in the "healthy" range for BMI. 4) Among non-diabetics, the BMI distribution shifts towards the right as the subpopulation ages, i.e. people gain weight as they get older. This shift is less obvious in the diabetic population. The young diabetics are just as overweight as the old diabetics, if not more so on average. 
![Figure 1.](figs/figsSep5/figAgeb.png)

Despite the link between obesity and diabetes, only about half of the diabetics in the EHR population are obese (BMI>30). Also, the majority of obese patients in the EHR data are not diabetic. Here we have a plot of the number of EHR patients above a given BMI level who are obese. Even in the EHR population, most overweight and obese patients are not diabetic. 
![Figure 1.](figs/figsSep5/figCumSum2.png)
This holds true even for the most obese patients. Here is a zoom in on the right tail of the plot for those with a BMi above 40, i.e. the severely obese or class 3 obesity. 
![Figure 1.](figs/figsSep5/figCumSum3.png)
And just for good measure, here is the proportion of diabetics at a given BMI level. There is a clear trend that starts to increase above a BMI of about 24. At the extreme low and high BMI values, there is only a small number of patients and so there is more noise around the mean trend. For the thinnest patients, the rate of diabetes is about 10%, and then it appears that the rate of diabetes tops out at about 35%, but there are individual BMI bins with higher rates. 
![Figure 1.](figs/figsSep5/figPropdiabetic.png)

Here, we have a plot of weight over time. Each line belongs to an individual patient. To aid visualizaiton, I am only showing patients that gained or lost at least 75 pounds. The color indicates how large the weight change is, so the biggest losers and gainers are in rich purple. 
![Figure 2.](figs/figsSep5/figDiabeticWeight.png)
You can see that there are a number of patients who have lost really significant amounts of weight. Also, while in the non-diabetic population we have a fairly even mix of losers and gainers, in the diabetic population most of the significant weight change is losses. This suggests that diabetes is a sufficiently serious diagnosis as to inspire weight loss, or at least weight control, in the patients. 
### <a id="smoking">Smoking</a>
The EHR population smokes less than that general population. There are at least two ways the EHR population under-represents smokers: First, there are more women than men in the EHR population and women smoke less. Second, California is over-represented in this population, and California also has one of the lowest rates of smoking in the country. Still, a state by state comparison broken out by Gender shows that even after accounting for state and gender, the EHR population still smokes less than the general population. 
![Figure 2.](figs/figsSep5/figSmokes.png)
I think the low rate of smoking may be evidence of a socioeconomic status of the population. People with low socioeconomic status smoke more and go to the [doctor less][doctorvisitsSES]. Here is a plot of smoking rate versus education level, a decent proxy for socioeconomic status. (The data for smoking by education level also comes from the Census.) The EHR population smokes like people who graduated from college. 
![Figure 2.](figs/figsSep5/figSmokeEdu.png)
### <a id="MU">Medical Utilization</a>
Smokers are an unhealthy group. In the EHR, they have more diagnoses, go to the doctor more often, and are taking more medications. 
![Figure 2.](figs/figsSep5/figSmokeMU.png)
Here is a word cloud for the Physicians that smokers see, excluding general/family practice or internal medicine. 
![Figure 2.](figs/figsSep5/figSmokeDocs.png)
Based on the doctors that smokers visit, we can assume that the EHR smokers are pursuing treatment for these common complications due to smoking: heart conditions, food problems and nerve damage.

Diabetes is also a pretty serious diagnosis. The EHR diabetics do not necessarily have more diagnoses, but they do go to the doctor more often and are taking more medications than non-diabetics.  
![Figure 2.](figs/figsSep5/figDiabeticMU.png)
Here is a word cloud of the physician specialists seen by Diabetics. I have excluded General Practice, Family Practice and Internal Medicine, who make up overwhelming the majority of doctor visits for diabetics and nondiabetics alike. 
![Figure 2.](figs/figsSep5/figDiabetesDocs.png)
We see that in addition to endocrinologists, the diabetics in the EHR population are seeing specialists for all of the major complications of diabetes: cardiovascular disease, kidney issues (nephrology), and foot problems (podiatry).
### Summary
The EHR population is biased towards middle-aged people carrying substantially more excess weight than their doctor would prefer. There are slightly more women than men, but the bias is measurable without being dramatic. The population has some regional bias towards the larger states, and a lot of bias towards California. There are quite a lot more diabetics in the EHR population than the general population, even after you account for age, weight and gender. The EHR population doesn't smoke much, which could be a clue about their socioeconomic status: they smoke at about the rate of college of graduates. 

### <a id="dataprep">Miscellaneous Data Preparation Notes and Issues</a>
1. Age: EHR includes year of birth, which I converted to age by subtracting from 2012. In a few cases, age was calculated as the difference between visit year and year of birth.
2. Some data for minors was included in data set. If you subtract YearOfBirth from VisitYear (excluding records where VisitYear=0) you find 819 records for minors. The youngest individual being 15 years old. This is presumably why there are records from Pediatricians in the dataset.
3. I removed all records for weight, height and BMI with unreasonable values. This means height measure above 9 feet tall or less than 3 feet tall, weight measure above 600 pounds or below 80 pounds.  
4. I removed approximately 35 records from Puerto Rico.

### <a id="sources">Sources</a>
1. [Kaggle and Practice Fusion][kaggle] provided the main dataset of de-identified electronic health records. This data makes up our information abou the EHR population. 
2. Data for [obesity by state][cdcObese] ultimate source: U.S. National Center for Health Statistics.
3. [The population of states][censusPops] was derived from census 2010. (U.S. Census Bureau, Population Division.)
4. Kaiser Health Facts provided a summary of the rate of [diabetes][kaiserDiabetes] by state. Ultimate source is BRFSS.
5. Smoking rate by state is derived from U.S. [census data][InfochimpSmoke], prepared by Infochimps.
6. Wikipedia gives the [BMI thresholds][BMIthreshold] from the World Health Organizaiton (WHO).
7. Study show, lower socioeconomic status means going to the [doctor less][doctorvisitsSES].

[kaiserDiabetes]: http://www.statehealthfacts.org/comparemaptable.jsp?ind=70&cat=2 "Title"
[kaiserSmokelaws]: http://www.statehealthfacts.org/comparemaptable.jsp?ind=931&cat=2
[InfochimpSmoke]: http://www.infochimps.com/datasets/current-cigarette-smoking-by-sex-and-state-2005
[censusPops]: http://www.census.gov/popest/data/datasets.html
[cdcObese]: http://www.cdc.gov/mmwr/preview/mmwrhtml/mm59e0…
[BMIthreshold]: http://en.wikipedia.org/wiki/Body_mass_index
[doctorvisitsSES]:http://www.rwjf.org/pr/product.jsp?id=54208
[kaggle]: https://www.kaggle.com/c/pf2012-at
[yasmin]: https://sites.google.com/site/yasminlucero/
