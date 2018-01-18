---
layout: page
title: Project Ideas
permalink: /ideas/
---

# Google Summer of Code 2018 Project ideas

The details of each of our project ideas are listed below, including potential
mentors. Interested mentors and students should subscribe to the OBF/GSoC
mailing list and announce their interest.

See the [main OBF Google Summer of Code page](../) for more information about the GSoC
program and additional ways to get in touch with us.


#### Quick links

* Table of Contents
{:toc}

## Cross-project ideas

OBF is an umbrella organization which represents many different programming
languages used in bioinformatics. In addition to working with each of the
"Bio\*" projects (listed below), this year we are also accepting a category of
"cross-project" ideas that cover multiple programming languages or projects.
These collaborative ideas are broadly defined and can be thought of as
"unfinished" — interested students should adapt the ideas to their own
strengths and goals, and are responsible for the quality of the final proposed
idea in their application.

**Feel free to propose your own entirely new idea.**

## Integration of CWL support into StackStorm automation framework

### Rationale

The needs of a DNA sequencing centre are several and varied: from heavy High Performance Computing (HPC) workloads over sample tracking via Laboratory Information Management Systems (LIMS) to the automation of common data and centre management tasks.

Due to it's high requirements on compute infrastructure and complexity, the data analysis part usually receives the lion share of attention when it comes to IT resources. However, the other, less exciting, tasks should not be forgotten and can add up to become a real bottleneck if not automated sufficiently.

We at the [University of Melbourne Centre for Cancer Research (UMCCR)][umccr] employ the help of tools like the [Arteria][arteria] project and the underlying automation platform [StackStorm][stackstorm], in order to streamline our data management tasks. We are also heavily relying on existing and established data analysis pipelines for the heavy computational tasks. However, those two worlds remain still mainly disconnected.

We would love to see the integration of the data analysis pipelines with the rest of our data/centre management pipelines and tasks. This would allow us to automate and streamline the whole data lifecycle and data governance, from generation on the sequencing machines over heavy computing on HPC/cloud environments to final dissemination and archival tasks, including full data provenance.

### Approach

StackStorm is a powerful open-source platform that provides an event-driven, integrated automation solution for several aspects of an organisational infrastructure. It already supports several workflow systems and can wire together tools, services and workflows. The Arteria project is already publishing convenience tasks and workflows for sequencing centres based on this powerful platform.

