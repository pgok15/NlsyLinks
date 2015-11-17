---
title: "ExtraOutcomes79"
---

***
# Description

> Extra outcome variables in the NLSY79

 dataset is provided primarily to facilitate documentation examples.
 
***
# Formats
The dataset is available in the following formats:

 * [CSV](https://raw.githubusercontent.com/LiveOak/NlsyLinksDetermination/master/ForDistribution/Outcomes/ExtraOutcomes79.csv) is our recommendation.
 * [R Binary](https://github.com/LiveOak/NlsyLinks/blob/master/data/ExtraOutcomes79.rda), after navigating to the page, click on the 'View Raw' button to download it.
 * *SAS* (coming soon.)

***
# Data Dictionary

A data frame with 11,495 observations on the following 6 variables. There is one row per subject.  

| Variable Name | Type | Variable Description |
| :------------ | :--- | :------------------- |
| SubjectTag | integer | The ID value assigned by NLS to the first subject.  For Gen1 Subjects, this is their "CaseID" (ie, R00001.00).  For Gen2 subjects, this is their "CID" (ie, C00001.00). |
| SubjectID | integer | The ID value assigned by NLS to the first subject.  For Gen1 Subjects, this is their "CaseID" (ie, R00001.00).  For Gen2 subjects, this is their "CID" (ie, C00001.00). |
| Generation | integer | The generation of the subject.  Values are either 1 or 2, representing Gen1 and Gen2.  Note that this variable is not a  `factor` (in constrast with data frames like [`Links79Pair`](./data_links_79_pair.html).  This dataset is supposed to mimick the dataset provided by the researcher, which typically will not have been converted to a `factor`. |
| HeightZGenderAge | float | The subject's height, standardized by gender and age (see Details). |
| WeightZGenderAge | float | The subject's weight, standardized by gender and age (see Details). |
| AfqtRescaled2006Gaussified | float | Armed Forces Qualification Test Score (Gen1 only; see Details). |
| Afi | float | Self-reported age of first intercourse (Gen1 only; see Details). |
| Afm | float | Self-reported age of first menstration (Gen1 only; see Details). |
| MathStandardized | float |  Standardized PIAT Math scores (Gen2 only; see Details). |


***
# Details
The `SubjectTag` variable uniquely identify subjects.  For Gen2
subjects, the SubjectTag is identical to their CID (ie, C00001.00 -the
SubjectID assigned in the NLSY79-Children files).  However for Gen1
subjects, the SubjectTag is their CaseID (ie, R00001.00), with "00"
appended.  This manipulation is necessary to identify subjects uniquely in
inter-generational datasets.  A Gen1 subject with an ID of 43 has a
`SubjectTag` of 4300.  The SubjectTags of her four children remain
4301, 4302, 4303, and 4304.

For Gen2, an NLSY79 variable of `MathStandardized` is C05801.00.

`Afi` and `Afm`, values were simplified
(to one value per subject) by Kelly Meredith in Sept 2010.

The variables for height and weight were manipulated in R files available in a 
[repository](https://github.com/LiveOak/NlsyLinksDetermination/tree/master/ForDistribution/Outcomes) available to the public.
Find the appropriate subfolder, and view the HTML report for more details.

***
# Example in R
```r
library(NlsyLinks) #Load the package into the current R session. #Update with `devtools::install_github("LiveOak/NlsyLinks")`
gen2Outcomes <- subset(ExtraOutcomes79, Generation==2) #Create a dataset of only Gen2 subjects.
                  
#plot(ExtraOutcomes79) #Uncomment to see a large scatterplot matrix.
summary(ExtraOutcomes79)

oldPar <- par(mfrow=c(3,2))
hist(ExtraOutcomes79$Generation)
hist(ExtraOutcomes79$MathStandardized)
hist(ExtraOutcomes79$HeightZGenderAge)
hist(ExtraOutcomes79$WeightZGenderAge)
hist(ExtraOutcomes79$Afi)
hist(ExtraOutcomes79$Afm)
par(oldPar)
```