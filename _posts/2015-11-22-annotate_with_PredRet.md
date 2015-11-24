---
title: "Annotating LC-MS data with PredRet in R"
excerpt: "Here I show how you can use the PredRet database to annotate your data in R"
author: "Jan Stanstrup"
modified: 2015-11-22
categories: metabolomics PredRet R
comments: true
layout: post
output:
  html_document:
    highlight: espresso
    keep_md: yes
    number_sections: yes
    theme: cerulean
    toc: yes
  pdf_document:
    number_sections: yes
    toc: yes
    toc_depth: 3
  word_document: default
---






<style type="text/css">
table.nicetable tr:nth-child(even) {
 background: #f8f8f8;
}

table.nicetable thead th {
font-weight: bold;
background: #d3d3d3;
text-align: left;
}

table.nicetable tr, table.nicetable th, table.nicetable td {
padding: 0.4em;
font-size: 0.7rem;
}
</style>






In this tutorial I will show you how you can use the PredRet database to annotate your LC-MS metabolomics data directly in R. The annotation function I will be using is general-purpose, though, so you can use it to annotate any data where you have a list of compounds with known *m/z*'s and retention times (RTs).

<br>

In short PredRet is a user-driven database of compound retention times. The purpose of PredRet is to be able to predict the RT of a compound in one (your!) chromatographic system if it has been experimentally determined in another chromatographic system by someone, somewhere in the world. You can download the paper [here](../material/papers/Stanstrup, Neumann, Vrhovsek - 2015 - PredRet Prediction of Retention Time by Direct Mapping between Multiple Chromatographic Systems.pdf) and visit the project's home page at [PredRet.org](http://PredRet.org).


<br>
<br>




## Pulling data from PredRet

