# Analyzing Carbon Dynamics following Fires in Longleaf & Slash Pine Stands of the Apalachicola National Forest

## Introduction
The purpose of this script to to use advanced Python packages to create a dataframe from multiple geospatial raster layers. 
The dataframe was then be used for data visualization and regression analysis. The aim of this analysis is to see how
fire severity impacts net ecosystem productivity and aboveground biomass following fire disturbances.

The raster layers come from the 'Forest Carbon Stocks and Fluxes After Disturbance, Southeastern USA, 1990-2010' dataset available 
through the Oak Ridge National Laboratory. Specifically, the purpose of this script to create a dataframe from 8 raster layers 
inclduing: Aboveground Biomass (Kg C m-2) at 1990, 2000, and 2010; Net Ecosystem Productivity (g C m-2) at 1990, 2000, and 2010; 
Forest Type; and Year of Fire Disturbance.

The raster layer were preprocessed using TerrSet prior to using them in this script. All layers have a have an AlbersUS83 projection
and have a 30m resolution.

## Methods
### Data Preprocessing
**Figure 1.** is a screenshot of the dataframe I created through Pandas. This dataframe consists of 189,220 observations and 14 columns (not all pictured here). Each observation is a burned pixel. The columns used for the final analysis are the Date and Age of the fires, Forest Type, Burn Severity, Aboveground Biomass at 2010, and Net Ecosystem Productivity at 2010. Burn Severity was assigned based on a pixel's decrease in Aboveground Biomass before and after a fire. Specifically, I classified pixels as "Severe" burns if they lost over 70% of their aboveground biomass after a fire. Pixels which lost between 30-70% of their aboveground biomass were labeled as "Moderate". Much fewer pixels lost less than 30% of their aboveground biomass. Therefore, I removed them from this study.

