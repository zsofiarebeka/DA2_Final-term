# <center> Data Analysis 2 - Final Term project</center>
# <center> Factors Affecting Women's Parliamentary Seats: Education, Gender Inequality, Labor, and Human Development Index </center>


<center>This study investigates the relationship between the % of seats held by women in parliaments and other socio-economic factors, like Gender Inequality Index (GII), Human Development Index (HDI), and data on the participation of men and women (separately) in the secondary education and the labour force accross 195 countries. With the help of regression models, it can be ecplored how these dimensions can be associated with the main dependent variable. The results show a strong positive correlation between women parliament seats(%) and secondary education participation rate and a negative correlation with the Gender Inequality Index.</center>

----------------------------------------------------------------------------------------------------------------------
## 1. Introduction

The underrepresentation of women is not a new phenomenon under the sun, in particular when it comes to roles with higher authorities.  One example are roles in the institutions of representative democracies, parliaments. Male majority in parliaments has been considered normal in the past decades, however female representation is gaining more and more attention and importance. As a woman, I find it particularly interesting and close to my heart to understand the factors that drive the change for equal representation of males and females in such institutions. There are several socio-economic factors that can be associated with this change, however female secondary education participation, a country's Gender Inequality Index and the female labour force participation are crucial benchmarks to assess female representation in parliaments across different countries.

- My aim with this paper is to study the correlation between:

    - female secondary education participation rate and % of parliament seats held by women
    - female secondary education participation rate, Gender Inequality Index (GII) and  and % of parliament seats held by women
    - female secondary education participation rate, female labour force participation rate and % of parliament seats held by women
    - all of the abovementioned rates and indexes and % of parliament seats held by women
    - And to broaden the scope of understanding gender disparities: Study the frequency distribution of the % of seats sorted by Human Development Index
    
The expectations of the results include higher female secondary education and labour force participation rate increase the possibility of the number of seats held by women. Moreover, a higher GII is expected to decrease the % of seats held by women.
    
-----------------------------------------------------------------------------------------------------------------------
## 2. Data

The data used in this report was found on [Kaggle]("https://www.kaggle.com/datasets/rajkumarpandey02/world-data-of-gender-inequality-index"), but the original source is [Human Development Reports]("https://hdr.undp.org/data-center/documentation-and-downloads"), namely the *Table 5: Gender Inequality Index*. The dataset contains 195 rows and 13 columns, where data is categorized by countries and is ranked by the Human Development Index (HDI). Other variables include ranks, index values and % rates and the original data type of the columns are *object*. The dataset contains several missing values denoted as '..' or '...'. The dataset is representative of 2021, except for the maternal mortality ratio, which reflects 2017 - and is not needed for our analysis. 

For this study, data cleaning and wrangling was necessary before performing regression models. Besides renaming and reformatting and dropping unnecessary columns, I replaced the missing values with the correct *NaN* format and transformed the data types of the columns from object to float to be able to perform regression models. The data cleaning resulted in the following conclusions:
- There are several missing values as the 'count' values are different
- The dependent variable, "parliamentseatsheldbywomenrate" ranges from 0% to 55.7% and has 2 missing values
- The explanatory variable, femalesecondaryeducation column has missing values (18, namely)
- The first conditioning variable, female labour force ranges from 6 to 83.1 and has 15 missing values
- The second conditioning variable, gender inequality index (GII) ranges from 0.013 to 0.82 (on a 0-1 scale) and has 25 missing values
- In conclusion, we need to drop the rows where we have missing values in the variables that we carry out this analysis with

Variables with explanation used for the regression analysis:

- **Dependent variable (y)**: Share of seats in the parliament: Proportion of seats held by women in the national parliament expressed as a percentage of total seats. For countries with a bicameral legislative system, the share of seats is calculated based on both houses.
- **Explanatory variable (x)**: Female secondary education: Percentage of the female population ages 25 and older that has reached (but not necessarily completed) a secondary level of education.
- **Conditioning variable (z1)**: Gender Inequality Index: A composite measure reflecting inequality in achievement between women and men in three dimensions: reproductive health, empowerment and the labour market. The exact calculation of the index can be found [here]("https://hdr.undp.org/sites/default/files/2021-22_HDR/hdr2021-22_technical_notes.pdf").
- **Conditioning variable (z2)**: Female labour force: Percentage of the female population ages 15 and older that participate in the labour force.
- **Dummy variable**: To be able to perform a logistic regression, I needed to create a binary variable of the dependent variable, "seats held in the parliament by women". As it is a percentage rate, I created a binary outcome variable indicating whether the percentage of seats held by women is above or below a specific threshold:
        - 1: Indicates that the percentage of seats held by women is above a certain threshold (25%)
        - 0: Indicates that the percentage of seats held by women is below or equal to the threshold
        
