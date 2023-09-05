# Modelling and Understanding Conspiracy Belief
**Capstone project for BrainStation data science bootcamp, June-September 2023**<br>
**Author**: Elliot Carter<br>
**Contact**: elliot.carter@gmail.com

Download original data from:
https://osf.io/jqnd6/ (must be converted to .csv from .RData)

Cleaned dataset and supplementary datasets available at:
https://drive.google.com/drive/folders/1vlUBD_szowe5O3GKrLhlAaN0_fqkKB3L?usp=sharing

Enviroment

    conda create -n conspiracy_project python=3.9 numpy pandas matplotlib seaborn plotly scikit-learn=0.24.1 jupyter jupyterlab conda activate er_predictor
    
Other libraries used

    conda install -c conda-forge xgboost=1.1.1 mlxtend conda install -c conda-forge shap conda install -c conda-forge lime

Kernel

    ipython kernel install --name "conspiracy_project" --user

**Project Overview**:

My project is aimed at using the tools of data science to better understand the phenomenon of conspiracy theory belief. Public officials need to understand the factors driving conspiracy belief to guide decision-making and communication. Deeper knowledge of the appeal of conspiracy theories and of the kinds of people who believe them would allow for better targeted messaging and interventions. This could help with educating the public on the efficacy and safety of vaccines, or on the necessity of environmental regulation. For a concrete example, consider that an independent research group, the Council of Canadian Academies, reports that misinformation about COVID-19 vaccines caused hesitancy towards vaccination for 2.35 million Canadians, and that vaccine hesitancy led to an excess $300 million in hospital costs and 2,800 deaths in Canada alone.

The dataset I am working with comes from a 2022 paper by Roland Imhoff and 39 coauthors at various European universities (Imhoff et al 2022). The paper reports the results of two surveys studying the relationship between political orientation and susceptibility to conspiracy belief, with respondents from 26 European countries. The datasets include two measures of  political orientation: self-reported location on a left-right political spectrum and reported voting behaviour in the previous election. Susceptibility to conspiracy belief is measured via responses to a standard questionnaire (the 'Conspiracy Mentality Questionnaire,' or 'CMQ') (originating in Bruder et al 2013). The datasets also include personal-level demographic information (age, sex, country, etc.) as well as some country-level information about political and economic climate.

In this project, I perform exploratory data analysis and data cleaning to prepare the data for modelling, and then optimize various models and use model-agnostic interpretive tools (SHAP and LIME) to understand how the models generate their predictions. I analyze the results to get a better understanding of the various linear and non-linear relationships between the individual and country-level features and conspiracy mentality. 

**Description of Project Components**:

**1_Initial_EDA**: This notebook reflects the first stage of the project, including exploratory data analysis, with a focus on identifying data quality issues and other concerns that set the stage for the preprocessing required before modelling. It also contains some initial observations about the distribution of the data and country-level patterns.

**2_EDA_and_Baseline_Modelling**: This notebook is the second stage of the project, and it contains the bulk of the data cleaning and preprocessing, with a focus on dealing with missing data and null values. It also includes some feature engineering, wherein new country-level features are added to the dataset, including unemployment rate, GDP, and the Economist's 'Democracy Index' score for each country. The notebook also contains baseline models of the data, which set the stage for further modelling in part 3.

**3_Model_Optimizaiton_and_Interpretation**: In this notebook, I use the previous baseline modelling results to guide the process of optimizing the models, and I explore options for interpreting the models using some model-agnostic interpretive tools (SHAP and LIME). I am working with the final, cleaned version of the data here. In the final section, I summarize the results of the models, recording the parameters and scores for the best versions. I also draw some conclusions about what we can learn by comparing the models' performance as well as from the results of the model-agnostic interpretive tools.

The github for the project also includes slides from presentations given at the BrainStation data science bootcamp, corresponding to the material covered in notebooks 2 and 3.

**Key Results**:

