# Piracy Probabilities

---

### Table of Contents

1. [Problem Statement](#Problem-Statement)
2. [Background](#Background)
3. [Preprocessing & Modeling](#Preprocessing-and-Modeling)
4. [Conclusion and Recommendations](#Conclusion-and-Recommendations)
5. [Datasets](#Datasets)

---

### Problem Statement
Identify causal societal and developmental factors related to piracy. Using these factors we aim to create an effective model to prove that these factors are strong determinants of high piracy activity looking at attacks from 2010 onwards. 

---

### Background
When we think of maritime piracy, it can often conjure up thoughts of wooden ships and eye patches, but it is still a problem that plagues us today. It is important to understand the societal and economic factors of piracy to redress causes of piracy and create a safer and more equitable world. The pirate attack data was obtained from the NATIONAL GEOSPATIAL-INTELLIGENCE AGENCY. This data set included over 7,000 observations of reported pirate attacks that ranged from 1978 to the present. Other data regarding economic, education, sea law adoption,  research and development was sourced from the United Nations Sustainable Development Goals data repository.

---

**Data Dictionary for Anti-Shipping_Activity_Messages.csv**

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**X**|*float*|Anti-Shipping Piracy Messages|Longitude|
|**Y**|*float*|Anti-Shipping Piracy Messages|Latitude|
|**OBJECTID**|*int*|Anti-Shipping Piracy Messages|Attack observation ID|
|**reference**|*object*|Anti-Shipping Piracy Messages|Attack reference number|
|**dateofocc**|*object*|Anti-Shipping Piracy Messages|Date of occurence|
|**subreg**|*int*|Anti-Shipping Piracy Messages|Subregion|
|**hostility_d**|*object*|Anti-Shipping Piracy Messages|Description of attack type|
|**victim_d**|*object*|Anti-Shipping Piracy Messages|Description of victim|
|**description**|*object*|Anti-Shipping Piracy Messages|Detailed description of attack by person reporting the incident|
|**hostilitytype_l**|*float*|Anti-Shipping Piracy Messages|Attack type broken out by category|
|**victim_l**|*float*|Anti-Shipping Piracy Messages|Victim type broken out by category|
|**navarea**|*object*|Anti-Shipping Piracy Messages|Navigation Area|

**Software Requirements**
1. Numpy - Complex math
2. Pandas - Data frames
3. Geopy - Used to feature engineer based off of coordinates
4. Seaborn - Visual Plots
5. Matplotlib - Visual Plots
6. Folium - Generate maps 
7. IPython - Display image files
8. Warnings - Prevent warning messages
9. Sklearn - Modeling


### Preprocessing and Modeling
We were able to pull over 7,000 observations of reported pirate attacks that ranged from 1978-present. Our project was more concerned with the effects of modern piracy, and as regions, economic factors and technologies experience a great deal of change over the that time period, we decided to look only at the attacks from 2010 to the present day.  This left us with approximately 3,5000 observations, which was more than enough for our purposes.

By far, cleaning the data was the most time consuming portion of this project. The biggest issue we had was joining the different data sets which required the featuring of the country column based on coordinate values. We accomplished this using the Nominatim module from a python package called GeoPy. Nominatim’s usage policy restricted us to a maximum of 1 request per second which, given the initial size of the data, was very time consuming.  Attack observations were linked to our other data sets by associated countries or, if too far from the coastline, were labeled as International Waters.

Few countries had SDG information records every single year. Data from a previous year was used when possible. If no country data was available for the 20 length of SDG, a value at the bottom of the range of worldwide data.

3 classification models were used: Logistic Regression, K-Nearest Neighbors, Random Forest. A baseline score was established. Then we leveraged GridSearchCV to identify the best scores and parameters possible for our models. 

|Model                               |R2 Traing Score   |R2 Testing Score  |Accuracy      |
|---                                 |---               |---               |---           |
|Logistic Regression                 |0.784             |0.717             |0.78 +- 0.10  |
|KNN                                 |0.997             |0.980             |0.96 +_ 0.04  |
|Random Forest                       |0.997             |0.980             |0.95 +- 0.09  |
|KNN w/o Location Features           |0.973             |0.849             |0.90 +_ 0.09  |
|Random Forest w/o Location Features |0.973             |0.879             |0.93 +- 0.10  |

---

### Conclusion and Recommendations
Most pirate attacks are happening in equatorial countries. Attacks tend to cluster in geographical choke points. Land-based lookout patrols points in these vulnerable areas are effective. Most attacks occur in regions that have a higher poverty rate, thus compounding problems in already troubled regions.  Piracy activity has steadily decreased over the past decade. Cargo ships and tankers are at a higher risk. We recommend increased security on board for vulnerable types of vessels and adoption of oceanic treaties to help curb piracy.

Interventions targeting poverty are likely to be effective. However, due to the low cost and effectiveness, convincing member states to adopt the United Nations Convention on the Law of the Sea and other oceanic treaties may represent the highest return on effort. A successful, multi-front strategy may include offering economic development support in exchange for ratifying oceanic treaties.

---

### Executive Summary
[Executive_summary]('./Executive%20summary.pdf')

---

### Datasets
* [Anti-Shipping_Activity_Messages.csv](#'/datasets/Anti-Shipping_Activity_Messages.csv')
* [esri_w_country_columns.csv]('datasets/esri_w_country_columns.csv') 
* [cleaned_pirate_activity_eda.csv]('datasets/cleaned_pirate_activity_eda.csv')  
* [modeling.csv]('datasets/modeling.csv') 

---
