---
title: 3PG/Q
author: Lorenzo Menichetti
output:
  bookdown::html_document2: default
bibliography: ../bibtex/library.bib
link-citations: yes
always_allow_html: yes
type: Checklist
modified: 2021-10-13T23:40:35+02:00
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

# The idea of 3PG/Q
This is an attempt to connect together the 3PGmix model, a well established tree growth model existing now in several branches described for example in the review by @Gupta2019, and in particular [3PGmix](https://sites.google.com/site/davidforresterssite/home/projects/3PGmix) with the decomposition model Q [@Agren1996b], in particular its updated calibration by #ECOSPHERE REFERENCE HERE#.
While 3PG will take care of simulating tree growth (CO2 sinks) Q will simulate decomposition processes (CO2 sources), closing the balance of the stand. A model such 3PG can consider interactions between trees and it is therefore suitable to describe stands more complex than uniform age and species, and it can therefore offer many possibilities for application in current century forestry.
```{r,, echo=FALSE, layout="l-page", fig.height=8, warning = FALSE, fig.cap = "A simplified diagram of the overall modeling approach"}
library(DiagrammeR)
grViz("images/model.gv")
```
One advantage of 3PGmix is that it is already developed for simulating uneven aged and multispecies stands.


## The Q model: main directions of future development
The model describes the decomposition of organic matter. It has so far been used to express the fate of all organic matter in the system, usually considering one decomposing cohort each time step and describing then its fate over time.
With the detailed inputs from 3PG we can describe separately different input sources. These are indeed likely to decompose with very similar kinetics, since decomposition kinetics seem to be rather constant and differences in different soils can be explained solely by the initial quality [@Menichetti2019], but nonetheless such assumption needs to be tested in the model both for different sites and different materials. It is possible for example that macronutrient balance (N and P) can have feedback on C decomposition. We will test if letting some key parameters of the model describing the kinetics will improve the simulation.
Another possibility we can add when representing separated decomposing pools is that, since these pools are defined just by spatial separation, we can introduce a transport term representing the movement of C from the litter to SOC (for example leaching or bioturbation).

So, summarizing the main differences this project wants to add compared to what is currently in use concerning Q:
*different inputs will be in different pools, each with its own starting quality
*we will test for separate kinetics for different inputs, which can be linked to nutrient status of the site and/or different inputs
*we will introduce a transport mechanism between litter and SOM

These modifications require extensive testing and studying them goes beyond the purpose of this very specific project, but we are going to set up the tools to test them in the future by designing the model from the beginning with the possibility for doing so.

The model could be used to simulate separate "pools" (with a different meaning than what commonly intended with compartmental SOC models, since here they do not denote different chemical qualities nor any different in recalcitrance) defined by their position. Each of them is going to be defined by a different initial input quality, due to the different originating material. The originating material comes from the 3PG simulation.
We can also test the possibility that even the kinetic terms, for example microbial growth, differ, and the initial assumption will be that these terms might differ between above-ground C and below-ground C due to different environments. This hypothesis will be tested and eventually the model will be simplified to represent only different cohorts if this degree of complexity will not be required.
The only topological reference between the "pools"

```{r,, echo=FALSE, layout="l-page", fig.height=4, warning = FALSE, fig.cap = "A simplified diagram of a possible division of the Q cohorts. Different cohorts are all described by different initial qualities, but the two boxes are also possibly described by different kinetic parameters"}
library(DiagrammeR)
grViz("images/Q.gv")
```


## Introducing 3PG
3PG, being physiologically based, is a rather complex model and needs many parameters (on top of fertility and climate corrections):
```{r, echo=FALSE}
parameters<-read.csv("i_parameters.csv")
knitr::kable(parameters, "pipe")
```


## Sensitivity analysis
The term "sensitivity analysis" is rather generic. In general it can refer either to the analysis of the impact of model parameters on the model predictions, or on the error of such predictions relatively to some dataset.
The sensitivity analysis we will employ is going to be based on the latter aspect. We will rely on the Hornberger-Spear-Young (HSY) sensitivity analysis as described in @Beven2008a, and we will consider the sensitivity of the error in predictions (defined as a fitness measurement) across the model parameter space.
For this initial model development phase we will base the sensitivity analysis on relatively uniform sites, so even aged and monospecific. These time series are easily available and we can rely therefore on more data points for the initial model definition.
The sensitivity analysis will be the first step of model calibration, and we will use it to define which parameters to focus on.

### Sites for sensitivity analysis and model calibration

## Model calibration

# Fertility
One of the key concepts in modeling forest stands is site ferility. Sweden is relying on what is called Site Index (SI) [@Hagglund1977].  This indicator is based on dominant height at a certain age (H100 ) and is determined empirically according to a dominant height curve, so based on actual productivity. Even if this index has been developed for uniform stands, it nevertheless offers a relatively good estimate of site fertility and a vast literature and data exist in this form. It is therefore important to develop a model able to utilize directly these data.
The fertility term in 3PG is a re-scaling of physiological tree functions and it has been determined according to various methodologies. In this initial model development phase we will develop a conversion between the two indexes by first calibrating the model on known sites, letting fertility be a part of the calibration, together with other parameters. We will obtain a calibration specific for each of the available forest sites, each of which will be associated with an already determined SI. We will then be able to study the relationship between 3PG fertility and SI, and develop a function to link the two (hopefully linear, but we can develop more advanced functions if needed).


## Future developments

# N interactions
Including N feedback on site fertility is going to represent an important tool for management. To do so we will (in future projects) add in the decomposition model Q the representation of N. We will then recalibrate the resulting model based on time series where there have been recorded variations in the available N, either through fertilization or through plant harvest.
This calibration should, in theory, make the model able to represent site fertility implicitly, solely as a consequence of its N balance.
This recalibration might require some model modifications, but not necessarily.


## Possible project impacts

# References

<div id="refs"></div>
