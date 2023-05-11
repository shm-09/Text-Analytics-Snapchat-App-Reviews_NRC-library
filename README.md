# Text-Analytics-Snapchat-App-Reviews_NRC-library
Analysis of Snapchat Application Review scrapped from Google Playstore (EDA, TF-IDF, LDA, Multinomail Regression)


### Objective: 
1.	Sentiment analysis of app reviews curated from Google Play Store for SnapChat. (NRC library used in R/Python)
2.	LDA Topic Modeling to understand aggregated broad ranging themes addressed per Sentiment derived from Sentiment Analysis.
**Data**: Extracted via review scrapping on Google Playstore

### Methodology:
1.	EDA ->
  a.	Getting a sense of the distribution of the reviews per Rating (1, 2, 3, 4 or 5 stars)
  b.	TF-IDF (over the entire corpus & over reviews per rating) to quantify the frequency of individual words & determine their uniqueness per topic.
  c.	Word clouds (over the entire corpus & over reviews per rating) to visualize commonly occurring words.
2.	Illustration of Zipf’s Law (which states that frequency is inversely proportional to rank)
3.	Text pre-processing ->
  a.	Cleaning (for special characters, punctuation etc.)
  b.	Converting all text to lower case
  c.	Tokenization (unigrams, bigrams)
4.	Text Analytics ->
  a.	TF-IDF & listing top-10 words per Rating from the Reviews corpus
  b.	Visualization of Bigrams to get a sense of negations occurring in the corpus
  c.	Topic Modeling (LDA) per Rating to understand the broad themes (what customers like or what grievances are being highlighted)
  d.	Sentiment analysis (NRC library) & categorization of Reviews per sentiment
5.	Multinomial Logistic Regression -> To predict the probability of the Rating being given (either 1, 2, 3, 4 or 5 stars) based on the sentiments conveyed in the reviews.
  a.	Dependent variable: Rating (1, 2, 3, 4 or 5)
  b.	Independent variables: affect frequencies (term frequencies) per sentiment/emotion
6.	Plotting Marginal Probability graphs from the Multinomial Regression results to visualize the effect of the term frequencies per emotion on the ratings. 

### Brief overview of NRC library/lexicon:
Contains of list of around ~15000 emotive words with their associations with 8 emotions (Anger, Anticipation, Disgust, Fear, Joy, Sorrow, Surprise & Trust) categorized into 2 broad sentiments (Negative & Positive).
We decided on taking the NRC library for this particular case as we wanted to determine the emotions being conveyed in the reviews.
Interesting Insights:
**Expectations:** The positive emotions should have a +ve coeff in the model while -ve emotions should have a -ve coeff in the model & depending on the rating category the model was predicting the probability of, the significance of variables will change accordingly.
**Analyzing the Multinomial regression:**
1.	For most of the emotions (fear, anger, sorrow, disgust, joy) the coefficients were following our general expectations:
  a.	As the frequency of terms conveying joy increased -> Rating increased (+ve coeff of Joy in the model)
  b.	As the frequency of terms conveying fear, anger, sorrow or disgust increased -> Rating decreased (-ve coeff of the emotions in the model)
2.	Surprisingly Trust, Surprise & Anticipation had -ve coefficients which went contrary to our expectations. Looking a bit deeper into it we realized the following:
  a.	In the NRC library, the terms associated with Trust (Account etc.) were generally used to convey a certain issue pertaining to the user Accounts. Although as a standalone token, it might have be positive, but the way in which it was used in the Reviews held an overall negative connotation leading to negative ratings.
  We came to this conclusion post analyzing the topics derived from LDA Topic modelling.
  Exp 1 – “Account” mostly occurred in reviews with Rating 1 or 2 & the general theme was users highlighting issues with their Accounts in the application. In the NRC library though,
  “Account” in listed under Trust.
  Exp 2 – “Hope” as well occurred in reviews with lower ratings accompanying general themes in which the users expressed their concerns over certain issues being fixed. “Hope” is listed under Anticipation in the NRC library.

### Key Learnings:
1.	Digging deeper into the lexicon of any particular Text/Sentiment analysis library is key to understanding the results being obtained.
2.	TF-IDF & Topic modelling should ideally be performed to make sense of the results being obtained, instead of just taking them at face value. 
