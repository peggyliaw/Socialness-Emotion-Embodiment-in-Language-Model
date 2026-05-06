# Socialness-Emotion-Embodiment-in-Language-Model
Testing the extent to which word meanings in language models are based on experience specific to humans: socialness, emotion, and physical body.

## Background/Motivation
Language models have been widely criticized for lacking core cognitive capacities that humans have. Three central critiques stand out: 
(1) Models are not inherently social
(2) Models do not possess emotions
(3) Models do not have physical bodies
In contrast, human language learning is deeply shaped by social interaction, emotional experience, and embodied engagement with the physical world. Word meanings are acquired not only through linguistic context, but also through relationships with others, affective states, and sensorimotor experience. Because language models lack these pathways to language learning, an open question remains: how similar/different are model's internal representations of meaning compared to humans'.

This project looks into whether word meanings encoded in language models are less grounded in socialness, emotion, and bodily experience relative to humans' understanding. Specifically, I compared model-derived representations with human ratings along these dimensions. This project aims to evaluate the extent to which current language models capture psychologically grounded aspects of meaning. 

## Datasets
This project uses several existing human datasets on socialness, emotional arousal, and body-object interaction ratings of English words.
- **Socialness Ratings (1-7)**. Diveica, V., Pexman, P.M. & Binney, R.J. (2023). Quantifying social semantics: An inclusive definition of socialness and ratings for 8388 English words. Behav Res 55, 461–473. https://doi.org/10.3758/s13428-022-01810-x. Ratings data available here: https://github.com/DiveicaV/SocialnessNorms/blob/main/Data/Ratings_sum.stat.csv
  - Socialness Ratings.csv
- **Arousal and Size Ratings (1-9)**. Scott, G.G., Keitel, A., Becirspahic, M. et al. The Glasgow Norms: Ratings of 5,500 words on nine scales. Behav Res 51, 1258–1270 (2019). https://doi.org/10.3758/s13428-018-1099-3
  - Glasgow Ratings.csv
- **BOI Ratings (1-7)**. Pexman, P.M., Muraki, E., Sidhu, D.M., Paul D. Siakaluk & Melvin J. Yap. (2019). Quantifying sensorimotor experience: Body–object interaction ratings for more than 9,000 English words. Behav Res 51, 453–466. https://doi.org/10.3758/s13428-018-1171-z
  - BOI Ratings.csv

Note that the priliminary analysis considers Size as the measurement of word meaning, because the link between speech sounds and meanings seem to be non-arbitrary and innate to humans on the Size dimension, as evidenced by research on sound symbolism.

Representations of word meanings in language model were quantified using "semantic projection" technique by Grand et al. (2018): https://arxiv.org/pdf/1802.01241

## Analysis and Results
Three regression models were built:
- Model 1: Size ~ Socialness * Group
- Model 2: Size ~ Arousal * Group
- Model 3: Size ~ BOI * Group
Hypothesis: the associations between Size and Socialness, Arousal, and BOI will be stronger for human than for model

**Model 1**
```
                                      coef    std err          t      P>|t|      [0.025      0.975]
---------------------------------------------------------------------------------------------------
Intercept                        2.889e-16      0.024   1.19e-14      1.000      -0.048       0.048
group[T.Model]                  -1.226e-16      0.034  -3.58e-15      1.000      -0.067       0.067
SocialnessScaled                    0.4694      0.024     19.372      0.000       0.422       0.517
SocialnessScaled:group[T.Model]    -0.3675      0.034    -10.725      0.000      -0.435      -0.300
```
Null results for group, meaning that model and human did not have a bias towards giving a higher or lower rating to Size.
High social words are perceived as larger in size, and this association is stronger in human compared to model.
**Model 2**
```
                                   coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------------------------
Intercept                     7.955e-16      0.023   3.39e-14      1.000      -0.046       0.046
group[T.Model]               -7.612e-16      0.033   -2.3e-14      1.000      -0.065       0.065
ArousalScaled                    0.5011      0.023     21.379      0.000       0.455       0.547
ArousalScaled:group[T.Model]    -0.1960      0.033     -5.914      0.000      -0.261      -0.131
```
Null results for group, meaning that model and human did not have a bias towards giving a higher or lower rating to Size.
High arousal words are perceived as larger in size, and this association is stronger in human compared to model.
**Model 3**
```

                               coef    std err          t      P>|t|      [0.025      0.975]
--------------------------------------------------------------------------------------------
Intercept                 2.437e-16      0.025   9.82e-15      1.000      -0.049       0.049
group[T.Model]           -5.296e-17      0.035  -1.51e-15      1.000      -0.069       0.069
BOIScaled                   -0.3748      0.025    -15.105      0.000      -0.423      -0.326
BOIScaled:group[T.Model]     0.3120      0.035      8.893      0.000       0.243       0.381
```
Null results for group, meaning that model and human did not have a bias towards giving a higher or lower rating to Size.
Words that are more difficult to interact with are perceived as larger in size, and this association is stronger in human compared to model.

## Takeaway
Represenataions of English word meanings (quantified on Size dimension) seem to be associated with social, emotional, and bodily information of words. This is true for both human and model. However, the effects were stronger for human compared to model. This indicates that, although representations of words are similar between human and model, language understanding in model may still be fundamentally different from how human acquire meanings of words.