![FL_Data_Screenshot](https://user-images.githubusercontent.com/54719919/84538971-9dd67f80-acc0-11ea-8d72-a9695f375f3d.png)

### Data Visualization
**Figure 2.** shows the frequency of moderately and severely burned pixels by year of fire disturbance. Notice there are no observations for the years 2002 & 2003. Overall, there is a higher frequency of burned pixels in 2008 & 2009. This indicates the was either an increase in fire frequency or an increase in the total area of Longleaf and Slash Pine fires in the years closest to 2010. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/54719919/84794197-f4470500-afc3-11ea-9447-609435a40471.png">
</p>

**Figure 3.** displays a scatterplot of Aboveground Biomass and Net Ecosystem Productivity at 2010. This was done to explore potential multicollinearity. Based on this chart, total aboveground biomass and net ecosystem productivity are not highly correlated because net ecosystem productivity can vary greatly at one value of aboveground biomass, especially for young burn scars. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/54719919/84538629-f9ecd400-acbf-11ea-9b05-47327d0c5541.png">
</p>

**Figures 4a. and 4b.** are scatterplots showing the Aboveground Biomass in 2010 for different-aged burn scars. Figure 4a shows the Aboveground Biomass at 2010 for every observation, while Figure 4b. shows the mean Aboveground Biomass at 2010 for moderately and severely burned pixels at every year. The mean was chosen for Figure 2b, as opposed to the median, because many pixels had repeating values if they were a part of the same burn scar and the mean was more sensitive to the range of aboveground biomass values across fires. For both moderate and high-severity burns, the aboveground biomass increases as the burn scar ages.

   **4a.**

<p align="center">
  <img src="https://user-images.githubusercontent.com/54719919/84539151-e42bde80-acc0-11ea-8c91-6b51d7c6ff2e.png">
</p>

   **4b.**

<p align="center">
  <img src="https://user-images.githubusercontent.com/54719919/84539159-e857fc00-acc0-11ea-86e0-2519fe9f1313.png">
</p>

**Figures 5a. and 5b.** are scatterplots showing the Net Ecosystem Productivity at 2010 for the different-aged burn scars. The moderately burned pixels and the severely burned pixels show slightly different trends. For moderate severity burns, the range of net ecosystem productivity values is narrower and the mean remains more consistent for every year following a burn compared to severe burns. For the severe burns, the range and mean of NEP values per pixel varies more, especifcally for younger burn scars. In Figure 4b, one can see that the mean NEP is negative for the first two years following a severe burn, meaning the stand becomes a carbon source during this time.

  **5a.**

<p align="center">
  <img src="https://user-images.githubusercontent.com/54719919/84539296-23f2c600-acc1-11ea-9b2a-5ae87d8a2c99.png">
</p>

  **5b.**

<p align="center">
  <img src="https://user-images.githubusercontent.com/54719919/84539280-1e957b80-acc1-11ea-8487-c63688ec1fa0.png">
</p>

### Regression Results

**Aboveground Biomass**

Below are the results of the linear and polynomial (quadratic) regressions used to model the relationship between aboveground biomass and burn scar age. For moderate burns, the linear and non-linear regressions have R-square values of .74 and .74 respectively. This mean both explain over 74% of the variance of aboveground biomass. For severe burns, the linear and non-linear regressions have R-square values of .84 and .86. Therefore, each model explained 84% and 86% of the variance of aboveground biomass.

**Moderate Burns**

*Linear Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541010-84373700-acc4-11ea-907c-6098c3cc61d7.png">
</p>

*Polynomial Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541011-84373700-acc4-11ea-8aa4-6234b7e3d349.png">
</p>

**Severe Burns**

*Linear Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541025-89948180-acc4-11ea-99df-9d5aef485481.png">
</p>

*Polynomial Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541026-89948180-acc4-11ea-98c1-434bc46c605b.png">
</p>

Because there is little difference between the linear and polynomial models of aboveground biomass and burn scar age for both moderate and severe burns, I would advise using the linear regression results to analyze this relationship because it provides the simplest explanation of how aboveground biomass changes following a fire event.

**Net Ecosystem Productivity**

The results of both linear and polynomial (quadratic) regressions used to model the relationship between net ecosystem productivity and burn scar age are below. For moderate burns, the linear regression has an R-square of .01 while the polynomial regression has an R-square of .01. For both models, burn scar age only explain over 1% and 2% of the variance of net ecosystem productivity. Therefore both models perform extremely poorly when describing the relationship between net ecosystem productivity and burn scar age for moderate burns. This is improved only slightly when examining the regression results for severe burns. In this case, the linear regression has an R-square of .08 while the polynomial regression has an R-square of .09. For both models, burn scar age only explain over 8% and 9% of the variance of net ecosystem productivity. Though the relationship between Net Ecosystem Productivity and Burn Scar Age is better modeled using polynomial equation, the polynomial regression still performs relatively poorly.

**Moderate Burns**

*Linear Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541012-84cfcd80-acc4-11ea-8561-f1afb823aaa2.png">
</p>

*Polynomial Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541013-84cfcd80-acc4-11ea-843c-427f66798d2d.png">
</p>

**Severe Burns**

*Linear Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541027-8a2d1800-acc4-11ea-8b86-71c9ffd02dd8.png">
</p>

*Polynomial Regression Results*
<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541028-8a2d1800-acc4-11ea-9885-dc0ec1bf43be.png">
</p>

Because Net Ecosystem Productvity and Burn Scar Age were poorly modeled by both linear and polynomial regressions, I opted to run the F-statistic test to determine whether the  relationship between Net Ecosystem Productivity and Burn Scar Age had a relationship signifcantly different from an intercept model.

### F-Statistic Results for Net Ecosystem Productivity

For moderate burns, the relationship had a p-value less than the alpha (0.05) and therefore was signifcantly different from an intercept model.

<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541023-89948180-acc4-11ea-8058-696b55d432fe.png">
</p>

For severe burns, the relationship also had a p-value less than the alpha (0.05) and therefore was signifcantly different from an intercept model.

<p align="left">
  <img src="https://user-images.githubusercontent.com/54719919/84541024-89948180-acc4-11ea-852b-3294fa0081c8.png">
</p>

This means that Net Ecosystem Productivty does have a signifcant relationship with Burn Scar Age. Therefore, it's worth spending more time either (1) finding a more appropriate mathematical function to represent the relationship between Burn Scar Age and Net Ecosystem Productivity or (2) adjusting the time frame of this study to focus only on the initial years following a burn when NEP is more volatile. 

### Conclusions & Improvements

1. Aboveground Biomass increases as burn scars age for both moderate and severe burns. Of the models I created, the relationship is best described using a simple linear model.

2. Net Ecosystem Productivity does have a significant relationship with burn scar age, as determined by the F-statsitic. However, the two models used for this project do not capture this relationship well. Additional exploration using different types of regression may provide a better model of how net ecosystem productivity changes over time.

3. This study could be improved by finding or creating data layers with a smaller time interval. Specifically, I think analyzing Net Ecosystem Productivity requires a higher resolution dataset because NEP is highly volatile for only several years after a fire. Therefore, using data with monthly of 6-month intervals would provide a sensitive picture of how NEP changes over time.

4. Additionally, with more time, I would find an MTBS data layer which describes fire severity rather than classify the burns based on aboveground biomass loss. I would do this because severity is also linked to belowground biomass loss. Therefore, only classifying fire severity based on aboveground biomass loss likely causes more fires to be classified as “Severe” than otherwise would be. 