- The best performing models on the dataset are non-linear, ensemble models: Gradient Boosting Regressor and XGBoost Classifier. With the best regression model, we can explain about 27% of the deviations from average conspiracy mentality score in the dataset. With the best classification model, we can accurately categorize about 70% of data points as having above-average conspiracy mentality scores.
- The features that the model uses to generate predictions ('predictors') include both individual level attributes (like age, sex, and political orientation) and country-level features (like the respondent's country, its GDP and its unemployment rate). In our best models, the most important individual-level predictors turn out to be the respondent's level of social conservatism (higher tends to cause higher predictions of conspiracy mentality) and their education status (university degrees tend to cause lower predictions). Features like age and sex also have considerable effects on the models' predictions, but the relationship is complex and non-linear (e.g., it's not simply that higher ages cause higher predictions or vice versa). The most important country-level feature across the models seems to be the country's unemployment rate, with lower rates causing lower predictions.
- What country the respondent comes from does not generally have a large effect on the predictions of our best models, with one exception: a respondent being from the Netherlands is one of the most important features our models used to predict conspiracy mentality (it causes lower predictions). The Netherlands has the lowest average conspiracy mentality score of all countries in the dataset, and it seems that the models cannot predict its low average score from combinations of other features (if we compare with Turkiye or Spain, the countries with the highest average scores, these countries turn out not to be important predictors for the best models).


**The Data**:

The data for this project comes from a 2022 study by Imhoff et al, from a paper titled "Conspiracy Mentality and Political Orientation Across 26 Countries." The dataset uses a measure for conspiracy mentality called the Conspiracy Mentality Questionnaire, or CMQ (Bruder et al 2013). The questionnaire asks respondants to rate their degree of confidence (from 'certainly not' to 'certain') in five statements:

1. *I think that many very important things happen in the world, which the public is never informed about.*
2. *I think that politicians usually do not tell us the true motives for their decisions.*
3. *I think that government agencies closely monitor all citizens.*
4. *I think that events which superficially seem to lack a connection are often the result of secret activities.*
5. *I think that there are secret organizations that greatly influence political decisions.*

**Data Dictionary**: 

- 'Country'
- 'Age'
- 'Sex'
- 'Edu_high': binary category; 1 means the respondant has a university degree
- 'Edu_low': binary category; 1 means the respondant did not finish high school
- 'Pol_Ori': respondant's self-rating of political orientation on a left-right spectrum ('ZPO' is a Z-score for 'Pol_Ori')
- 'CMQ_{X}': respondant's response to statement X on the CMQ (responses are ratings from 1 to 11; should be rescaled so that 1=0 and 11=10)
- 'CM5x': average of CMQ responses for all five statements
- 'CM4x': average of CMQ responses excluding statement 2
- 'CT_{left/right/neutral}': respondant's endorsement of country-specific conspiracy theories coded as politically left, right or neural
- 'Winner_State': binary variable; 1 represents that the respondant's preferred political party was in power at time of survey
- 'CHES_version': the version of the 'Chapel Hill Expert Survey' used, a survey of experts which produces a codebook for estimating the political ideology of political parties. The CHES codebook was used to translate participants' proclaimed voting intentions or party preferences into comparable numerical ratings (see: https://www.chesdata.eu/)
- 'lrgen','lrecon','galtan': rating of political party preference on different versions of left-right scale (gen: general scale, econ: economic scale, galtan: social scale) (Dataset also includes means and Z-scores for these variables)
- 'lrgengov','lrecongov','galtangov': country-level variables representing the ruling party's location on three different left-right spectra: general, economic, and social, respectively


**References**:

Brandenstein, N. (2022). Going beyond simplicity: Using machine learning to predict belief in conspiracy theories. European Journal of Social Psychology, 52, 910– 930. https://doi.org/10.1002/ejsp.2859

Bruder M, Haffke P, Neave N, Nouripanah N and Imhoff R (2013) Measuring individual differences in generic beliefs in conspiracy theories across cultures: Conspiracy Mentality Questionnaire. Front. Psychol. 4:225. doi: https://doi.org/10.3389/fpsyg.2013.00225

Imhoff, R., Zimmer, F., Klein, O. et al. (2022). Conspiracy mentality and political orientation across 26 countries. Nat Hum Behav 6, 392–403. https://doi.org/10.1038/s41562-021-01258-7

McBride, O., Murphy, J., Shevlin, M., Gibson-Miller, J., Hartman, T.K., Hyland, P., Levita, L., Mason, L., Martinez, A.P., McKay, R., Stocks, T.V., Bennett, K.M., Vallières, F., Karatzias, T., Valiente, C., Vazquez, C. and Bentall, R.P. (2021), Monitoring the psychological, social, and economic impact of the COVID-19 pandemic in the population: Context, design and conduct of the longitudinal COVID-19 psychological research consortium (C19PRC) study. Int J Methods Psychiatr Res, 30: e1861. https://doi.org/10.1002/mpr.1861