So lets get going. <br>
First we will download the PredRet database with the [PredRetR package](https://github.com/stanstrup/PredRet). We will get both the experimental and the predicted values for the chromatographic system "LIFE_old".


{% highlight r %}
library(PredRetR)

predret_db <-    PredRet_get_db(exp_pred = c("exp","pred"),
                                systems = "LIFE_old"
                               )
{% endhighlight %}



{% highlight text %}
## Error in PredRet_get_db(exp_pred = c("exp", "pred"), systems = "LIFE_old"): unused argument (systems = "LIFE_old")
{% endhighlight %}


<br>
Then lets take a look at the structure of the ```data.frame``` we have retrieved. If the ```recorded_rt``` column has data we have an experimentally determined RT, if the ```predicted_rt``` column has data we have a RT predicted with the PredRet systems. The ```ci_lower``` and ```ci_upper``` columns show the prediction interval for the predictions.


{% highlight r %}
dim(predret_db)
head(predret_db)
{% endhighlight %}


{% highlight text %}
## Error in eval(expr, envir, enclos): object 'predret_db' not found
{% endhighlight %}



{% highlight text %}
## Error in head(predret_db): object 'predret_db' not found
{% endhighlight %}



<br>

We have the RT directly in the database above but we do not have the *m/z*. Since we have the InChI the easiest way to get the *m/z* is to extract the molecular formula and then use the [Rdisop](https://bioconductor.org/packages/release/bioc/html/Rdisop.html) package to get the mass.


{% highlight r %}
library(Rdisop)
library(stringr)

formulas   <- str_split_fixed(predret_db[,"inchi"],"/",3)[,2]
{% endhighlight %}



{% highlight text %}
## Error in stri_split_regex(string, pattern, n = n, simplify = TRUE, opts_regex = attr(pattern, : object 'predret_db' not found
{% endhighlight %}



{% highlight r %}
masses     <- sapply(formulas, function(x) getMass(getMolecule(x))   )
{% endhighlight %}



{% highlight text %}
## Error in lapply(X = X, FUN = FUN, ...): object 'formulas' not found
{% endhighlight %}



{% highlight r %}
predret_db <- cbind.data.frame(predret_db, mz_pos = masses + 1.0073)
{% endhighlight %}



{% highlight text %}
## Error in data.frame(..., check.names = FALSE): object 'predret_db' not found
{% endhighlight %}


<br>

We can then split the database in two. One for the experimental RTs and one for the predicted. Here I have used some pipe/dplyr style code and even a forward assign. If you are not familiar with this type of R code I urge you to look into it. It really makes code much more readable.


{% highlight r %}
library(dplyr)
predret_db %>% filter(!is.na(recorded_rt)) -> predret_db_exp
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'predret_db' not found
{% endhighlight %}



{% highlight r %}
predret_db %>% filter(is.na(recorded_rt))  -> predret_db_pred
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'predret_db' not found
{% endhighlight %}


<br>

## Annotating a dataset

We now have the database ready for annotation. <br>
So we can load a dataset/peaklist. This peaklist was previously created with XCMS and fragments/adducts annotated with CAMERA. But again any peaklist will do.


{% highlight r %}
library(readxl)
{% endhighlight %}



{% highlight text %}
## Error in library(readxl): there is no package called 'readxl'
{% endhighlight %}



{% highlight r %}
data <- read_excel("../material/data/peaklist_pos.xlsx") %>% 
        replace(is.na(.), "") %>% 
        as.data.frame
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): could not find function "read_excel"
{% endhighlight %}

<br>
Lets take a look at the interesting columns we have in the dataset.

{% highlight r %}
info_cols <- c("mz","rt","isotopes","adduct","pcgroup")
dim(data)
{% endhighlight %}



{% highlight text %}
## NULL
{% endhighlight %}



{% highlight r %}
head(    data[,info_cols]    )
{% endhighlight %}



{% highlight text %}
## Error in data[, info_cols]: object of type 'closure' is not subsettable
{% endhighlight %}

<br>
Now we can use db.comp.assign from my [chemhelper](https://github.com/stanstrup/chemhelper) package to annotate the dataset. <br>
We would probably want one column in our peaklist for the RTs we have determined experimentally and one for the predicted RTs. So we do the annotation twice. <br>
The first two arguments to the function are the *m/z* and RT of the dataset. The next three are the name, *m/z* and RT of the database of known compounds. Lastly we give the tolerance for the *m/z* and RT for a database match.



{% highlight r %}
library(chemhelper)
{% endhighlight %}



{% highlight text %}
## Error in library(chemhelper): there is no package called 'chemhelper'
{% endhighlight %}



{% highlight r %}
anno_exp <- db.comp.assign(mz           = data[,"mz"],
                           rt           = data[,"rt"],
                           comp_name_db = predret_db_exp[,"name"],
                           mz_db        = predret_db_exp[,"mz_pos"],
                           rt_db        = predret_db_exp[,"recorded_rt"] *60, # *60 since XCMS works in seconds but PredRet is in minutes.
                           mzabs        = 0.01,
                           ppm          = 15,
                           ret_tol      = 10
                           )
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): could not find function "db.comp.assign"
{% endhighlight %}



{% highlight r %}
anno_pred <- db.comp.assign(mz          = data[,"mz"],
                           rt           = data[,"rt"],
                           comp_name_db = predret_db_pred[,"name"],
                           mz_db        = predret_db_pred[,"mz_pos"],
                           rt_db        = predret_db_pred[,"predicted_rt"] *60,
                           mzabs        = 0.01,
                           ppm          = 15,
                           ret_tol      = 10
                           )
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): could not find function "db.comp.assign"
{% endhighlight %}


<br>
Now lets put the annotations together with our dataset.

{% highlight r %}
data_annotated <- cbind.data.frame(data,anno_exp,anno_pred)
{% endhighlight %}



{% highlight text %}
## Error in data.frame(..., check.names = FALSE): object 'anno_exp' not found
{% endhighlight %}


<br>

## The result

Then lets take a look at one of the feature groups (from CAMERA) where we got an annotation. In this example we have a feature that was annotated as tryptophan. The "OR" is because tryptophan was in the database several times. If multiple compounds would fit the *m/z* and RT they would be written with "OR" between them. <br>
There is also a fragment annotated as adipic acid and 2-methylglutaric acid using a hit from the predicted RTs. In this case we have almost perfect CAMERA annotation suggesting the pseudo-molecular ion is the *m/z* = 205.0979 feature and the compound is very likely tryptophan.

{% highlight r %}
data_annotated %>% filter(pcgroup==16) %>% select(one_of(info_cols,"anno_exp","anno_pred"))
{% endhighlight %}


{% highlight text %}
## Error in eval(expr, envir, enclos): object 'data_annotated' not found
{% endhighlight %}


<br>
Lets take a look at another feature. This time we have experimental RTs that say the feature is either 1,7-dimethylxanthine OR theobromine but a prediction from the PredRet database also suggest that the feature could be theophylline as well.


{% highlight r %}
data_annotated %>% filter(pcgroup==400) %>% select(one_of(info_cols,"anno_exp","anno_pred"))
{% endhighlight %}


{% highlight text %}
## Error in eval(expr, envir, enclos): object 'data_annotated' not found
{% endhighlight %}


<br>
That's it!