Other variables in the dataset:
- Countries
- Human Development Index indicators:
    - HDI rank
    - HDI level
- Gender Inequality Index indicators:
    - GII (z1)
    - GII rank
- Reproductive Health indicators:
    - Maternal mortality ratio: Number of deaths due to pregnancy-related causes per 100,000 live births.
    - Adolescent birth rate: Number of births to women ages 15–19 per 1,000 women ages 15–19.
- % of seats in the parliament  held by women (y)
- Educational indicators:
    - Female secondary education rate
    - Male secondary education rate
- Workforce indicator:
    - Female labour force participation (x)
    - Male labour force participation
 
----------------------------------------------------------------------------------------------------------------
## 3. Models

### Model 1: % of seats held by women in the parliament on female secondary education rate

$parliamentseats=\beta_0+\beta_1 x_1 x femalesecondaryeducation$

Model 1 is a simple linear regression of % of seats held by women in the parliament on female secondary education rate. The regression table can be found at **Appendix A1**. According to the $\beta_1$ of the model, females with secondary education have 7.01% more probability, on average, to earn seats in the parliament. Approximately 2.9% of the variation in the percentage of seats held by women in parliament can be explained by the variation in female secondary education rate. The CI of the slope is [0.008;0.132] which does not include zero, meaning that we can be 95% confident that the true effect of the female secondary education rate on the percentage of seats held by women in parliament is between 0.8% and 13.2%. The p-value < 0.05 also proves the above statement.
<img width="397" alt="image" src="https://github.com/zsofiarebeka/DA2_Final-term/assets/144313188/60aa1866-1fcd-4854-b40a-dd5bce023f90">

To identify a potential nonlinear relationship, I created a regression graph with the lowess method. (**Appendix A2**) According to the chart, there is a slight decrease in the seats between 20% and 40% of female secondary education rate, which is not visible in the simple linear regression.

<img width="533" alt="image" src="https://github.com/zsofiarebeka/DA2_Final-term/assets/144313188/15c2bc8e-3290-4884-8037-13ae98abbcdc">

### Model 2: % of seats held by women in the parliament on female secondary education rate and GII (z1)

$parliamentseats=\beta_0 + \beta_1 femalesecondaryeducation + \beta_2 GII$

The second model studies how the female secondary education and the Gender Inequality Index combined have an overall impact on the seats held in the parliament. (**Appendix B1**) All covariates are significant at 99%. $\beta_1$ of this model indicates that for a one-unit increase in female secondary education rates, and while holding the GII constant, the model predicts a decrease in the percentage of seats held by women in parliament by 0.208 units. The CI of the slope is [-0.295;-0.121] not including zero. Conditioning on z1, $\beta_2$ shows that for a one-unit increase in the GII, and while holding female secondary education constant, the model predicts a decrease in the percentage of seats held by women in parliament by 52.114 units. The two variables' CIs don't overlap, suggesting a statistically significant difference. The robust SE of this coefficient is significantly higher (6.409) than the SE of $\beta_1$, meaning that it might be less reliable or more sensitive to variations in the data compared to $\beta_1$. R-squared is 0.267, meaning that by taking GII into consideration, we increase the model's goodness of fit. To identify further potential nonlinear relationships, I analyzed the second model with a lowess method and found a similar pattern to Model 1 (decrease between 20% and 40%). (**Appendix B2**)

<img width="551" alt="image" src="https://github.com/zsofiarebeka/DA2_Final-term/assets/144313188/a7a3f254-6c97-45cd-b7cb-c6e86ead0c50">

### Model 3: % of seats held by women in the parliament on female secondary education rate and female labour force rate (z2)

$parliamentseats=\beta_0 + \beta_1 femalesecondaryeducation + \beta_2 femalelabourforce$

The third model examines how the female secondary education and the Female labour force participation rate combined have an overall impact on the seats held in the parliament. (**Appendix B3**) All covariates are significant at 99% except for $\beta_0$ which is significant at 95%. $\beta_1$ showss a one-unit increase in female secondary education rates, and while holding the female labour force rate constant, the model predicts a 8.2% increase in the percentage of seats held by women in parliament. The CI of the $\beta_1$ is [0.023;0.142]. $\beta_2$ suggests that for a one-unit increase in the female labour force, and while holding female secondary education constant, the model predicts a 24.1% increase in the percentage of seats held by women in parliament. The CI of the slope is [0.130;0.352], meaning that we can be 95% confident that the true effect of the of the female labour force rate, while holding the female secondary education rate constant, on the percentage of seats held by women in parliament is between 13% and 35.2%. R-squared is higher than the R-squared only considering the female secondary education (0.117), but not higher when we only take the GII into consideration (0.259).

### Model 4: % of seats held by women in the parliament on female secondary education rate, GII (z1) and female labour force rate (z2)

