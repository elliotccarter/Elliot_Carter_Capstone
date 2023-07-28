# Elliot_Carter_Capstone
Project title: Modeling and Predicting Conspiracy Belief

Download dataset from:
https://osf.io/jqnd6/ (must be converted to .csv from .RData)

Project Overview:

Problem Area:
Many of the biggest problems we face collectively—climate change, pandemics, and threats to democracy, for example—demand coordinated, cooperative responses. But how can we cooperate to address these issues when we cannot even agree about their existence or nature? Misinformation and conspiracy belief are widespread and persistent obstacles to building the collective trust required to meet these challenges.

It is notoriously difficult to change conspiracy theorists’ minds (‘Of course things seem that way; that’s part of the cover up!’). But a reasonable first step would be to try to understand why people believe in conspiracy theories, and what kinds of people are most susceptible to conspiracy belief.

The User and the Impact:
Public officials need to understand the motivations behind conspiracy belief to guide decision-making and communication. Deeper knowledge of the appeal of conspiracy theories and of the kinds of people who believe them would allow for better targeted messaging and interventions. This could help with educating the public on the efficacy and safety of vaccines, or on the necessity of environmental regulation. For a concrete example, consider that an independent research group, the Council of Canadian Academies, reports that misinformation about COVID-19 vaccines caused hesitancy towards vaccination for 2.35 million Canadians, and that vaccine hesitancy led to an excess $300 million in hospital costs and 2,800 deaths in Canada alone.  To tackle the problems posed by misinformation, we need a better collective understanding of how it spreads.

The Idea:
The idea behind this project is to use machine learning to help identify the factors that best predict conspiracy belief. The extant quantitative research on conspiracy theories has identified various correlations between conspiracy belief and demographic variables (e.g., age, or gender) or psychological features (e.g., narcissism, or trust in scientists or governments). 

But little work has been done so far attempting to model the data or apply the tools of machine learning to the problem. An exception is Brandenstein (2022), who built a predictive model based on survey data collected by the COVID-19 Psychological Research Consortium in the UK (McBride et al. 2019). The aim of this project is to further explore the application of machine learning techniques to understanding conspiracy belief. For example, how might we use other datasets to build predictive models to understand what makes someone susceptible to believing in conspiracy theories? Or how might we use machine learning segmentation or cluster analysis to understand the relationships between demographic and psychological features typical of a conspiracy believer?

The Data:
The data for this project comes from a 2022 study by Imhoff et al, from a paper titled "Conspiracy Mentality and Political Orientation Across 26 Countries." The dataset uses a measure for conspiracy mentality called the Conspiracy Mentality Questionnaire, or CMQ (Bruder et al 2013). The questionnaire asks respondants to rate their degree of confidence (from 'certainly not' to 'certain') in five statements:

1. *I think that many very important things happen in the world, which the public is never informed about.*
2. *I think that politicians usually do not tell us the true motives for their decisions.*
3. *I think that government agencies closely monitor all citizens.*
4. *I think that events which superficially seem to lack a connection are often the result of secret activities.*
5. *I think that there are secret organizations that greatly influence political decisions.*

The study includes two datsets, which differ in the columns they contain. Here is a partial description of the data:

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