The [Common Workflow Language](http://www.commonwl.org/user_guide/) (CWL) is gaining popularity as a future proof standard for describing analysis workflows and tools in a way that makes them portable and scalable across a variety of software and hardware environments in the fields of data-intensive science, such as Bioinformatics, Medical Imaging, Astronomy, Physics, and Chemistry and several major workflow engines such as [Cromwell][cromwell], [Toil][toil], [Arvados][arvados], [Galaxy][galaxy], [Taverna][taverna] and others have started to adopt it.

We propose the combination of both systems: the integration of CWL support into the StackStorm automation platform.

### Steps

* Investigate existing workflow integrations (ActionChain, Mistral, CloudSlang) as template for CWL integration
* Investigate jinja integration (see existing integrations) to dynamically configure CWL templates
* Create st2 workflow runner (execute CWL workflow against configured cwl_runner)
* Start with Cromwell as workflow execution engine/cwl_runner
* (advanced) investigate workflow engine integration/interfacing (use of GA4GH WES API)

#### Questions about StackStorm
* How does it model the compute and storage resources?
    * It doesn't, you just define: triggers, actions and rules.
      * So we'll need to embed a complete workflow system, invoked via cwl-runner or WES.
          * More like [wrapping it under `st2/contrib/runners`](https://github.com/StackStorm/st2/tree/42136926ed2566d49856a24961a27c3993660ac8/contrib/runners) and luckily there are several existing examples.
* Does StackStorm have a scheduler?
    * Ish, internal one to manage the events/jobs: https://keepingitclassless.net/2017/08/stackstorm-architecture-core-services/
* Can a user dynamically add new workflows, or is it more static like AirFlow?
    * The user can define so-called "packs" which bundle the aforementioned triggers/actions/rules. Examples of packs contributed by the community: https://github.com/StackStorm-Exchange. Then the pack can just be installed, don't have much experience with AirFlow, but I would say that this aspect would be similar to Galaxy installing tool/workflow XMLs.

### Language and skills

* Python
* Common Workflow Language
* YAML

### Difficulty

Medium

### Mentors

Florian Reisinger, Oliver Hofmann, Michael Crusoe, Anton Khodak, Roman Valls Guimera



[stackstorm]: https://stackstorm.com/
[cromwell]: https://github.com/broadinstitute/cromwell
[toil]: https://github.com/BD2KGenomics/toil
[arvados]: https://github.com/curoverse/arvados
[cwl]: http://www.commonwl.org/
[stackstorm_runners]: https://github.com/StackStorm/st2/tree/42136926ed2566d49856a24961a27c3993660ac8/contrib/runners
[galaxy]: https://usegalaxy.org/
[taverna]: https://taverna.incubator.apache.org/
[umccr]: https://umccr.github.io/
[arteria]: https://arteria-project.github.io/


## OpenMS

[OpenMS](www.openms.de) is an open-source software C++ library for LC/MS data management and analyses. It offers an infrastructure for the rapid development of mass spectrometry related software. OpenMS is free software available under the three clause BSD license and runs under Windows, MacOSX and Linux. The source code is hosted publicly available on [GitHub](https://github.com/OpenMS/OpenMS/).

### Improve Posterior Error Probability estimation for peptide search engine results

#### Rationale

Mass spectrometry has become one of the bioanalytical tools of choice for many life scientists. Technological advancements in the last years have led to an increase in acquisition speed and resolution. Common tasks, like identifying and quantifying proteins and metabolites from biological or medical samples are regularly performed in different fields of research, industry, and clinical diagnostics.

A crucial part in proteomics is to control the uncertainty in peptide identifications generated by peptide-spectrum matching based search engines that compare spectra against the theoretical spectra of valid peptide candidates. Since most spectra contain noise or even fragments of multiple peptides it is important to quantify the confidence in a particular peptide-spectrum match. Although there are scoring mechanisms implemented in the different search engines, most of them are based on empirical criteria such as number of overlapping peaks. To bring them all in a common mathematical measure, techniques arose that calculate a probability for a correct match based on the score distributions.

#### Approach

OpenMS currently includes a very simple expectation-maximization algorithm to fit a two-component Gaussian mixture to the aforementioned
score distributions (of a single search engine score). There are issues with such a simple approach: numerical instabilities, bad quality of fit, no user feedback, etc.

Several papers have been published that describe implementations of more elaborate methods, e.g.:
[PeptideProphet](https://www.ncbi.nlm.nih.gov/pubmed/12403597) (and its extensions) as well as 
[curveFDP](http://pubs.acs.org/doi/abs/10.1021/ac902892j)

A good review with pseudocode for PeptideProphet can be found [here](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3489532/).

for which reference implementations or pseudocode can be found. They could be potentially interesting algorithms that can be validated against a reference implementation.

OpenMS tool developers and users alike would benefit from well-tested, native implementations using the OpenMS library. It would directly
impact the quality of the IDPosteriorErrorProbability tool and all subsequent tools that use the estimated probabilities.

#### Languages and skills

* Intermediate knowledge of C++ and its STL. Knowledge of Boost's Math Library might be of use.
* Depending on the implemented algorithm, intermediate knowledge on statistics (in particular deeper knowledge in one or more of the following would be a plus: mixture models, maximum likelihood estimation, optimization, expectation-maximization algorithm, kernel density estimation)
* Basic knowledge on peptide search engines and target-decoy approaches (can be acquired in the first days).
* Basic knowledge on mass spectrometry (can be acquired in the first days).

#### Code

Expected outcome:
The existing implementation for posterior error probability estimation in OpenMS ([IDPosteriorErrorProbability]( https://github.com/OpenMS/OpenMS/blob/develop/src/topp/IDPosteriorErrorProbability.cpp)) should be improved by a more stable and
hopefully better performing implementation (e.g. based on the suggested references) by combining different scores of a search engine, using semi-supervised, semi-parametric or dynamically adapting fitting algorithms. Additionally user feedback could be improved to tell users about the quality of fit.

#### Difficulty
<span class="easy">medium</span>.

#### Mentors
[Timo Sachsenberg](https://github.com/timosachsenberg), [Julianus Pfeuffer](https://github.com/jpfeuffer)
