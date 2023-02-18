<!-- #region -->
# Explainable & Realistic Price rofiles in the “Emerald City” (Seattle-Metro)

<br/>

<figure>
    <img src="data/KC_WA.png"
         alt="Housing Markets!"
         width="300"
         height="300">
</figure>

## Authors

Ryan Moore and Diego Fernandez

## Project Overview

<br/>

<figure>
    <img src="data/blueprint.jpg"
         alt="Housing Markets!"
         width="300"
         height="150">
</figure>

<br/>

This project is for the benefit of our stakeholders, Gemstone Developers. The engagement team is tasked with identifying areas in the target expansion area, King County, WA, which can have their price variances predicted using only housing attributes in their control (housing attributes related to design such as sqft, floors, heating type, etc).

### Business Problem

Gemstone Developers are looking to expand their business to the Seattle-Metro Area, and are very risk averse. They would like to know which areas are good bets to expand into, defined as areas that can have their price fluctuations explained using design attributes alone.

They have expressed that they want to cut down on 'unexplained factors' when it comes to fluctuation in price, and have tasked the engagement team to find areas that can have their price fluctuations explained to a statistically significant degree.

### Executive Overview: Results

Using multi-linear regression, the team determined which attributes in the data would be relevant to a developer and identified zip codes which can have their price fluctuations explained to a statistically significant degree. 

The engagement team used an "adjusted r-squared" score of above .6 as appropriately predictable and the success criteria. The engagement team identified 5 zip codes which meet the success criteria.


## Data and Methodology

We utilized a year of housing sale data for our stakeholder-requested analysis

### Data Scope

<br/>

<figure>
    <img src="data/scope.png"
         alt="Housing Markets!"
         width="300"
         height="150">
</figure>

<br/>

Our Datascope was real estate sales from the year of 2021 until 2022. Our stakeholder was only concerned about ZIP Codes within King County; it was identified early on that the data set contained not only sales data in the greater Washington area, but also real estate sale data in other states such as New Jersey, New York, Florida, and even Canada. Please see the date of cleaning section for more information on how we dealt with these records.

Inside of the real estate data, each row represented an individual sale of a property. The subsequent columns describes the features of that sale: including price, address, latitude, and longitude, and other design attributes of the house (square footage, number of floors, patio square feet, garage square feet, ect).

### Data Cleaning

<br/>

<figure>
    <img src="data/cleaning.jpg"
         alt="Housing Markets!"
         width="200"
         height="200">
</figure>

<br/>

As mentioned above, the first step of our data cleaning was to isolate only records that were sold in Washington state. This was done by splitting the address column into various attributes: street name, city, state, and ZIP Code. This allowed us to filter for Washington state. This was done once we had confirmed the address was split appropriately.

Secondly, we converted the different rating columns (grade, condition, view, etc) from their text-based counterparts into numerical values. For example, rather than having the view column show as poor, fair, average, and so on, we converted this into a numerical scale. We did the same exercise for maintenance, condition, and construction grade.

Thirdly, we converted the greenbelt, nuisance, and waterfront criteria from their text based counterparts to one if true, and zero if false. 

Lastly, we converted the heating tape column into dummy variables. The heating column could contain either a singular heating source, or a mix of heating sources (for example, solar/gas heating). To evaluate each heating source individually. This column was split up into individual dummy columns with each record having either a one or a zero, depending on whether or not that property had the heating source.

The sale date was also converted into a datetime object in split up between month in the year, but this is ultimately not used in our analysis 

### Data Filtering

<br/>

<figure>
    <img src="data/filter.png"
         alt="Housing Markets!"
         width="300"
         height="150">
</figure>

<br/>

As mentioend above, we filtered for records only inside of Washington state. We then filtered for ZIP Codes that were considered “ active”. The engagement team decided the 300 sales in the past year for a particular ZIP Code would make it eligible for further analysis (see bias for more information). This was done by grouping all sales by ZIP Code which was a column created above in the data cleaning section.

52 ZIP Codes were identified in total due to their activity levels.

### Data Bias

<br/>

<figure>
    <img src="data/bias.jpg"
         alt="Housing Markets!"
         width="300"
         height="150">
</figure>

<br/>


The engagement team consider the fact that the model may favor ZIP Codes with fewer data points, as smaller data sets are more easily explained than larger ones. To account for this, we decided to go with only active ZIP Codes, that is, ZIP Codes that had 300 or more sales in our data set.

We also noted that there would be bias for ZIP Codes that had lower total price variance, that is the minimum and maximum should be relatively narrow as these sales would be more clustered. When thinking about this bias, we saw this as a benefit to a stakeholder, as the whole intention of the stakeholder is to develop in areas that do not have high fluctuations in sale price. The bias was considered, but was ultimately deemed to be fat beneficial to our analysis

### Methodology

<br/>

<figure>
    <img src="data/method.png"
         alt="Housing Markets!"
         width="200"
         height="200">
</figure>

<br/>

With our target ZIP Codes identified, the engagement team developed a loop which would automatically calculate the ideal combination of identified attributes to maximize the adjusted R squared score.

A colinearity analysis was performed on each of the attributes to ensure colinearity would not distort our R Squared score. We selected elements that were no co-liniated and also relevant to a developer: sqft_living, floors, condition, grade, and heat_gas.

For each ZIP Code, the loop would go through every potential combination of identified attributes and return of the combination that would return the highest adjusted our squared score. The engagement team decided to go with adjusted our squared score to account for the business in practicality of knowing exactly how many Attributes would be going into an initial project.

## Results and Recommendations

<br/>

<figure>
    <img src="data/results.jpg"
         alt="Housing Markets!"
         width="300"
         height="150">
</figure>

<br/>

The engagement team identified five key ZIP Codes with an R squared, score of above .6, which is close to being statistically significant and of interest to our stakeholder.  In plain language is score of .6 means that the attributes selected by our methodology account for about 60% of the total fluctuation in price between sales in that ZIP Code.

Our recommendations for the stakeholder are all rooted in application of the model. The engagement team has developed: 
- Select locations with a high degree of explain ability in the fluctuations of price for that ZIP Code
- Consider how selection of attributes would impact the models ability to explain fluctuations in price
- As well as the inverse; that is, use business considerations to see whether or not determining a certain attribute, would materially affect the explanatory power of the model for a particular ZIP Code

## Repo Structure

<br/>

<figure>
    <img src="data/KC_WA.jpg"
         alt="Housing Markets!"
         width="300"
         height="150">
</figure>

<br/>

This is the README file 

The index.IPYNB contains the Jupiter notebook that explains our information processing and further analysis. 

How are slides.pdf contains are Google slides presentation that summarizes the methodology in findings 

In raw data, you will be able to see the data set we worked with as well as the illustrations used throughout this read me.
<!-- #endregion -->

```python

```