$parliamentseats=\beta_0 + \beta_1 femalesecondaryeducation + \beta_2 GII + \beta_3 femalelabourforce$

This model challenges the assumptions about the direct relationships between all the variables and their correlation between parliament seats. (**Appendix C1**) All covariates are significant at 99%. $\beta_1$ indicates that the model predicts a 1.4% increase in the percentage of seats held by women in parliament considering female secondary education. The confidence interval of the slope is [-0.259;-0.088] which does not include zero. None of the confidence intervals overlap, indicating a statistically significant difference between the variables. (**Appendix C2**) This particular regression model exhibits the highest R-squared value among all the examined models, indicating the strongest explanatory power in explaining the variation (0.299). This means that by taking all the variables into consideration, we increase our model's goodness of fit.

<img width="439" alt="image" src="https://github.com/zsofiarebeka/DA2_Final-term/assets/144313188/b6fc7cd1-b35d-40cd-8c6f-fd6b5a22f4e2">


To broaden the scope of understanding gender disparities, **Appendix D** shows a distribution of parliament seats by the Human Development Index (HDI). My expectations were skewed distributions with right long tails, but surprisingly, distributions for all HDI categories are normal, only slightly skewed to the right as the HDI level increases.

<img width="468" alt="image" src="https://github.com/zsofiarebeka/DA2_Final-term/assets/144313188/bf374086-2f70-42de-ae27-2c4eee7a9538">

## 4. Probability calculation

Upon checking the linear probability model (LPM), I concluded that the spread of the prediction goes well above 1 (39.3141) which means that we need to use logit and probit models to get accurate predicted probability values. (**Appendix E1**)

### Interpretation for logit

- A one-unit increase in female secondary education is associated with an approximate decrease of 0.0063 in the log odds of being above the threshold (holding other variables constant). The effect is statistically significant (p < 0.05)
- A one-unit increase in the Gender Inequality Index (GII) is associated with an approximate decrease of 1.5492 in the log odds of being above the threshold (holding other variables constant). The effect is highly statistically significant (p < 0.001).
- A one-unit increase in female labor force participation rate is associated with an approximate increase of 0.0051 in the log odds of being above the threshold (holding other variables constant). The effect is statistically significant (p < 0.05).

### Interpretation for probit
- Almost same results as the results as of logit, however, far from LPM.

### Interpreting goodness of fit measures (Appendix E2)

- The Brier scores suggest that the models perform very similarly, with logit (0.2011) and probit (0.2012) providing the best fit.
- LPM has a higher Brier score of 659.618 suggesting a significantly worse fit.
- The log-loss values of each model show the similar ordering: logit and probit model show very similar results (-0.5855 and -0.5852 respectively).
- LPM has a higher log-loss absolute value, performing lower than logit and probit.
- The prediction values of only the logit and probit models are correctly bound between 0 and 1.

<img width="152" alt="image" src="https://github.com/zsofiarebeka/DA2_Final-term/assets/144313188/1559f313-7051-422a-a0ca-41394299ab98">

----------------------------------------------------------------------------------------------------------------------
## 5. Conclusion

The study uncovers key relationships between socio-economic factors and women's representation in parliamentary seats. To enhance female representation, and considering the strong correlation between secondary education and % of seats, nations should invest and ensure comprehensive and accessible educational opportunities for women accross all demographics. The tackle the matter of significant impact of GII on parliamentary seats, I would suggest targeted policies promoting gender equity in healthcare, workforce participation which could contribute to a more equitable political landscape. In the case of labour force - as it has also significant (24.1% increase) - impact, I would recommend providing parental leave, affordable childcare, promoting flexible work arrangements, and prividing equal career development opportunities for all genders.

## 6. Main summary and limitations

The analysis revealed a strong correlation between female secondary education rates and parliamentary seats held by women, with a 1% increase in education linked to a 7.01% rise in representation. Notably, this relationship diminished between 20% and 40% education rates. Conversely, higher Gender Inequality Index (GII) values corresponded to a significant decrease (52.114 units) in women's parliamentary representation per GII unit increase. Moreover, a 1% rise in female labor force participation correlated with a 24.11% increase in parliamentary seats held by women, showcasing the empowerment of increased workforce participation. While logit and probit models align closely with actual outcomes, the LPM model underperforms. The study's limitations encompass missing data resulting in incomplete country representation. Additionally, the Gender Inequality Index (GII) values' interpretation was challenging due to high standard errors (6.409).

-----------------------------------------------------------------------------------------------------------------------
## References

- World Data of Gender Inequality index (2023) Kaggle. Available at: https://www.kaggle.com/datasets/rajkumarpandey02/world-data-of-gender-inequality-index (Accessed: 21 December 2023). 
- Nations, U. (no date) Documentation and downloads, Human Development Reports. Available at: https://hdr.undp.org/data-center/documentation-and-downloads (Accessed: 21 December 2023). 
