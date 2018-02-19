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

## Common Workflow Language

### Integration of CWL support into StackStorm automation framework

#### Rationale

The needs of a DNA sequencing centre are several and varied: from heavy High Performance Computing (HPC) workloads over sample tracking via Laboratory Information Management Systems (LIMS) to the automation of common data and centre management tasks.

Due to it's high requirements on compute infrastructure and complexity, the data analysis part usually receives the lion share of attention when it comes to IT resources. However, the other, less exciting, tasks should not be forgotten and can add up to become a real bottleneck if not automated sufficiently.

We at the [University of Melbourne Centre for Cancer Research (UMCCR)][umccr] employ the help of tools like the [Arteria][arteria] project and the underlying automation platform [StackStorm][stackstorm], in order to streamline our data management tasks. We are also heavily relying on existing and established data analysis pipelines for the heavy computational tasks. However, those two worlds remain still mainly disconnected.

We would love to see the integration of the data analysis pipelines with the rest of our data/centre management pipelines and tasks. This would allow us to automate and streamline the whole data lifecycle and data governance, from generation on the sequencing machines over heavy computing on HPC/cloud environments to final dissemination and archival tasks, including full data provenance.

#### Approach

StackStorm is a powerful open-source platform that provides an event-driven, integrated automation solution for several aspects of an organisational infrastructure. It already supports several workflow systems and can wire together tools, services and workflows. The Arteria project is already publishing convenience tasks and workflows for sequencing centres based on this powerful platform.

The [Common Workflow Language](http://www.commonwl.org/user_guide/) (CWL) is gaining popularity as a future proof standard for describing analysis workflows and tools in a way that makes them portable and scalable across a variety of software and hardware environments in the fields of data-intensive science, such as Bioinformatics, Medical Imaging, Astronomy, Physics, and Chemistry and several major workflow engines such as [Cromwell][cromwell], [Toil][toil], [Arvados][arvados], [Galaxy][galaxy], [Taverna][taverna] and others have started to adopt it.

We propose the combination of both systems: the integration of CWL support into the StackStorm automation platform.

#### Steps

* Investigate existing workflow integrations (ActionChain, Mistral, CloudSlang) as template for CWL integration
* Investigate jinja integration (see existing integrations) to dynamically configure CWL templates
* Create st2 workflow runner (execute CWL workflow against configured cwl_runner)
* Start with Cromwell as workflow execution engine/cwl_runner
* (advanced) investigate workflow engine integration/interfacing (use of GA4GH WES API)

##### Questions about StackStorm
* How does it model the compute and storage resources?
    * It doesn't, you just define: triggers, actions and rules.
      * So we'll need to embed a complete workflow system, invoked via cwl-runner or WES.
          * More like [wrapping it under `st2/contrib/runners`](https://github.com/StackStorm/st2/tree/42136926ed2566d49856a24961a27c3993660ac8/contrib/runners) and luckily there are several existing examples.
* Does StackStorm have a scheduler?
    * Ish, internal one to manage the events/jobs: https://keepingitclassless.net/2017/08/stackstorm-architecture-core-services/
* Can a user dynamically add new workflows, or is it more static like AirFlow?
    * The user can define so-called "packs" which bundle the aforementioned triggers/actions/rules. Examples of packs contributed by the community: https://github.com/StackStorm-Exchange. Then the pack can just be installed, don't have much experience with AirFlow, but I would say that this aspect would be similar to Galaxy installing tool/workflow XMLs.

#### Language and skills

* Python
* Common Workflow Language
* YAML

#### Difficulty

{% include difficulty.html difficulty="medium" %}

#### Mentors

[Sehrish Kanwal](https://github.com/skanwal), [Florian Reisinger](http://github.com/reisingerf), [Oliver Hofmann](http://github.com/ohofmann), [Michael Crusoe](http://github.com/mr-c), [Anton Khodak](https://github.com/anton-khodak), [Roman Valls Guimera](http://github.com/brainstorm)



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
{% include difficulty.html difficulty="medium" %}

#### Mentors
[Julianus Pfeuffer](https://github.com/jpfeuffer), [Timo Sachsenberg](https://github.com/timosachsenberg), [Oliver Alka](https://github.com/oliveralka)

### Improve Visualization of Spectra and Analysis Results in GUI Tool (TOPPView)

#### Rationale
Mass spectrometry has become one of the bioanalytical tools of choice for many life scientists. For the analysis of individual spectra, visualization is the key to perform and validate annotations and optimize data processing workflows. 

#### Approach
The OpenMS visualization tool TOPPView offers a wide range of possibilities to visualize raw data and analysis results. In this GSoC project, we intend to improve TOPPView improve overall user experience by adding requested features, e.g., introducing a visualization widget for protein sequence coverage from identification results, adding visualization of chromatograms, and an improved spectrum comparison widget.
OpenMS tool developers and users alike would benefit from these improvements.

#### Languages and skills
* Intermediate knowledge of C++ and its STL.
* Basic knowledge of Qt and Qt Widgets (Qt4 and Qt5).
* Interest or experience in working on GUI implementations
* Basic knowledge of mass spectrometric terms and concepts (can be acquired in the first days).

#### Code
Expected outcome:
The TOPPView implementation should be extended to improve the the general user experience. This could include the creation of widgets for the visualization of chromatograms, an improved spectrum comparison and annotation facility, and a viewer for protein coverage.

#### Difficulty
{% include difficulty.html difficulty="medium" %}

#### Mentors
[Oliver Alka](https://github.com/oliveralka), [Timo Sachsenberg](https://github.com/timosachsenberg), [Julianus Pfeuffer](https://github.com/jpfeuffer)


## Sambamba

### Taking the <i>fastest sequence transforming software in the world</i> to the next level

In 2012 we created [sambamba](https://github.com/biod/sambamba) as the
fastest software that could parse and transform different file formats
as coming out of a sequencer. Sambamba is used today as time critical
software for analysing all types of DNA data, for example in the
context of plant research and human disease diagnostics. Sequencing is
a rapidly growing effort involving more and more researchers - we want
to make sambamba even faster and support columnar data storage such as
provided by [Parquet](http://parquet.apache.org/) - similar to what
Google uses for large data. Sambamba is written in D and C++. D is a
perfect fit for writing performance code in a high-level programming
language.

#### Rationale

Sambamba already supports multiple file formats. Current work is on
making sambamba more composable. Instead of having split sorting,
filtering and marking steps we will combine them into one run of the
tool.

[BAM](http://samtools.github.io/hts-specs/) is the most popular file
format for storing sequence alignments, but it has some disadvantages
(no support for modern light compression, row-based storage). CRAM is
another format supported by Sambamba. CRAM files have higher
compression, but are slower in processing.

[Adam](https://github.com/bigdatagenomics/adam) or Parquet columnar
format can give both high compression and fast processing.  It can be
also be used as a
[Spark data-frame](https://spark.apache.org/docs/latest/sql-programming-guide.html)
into Python, R, or Scala, thus providing easy scaling.

The provided BAM → ADAM converter is rather slow, taking about half an
hour (8 threads) to convert a 10GB BAM file. This is a barrier for
adoption: for comparison, re-compressing the same file with sambamba
(BAM → BAM) using 8 threads takes only about 5 minutes.

Faster conversion speed is not easily attainable on JVM platform,
partly because [htsjdk](https://github.com/samtools/htsjdk) BAM reader
is single-threaded and is known to be slow.  Sambamba, on the other
hand, provides a solid base for building a fast converter.

#### Approach

ADAM files can be rather easily read/written with the aid of
[parquet-cpp](https://github.com/apache/parquet-cpp) and
[avro](https://github.com/apache/avro) C/C++ libraries.

D has great support for interfacing with C and even
[some support](https://dlang.org/spec/cpp_interface.html) for C++.

First create D read support to familiarize with BAM and ADAM formats,
sambamba code base, and all the libraries involved. After that the
writing code path can be added.  Optionally, filtering in the reader
can be then enhanced by leveraging Parquet metadata and columnar
structure.

#### Languages and skill

The student should have an interest in using different programming
languages and functional programming techniques, but good knowledge of
C++ or similar is enough.

The deployment and programming environment will be handled by the
functional package manager
[GNU Guix](https://www.gnu.org/software/guix/) which can run on any
Linux distribution, including Ubuntu and Fedora.

#### Code

* [sambamba](https://github.com/biod/sambamba)
* [ADAM](https://github.com/bigdatagenomics/adam)

#### Difficulty

This is {% include difficulty.html difficulty="hard" text="challenging" %} project for someone
who wants to be a hard core coder! Successfully completing this
project will give a lot of credibility when looking for a job in
science.

#### Mentors

[Pjotr Prins](https://github.com/pjotrp),
[Artem Tarasov](https://github.com/lomereiter).

We will also ask James Bonfield (htslib) and one of the ADAM authors
to help mentor.

## GeneNetwork PureScript Genome Browser (partly Biodalliance)

[GeneNetwork.org](http://gn2.genenetwork.org/) (GN) is a Web 2.0 environment for genetic analysis in mouse, rat and human (QTL mapping and GWAS). GN is used daily by scientists with over a thousand publications citing it.

In the context of GeneNetwork we have developed a state-of-the-art embeddable [genetics browser in PureScript](https://github.com/chfi/purescript-genetics-browser), which can be run independently of a database and therefore embedded into publications. PureScript is a purely functional programming language that translates into JavaScript. The current code base was written by Christian Fischer, and started out as a Google Summer of Code project. The original idea of our browser is based on [Biodalliance.org](http://www.biodalliance.org/) (BD) and components thereof can be reused. BD is a fast, interactive, genome visualization tool that's easy to embed in web pages and applications. It supports integration of data from a wide variety of sources, and can load data directly from popular genomics file formats including bigWig, BAM, and VCF. Biodalliance has been adopted by some major bioinformatics websites including, for example, [UK10K](http://www.uk10k.org/dalliance.html).

#### Rationale

To improve user experience and biomedical discovery we are working on advanced genome visualisation and embedding the state-of-the-art [Biodalliance genome browser](http://www.biodalliance.org/) into GN with several new *tracks* for visualizing mapped QTL, underlying genotypes and SNP density. We are building on the current tooling to provide a full user experience and interactive tracks that can be embedded in online scientific journals. Example: ![Biodalliance](https://sagebionetworks.jira.com/secure/attachment/24449/biodalliance%20widget%20output.png)

#### Approach
The student will get acquainted with PureScript and community before GSoC starts. The work plan will target porting a few existing tracks from BD (e.g. gene track, sequencing reads track) to PureScript to increase insight in how it all hangs together. Thereafter a component will be built to navigate a graph of linked data items, for example using Cytoscape.js. These linked data items may refer to interactions between different elements on different tracks.

#### Languages and skill
The genetics browser is written in [PureScript](http://www.purescript.org/). A command of JavaScript, to read BD code, is recommended.

#### Code
* [PureScript browser](https://github.com/chfi/purescript-genetics-browser)
* [Genenetwork.org](https://github.com/genenetwork)
* [Biodalliance](https://github.com/dasmoth/dalliance)

#### Difficulty
{% include difficulty.html difficulty="medium" %} mostly PureScript and JavaScript, but Python and Elixir may come in handy

#### Mentors
[Christian Fischer](https://github.com/chfi/), [Pjotr Prins](https://github.com/pjotrp), [Danny Arends](https://github.com/dannyarends) and [Karl Broman](https://github.com/kbroman)


## Web services

### Add block chains and hyperledger support for the 'Journal of Open Data Publications'

#### Rationale

We are working on the next generation of scientific publications. The
publication workflow will be the engine behind our new journal 'The
Journal of Data Publications for the Web' (or similar). Unlike
existing publication workflows ours delivers machine readable
"journal" "linked-data" publications. We understand the publication
as an aggregation of versioned and addressable nanopublications that
coexist with the human narrative.  Instead of the publication
requiring curation and semantic annotation as a post publication
activity, we are delivering a publication that is to be born semantic
and thus interoperable with the web of data. More importantly, we
understand that publications are assets being created thought the
research life cycle; in order to keep a reliable track of assets and
transactions we are using Hyperledger, in order to facilitate and
encourage data exchange (reuse) and deliver addressable content we are
using the IPFS. In this way we are "notarizing" the assets beyond the
DOI in a decentralized P2P environment that ensures preservation and
allows us to account for everything that happens to the assets via
smart contracts.  Our publications are not limited to a narrative with
metadata, e.g.  paper-authors-tittle-abstract with the understanding
that machine procesability means layout processing. Over a simple UI
meant for authors to describe their work, we are generating linked
data and doing semantic mark up; also, we are making it simple for the
authors to declare the map of relations for their assets, i.e.,
manuscripts.

The publications have extensible distributed scholarly compounds,
DISCOs, thus generating for each publication a map of resources. Our
system goes beyond github because we don't rely on trackers for the
review or post publication process; instead, we consider the value in
the review and post publication as part of the map of resources and
also, more importantly, as part of the derivative assets created
pivoting on the original publication. Our P2P layer generates
consensus tokes for all activities derived from the publication
-e.g. review, editorial, post publication, followups, updates.

#### Approach

We use a Python based frame work (flask). We are using IPFS for
distributed file storage. The work plan should include a work package
for creating a simple submission system for providing a data link to
IPFS storage with a description. This information will be stored in
block chains using hyperledger and updated on modification. We already
have some prototypes in place. The student will execute the following

1. Get acquainted with hyperledger and IPFS (before GSoC!)
2. Update the YAJ code to allow submission of information (expand
   on existing simple issue tracker)
3. Embed the current hyperledger prototype in the yaj code base
4. Submit and publish publications through IPFS and hyperledger
5. Introduce a 'token' mechanism that people can give credit, e.g.,
   generate a citation
6. Simulate publications and generating tokens
7. Show stats page for citations belonging to a publication

In all, the idea is to create a working example of the mechanism of
distributed storage of publications, distributed and reproducible
tracking and access, distributed tokens for usage 'credit' and finally
metrics for how well a publication is doing. This principles will
later, probably after GSoC, be extended to other credits, e.g. for
review, for using a piece of data or software etc.

As this is a complex project that can be filled in in multiple ways,
the student is encouraged to write the work plan in close association
with below mentors. Don't wait until the last week.

#### Languages and skill

Requires Python web programming with an elastic search database and
hyperledger as a back-end. Some JavaScript may be necessary.

#### Code

* [JOSS](https://github.com/openjournals/joss)
* [Hyperledger]
* [IPFS]
* [Alex link]

#### Difficulty

{% include difficulty.html difficulty="medium" %} mostly Python for the
back-end and PureScript and JavaScript for the front-end.
Understanding of HTML and SQL may come in handy.

#### Mentors

[Alexander Garcia](https://github.com/alexgarciac),
[Pjotr Prins](https://github.com/pjotrp),
[Arfon Smith](https://github.com/arfon)

#### Contact

* IRC: `#genenetwork` on [Freenode](http://freenode.net/)
* Direct: alexgarciac at gmail


## BioJS

### Backend Website Student Project for BioJS


BioJS is a library of over one hundred JavaScript components enabling developers to visualize and process data using current web technologies. BioJS makes it easy for them to integrate their visualizations into their own website or web application. BioJS is a community that spans multiple countries and multiple high profile bioinformatics organisations.

#### Rationale

At the moment, BioJS has 2 websites that we would like to merge into one, [http://biojs.io](http://biojs.io)[http://biojs.net](http://biojs.net). We would like to merge and redesign the middleware/backend parts of the  two websites for easier maintenance and better performance for our international audience.
Currently the library at [http://biojs.io](http://biojs.io) is using a separate server to create the metadata to display in the library, and also providing the precomputed visualisations for the examples. We would like to simplify this process to make it easier to maintain.
We would also like to provide more DevOps infrastructure to ensure deployment of new servers is easier in the future.
If you like like to work on the middleware/backend development of an international, respected open source data visualisation bioinformatics code, this is your project.

#### Mentors

[Dennis Schwartz](https://github.com/DennisSchwartz),
[Yo Yehudi](https://github.com/yochannah),
[Rowland Mosbergen](https://github.com/rowlandm)

#### Difficulty

{% include difficulty.html difficulty="medium" %}

#### Goals
The primary goal is to:

* Create a new simplified middleware/backend website for BioJS
* Redesign the backend of the BioJS library visualisation pages ([http://biojs.io](http://biojs.io)) to improve speed for an international audience and reduce complexity
* Work with a flexible middleware web framework to interact with the new website front end and provide extensibility in the future
* Provide DevOps scripts to make deployments of infrastructure easier in the future
* Ensure that the BioJS website is reliable and maintainable

There is also a fair amount of flexibility with this project to allow the student to inject their own ideas and introduce new features and functionality.

#### Skills/Prerequisites

* Basic knowledge of Ansible/Javascript/CSS
* Ability to work independently and to report to a group and discuss theories and results
* Good analytical skills
* Basic git skills required as working with github is mandatory

#### Student Benefits

* We aim to ensure that each student gets a great learning experience tailored to their ability, interest and experience.
* Hands on experience in providing a major change to a web-based application that is used around the world.
* Practical experience in Ansible, Javascript and CSS for a software project that is used around the world
* Gain understanding of how real-world software is developed and how priorities are established
* Improving your oral and written communication skills in a team environment

#### How to Apply

* Provide a cover letter that explains why your skills would be a good fit. If you don’t have the skills, explain why you would like to learn those skills. 2 pages maximum.
* Provide a resume with a list of skills. 2 pages maximum.
* Provide links to any code you might have contributed to eg. github, bitbucket repos/commits
* If you have any questions, please ask us here - https://gitter.im/biojs/biojs


### Frontend Website Student Project for BioJS

BioJS is a library of over one hundred JavaScript components enabling developers to visualize and process data using current web technologies. BioJS makes it easy for them to integrate their visualizations into their own website or web application. BioJS is a community that spans multiple countries and multiple high profile bioinformatics organisations.

#### Rationale

At the moment, BioJS has 2 websites that we would like to merge into one, [http://biojs.io](http://biojs.io)[http://biojs.net](http://biojs.net). We would like to redesign the website but also retain some of the look and feel of previous websites. The final design should be consistent across the individual pages.
As BioJS is international in nature, optimising the front end experience to ensure a good user experience and responsiveness is key.
An example of the new design of a landing page is in this issue tracker: https://github.com/biojs/organisation/issues/4
If you like like to work on the middleware and front end development of an international, respected open source data visualisation bioinformatics code, this is your project.

#### Mentors

[Dennis Schwartz](https://github.com/DennisSchwartz),
[Yo Yehudi](https://github.com/yochannah),
[Rowland Mosbergen](https://github.com/rowlandm)

#### Difficulty

{% include difficulty.html difficulty="medium" %}

#### Goals

The primary goal is to:

* Create a new website front end landing page for BioJS
* Redesign the BioJS library page [http://biojs.io](http://biojs.io) to improve speed for an international audience
* Work with a flexible middleware web framework to house the new website front end and provide extensibility in the future
* Create pages to provide help and tutorials for the BioJS community

There is also a fair amount of flexibility with this project to allow the student to inject their own ideas and introduce new features and functionality.

#### Skills/Prerequisites

* Basic knowledge of Javascript/CSS
* Ability to work independently and to report to a group and discuss theories and results
* Good analytical skills
* Basic git skills required as working with github is mandatory

#### Student Benefits

* We aim to ensure that each student gets a great learning experience tailored to their ability, interest and experience.
* Hands on experience in providing a major change to a web-based application that is used around the world.
* Practical experience in Javascript and CSS for a software project that is used around the world
* Gain understanding of how real-world software is developed and how priorities are established
* Improving your oral and written communication skills in a team environment

#### How to Apply

* Provide a cover letter that explains why your skills would be a good fit. If you don’t have the skills, explain why you would like to learn those skills. 2 pages maximum.
* Provide a resume with a list of skills. 2 pages maximum.
* Provide links to any code you might have contributed to eg. github, bitbucket repos/commits
* If you have any questions, please ask us here - [https://gitter.im/biojs/biojs](https://gitter.im/biojs/biojs)

## Bionode

### Bionode workflow engine for streamed data analysis (bionode-watermill)

This project was started in 2016, continued in 2017, and looking for another
committed student! **The student will have a certain amount of developer
freedom in implementing project features, and will play a large role in
bringing this project to 1.0.**

#### Rationale

Researchers should be able to:

* Perform analyses while data are generated (i.e. with "data streams");
* Easily and rapidly update results if input data or analysis
  approaches/parameters/tools change (with minimal recomputation);
* Effortlessly change and scale underlying computing platforms while pipeline
  is running;
* Easily visualise results (e.g., interactive shell into working directory of a
  pipeline step, RStudio remote access).

This is difficult because current approaches were developed when datasets were
simpler and smaller. The student will take advantage of recent improvements in
generic analysis tools (Node.js Streams & asynchronous concurrency) to attain
the above objectives, as well as the recently completed CWL specifications.

See [NGS Workflows](https://jmazz.me/blog/NGS-Workflows) for a summary of other
workflow engines, illustrating some concerns bionode-watermill was built to
address.

#### Approach

The student will create a workflow engine for streamed data analysis with
concurrent pipelining. Julian Mazzitelli, the developer of bionode-watermill
will be available for discussions regarding code implementation, design
patterns of the existing project, and general programming aid. Max Ogden and
Mathias Buus, top Node.js contributors and founders of Dat-data.com, will
provide technical help with aspects related to streaming and JS. Bruno Vieira
(founder of Bionode.io) will co-supervise.

The student will incorporate the Common Worklflow Language (CWL) specification
into the project. This will entail implementing interoperability/validation
between bionode-watermill's `task` objects and CWL documents.

Some work on the data structures and programming interfaces for
commonly used data sources (e.g., NCBI, Uniprot, Ensembl/Biomart)
and data types (e.g., VCF, BAM, FASTQ) will be required.

The underlying computational architecture should be abstracted. This means that
analysis code will run identically using different traditional high performance
computing system (e.g., Torque, SGE) and modern systems (e.g., Hadoop
MapReduce). This could also be achieved by mapping the watermill pipeline spec
into a CWL/CWL workflow spec one, of which then other tools can run it.

#### Languages and skill

- JavaScript is a requirement (ES6, Promises, Observables is an asset)
- ReduxJS is an asset (the codebase is implemented with redux and sagas)
- Node.js core APIs (streams, files, http) is an asset
- Some biology knowledge is a plus (e.g. undergraduate biology courses, basic
  understanding of next generation sequencing pipelines)

#### Code

- [bionode-watermill](https://github.com/bionode/bionode-watermill)
- [bionode/gsoc16](https://github.com/bionode/gsoc16)
- [bionode/gsoc17](https://github.com/bionode/gsoc17)

#### Difficulty

{% include difficulty.html difficulty="medium" %}

#### Mentors

[Julian Mazzitelli][thejmazz], [Bruno Vieira][bmpvieira], [Max Ogden][maxogden], [Mathias Buus][mafintosh]

[thejmazz]: https://github.com/thejmazz
[maxogden]: https://github.com/maxogden
[mafintosh]: https://github.com/mafintosh
[bmpvieira]: https://github.com/bmpvieira


#### Contact

- [gitter](https://gitter.im/bionode/bionode)

## Stemformatics

### ISCANDAR integration Student Project

Stemformatics is an online portal that allows stem cell biologists to visually analyse and explore interesting datasets quickly and easily. It is a worldwide resource for collaborators in Australia, North America, Asia and Europe.

#### Rationale

One of the next big data visualisation challenges in biology is single cell RNASeq. Previously, RNASeq samples numbered in the 10s and sometimes 100s of samples. Now single cell RNASeq is in the 100s and 1000s of samples.

ISCANDAR is a stand alone tool for bioinformaticians to create an interactive single cell RNASeq report for biologists that was created in the Wells Lab and can be hosted inside Stemformatics. Currently to access a private ISCANDAR report relies on a separate username and password.

Stemformatics would like to be able to host private ISCANDAR and other types of reports as well as integrate the functionality of ISCANDAR into Stemformatics. Careful attention will be needed to make the integrated functionality look, feel and respond similarly to the rest of Stemformatics.

If you like to work on integrating and optimising applications for the web in a field that is very hot right now, this is your project.


#### Mentors

[Jarny Choi](https://github.com/jarny)

#### Difficulty

{% include difficulty.html difficulty="hard" %}

#### Goals
The primary goals are to:

* Provide an authentication between Apache and Pyramid (Python) web framework to host private reports without a .htaccess password
* Create a good user experience that allows people to use the functionality of ISCANDAR that is integrated into Stemformatics
* Make changes to the middleware that controls how genes and datasets are accessed
* Make changes to the database to allow for these changes
* Make changes to ensure the responsiveness of the integrated functionality is high

There is also a fair amount of flexibility with this project to allow the student to inject their own ideas and introduce new features and functionality.

#### Skills/Prerequisites

* Basic knowledge of Python/Javascript/CSS
* Ability to work independently and to report to a group and discuss theories and results
* Good analytical skills
* Working with git would be an advantage

#### Student Benefits

* We aim to ensure that each student gets a great learning experience tailored to their ability, interest and experience. You can read about it in our “Commitment to Students” document.
* Hands on experience in providing a major change to a web-based application that is used around the world.
* Practical experience in Apache, Python,  Javascript and CSS for a software project that is used around the world
* Potential to have your application used by others around the world who work in bioinformatics
* Gain understanding of how real-world software is developed and how priorities are established
* Improving your oral and written communication skills in a team environment

#### How to Apply

* Provide a cover letter that explains why your skills would be a good fit. If you don’t have the skills, explain why you would like to learn those skills. 2 pages maximum.
* Provide a resume with a list of skills. 2 pages maximum.
* Provide links to any code you might have contributed to eg. github, bitbucket repos/commits
* If you have any questions, please ask us here - https://gitter.im/stemformatics/Lobby


### S4M Module Development on HPCs

Stemformatics is an online portal that allows stem cell biologists to visually analyse and explore interesting datasets quickly and easily. It is a worldwide resource for collaborators in Australia, North America, Asia and Europe.

#### Rationale

Stemformatics has a large amount of datasets that biologists can benchmark
against their own datasets. To process these datasets though our pipeline,
Stemformatics has created the S4M framework. S4M is written in shell in a POSIX
compliant way.

The S4M framework consists of a series of modules that run bioinformatics
software to process these datasets. Stemformatics would like to expand the
modules to make them more automated, faster and more integrated with the main
Stemformatics website and Data Portal.

If you like to work on the backend and want to learn hardcore command line
skills, this is your project.


#### Mentors

[Othmar Korn](https://bitbucket.org/uqokorn/)


#### Difficulty

{% include difficulty.html difficulty="hard" %}

#### Goals

The primary goal is to add to the number of modules in S4M. Usually there are
one off scripts that have already been run on datasets that need to be made more
generic to fit into the S4M  architecture.

There is also a fair amount of flexibility with this project to allow the
student to inject their own ideas and introduce new features and functionality.

#### Skills/Prerequisites

* Basic knowledge of Linux, vim and bash scripting
* Ability to work independently and to report to a group and discuss theories
  and results
* Good analytical skills
* Working with git would be an advantage

#### Student Benefits

* We aim to ensure that each student gets a great learning experience tailored
  to their ability, interest and experience. You can read about it in our
  “[Commitment to
  Students](https://docs.google.com/document/d/1rs9IpTfJHpaQ95RLs78tiR70fBXZ-u51h0dxFF6ddac/edit?usp=sharing)”
  document.
* Hands on experience in providing command line, pipeline and module development
* Practical experience in Linux, vim and bash scripting for a software project
  that is used around the world
* Gain understanding of how real-world software is developed and how priorities
  are established
* Improving your oral and written communication skills in a team environment
* Potential opportunities to give presentations about the project to a wider
  audience

#### How to Apply

* Provide a cover letter that explains why your skills would be a good fit. If
  you don’t have the skills, explain why you would like to learn those skills. 2
  pages maximum.
* Provide a resume with a list of skills. 2 pages maximum.
* Provide links to any code you might have contributed to eg. github, bitbucket
  repos/commits
* If you have any questions, please ask us here -
  https://gitter.im/stemformatics/Lobby


### PHP Validator Migration and Ontology Integration

Stemformatics is an online portal that allows stem cell biologists to visually analyse and explore interesting datasets quickly and easily. It is a worldwide resource for collaborators in Australia, North America, Asia and Europe.

#### Rationale

The Stemformatics PHP validator was initially built 6 years ago in PHP as a stand alone application. It helps validate the samples that are annotated (described) by the biologist in Stemformatics. It needs to be migrated over to a Pylons/Pyramid Python web framework.

There is also an opportunity to work with the front end user interface. Stemformatics will need to allow users to annotate large volumes of metadata while still providing an ontology/validation system. Eg. 1500 samples need to be annotated in Stemformatics. These samples need to be annotated against a controlled vocabulary called an ontology.

If you like to work closely with clients and you are interested in building front-end, optimised solutions for complex processes, this is your project.


#### Mentors

[Isha Nagpal](https://bitbucket.org/ishanagpal/)


#### Difficulty

{% include difficulty.html difficulty="medium" %}

#### Goals

The primary goals are to:
* Migrate PHP code to a Stemformatics Pylons/Pyramid web framework
* Create unit tests and regression tests
* Provide a continuous integration environment via Jenkins or Travis
* Provide documentation around this work
* Provide ideas and a potential prototype around the front end user interface to account for large sample annotations
* Prototype a web application with the ideas provided previously


There is also a fair amount of flexibility with this project to allow the student to inject their own ideas and introduce new features and functionality.

#### Skills/Prerequisites

* Basic knowlege of PHP/Python/Javascript/CSS
* Ability to work independently and to report to a group and discuss theories and results
* Good analytical skills
* Working with git would be an advantage


#### Student Benefits

* We aim to ensure that each student gets a great learning experience tailored to their ability, interest and experience. You can read about it in our “[Commitment to Students](https://docs.google.com/document/d/1rs9IpTfJHpaQ95RLs78tiR70fBXZ-u51h0dxFF6ddac/edit?usp=sharing)” document.
* Hands on experience in providing a major change to a web-based application that is used around the world.
* Practical experience in Python, PHP, Javascript and CSS for a software project that is used around the world
* Gain understanding of how real-world software is developed and how priorities are established
* Improving your oral and written communication skills in a team environment
* Potential opportunities to give presentations about the project to a wider audience

#### How to Apply

* Provide a cover letter that explains why your skills would be a good fit. If you don’t have the skills, explain why you would like to learn those skills. 2 pages maximum.
* Provide a resume with a list of skills. 2 pages maximum.
* Provide links to any code you might have contributed to eg. github, bitbucket repos/commits
* If you have any questions, please ask us here - https://gitter.im/stemformatics/Lobby

## antiSMASH

[antiSMASH](http://antismash.secondarymetabolites.org) is a tool to mine the
genomes of micro-organisms for biologically interesting gene clusters, so-called
secondary metabolites, to help find new antibiotics. It is a python-based  open
source tool that is developed at the Technical University of Denmark and Wageningen
University.

Project ideas around antiSMASH range from very close to applied biology to more
general software engineering projects.

### Improve gene cluster visualization (SVGene)

#### Rationale

antiSMASH generates a static HTML page report with prediction results for analysis runs.
This is the main UI used by the experimental biologists. To give an overview of the gene
cluster layout, antiSMASH uses the [SVGene](https://github.com/kblin/svgene) JavaScript library
to render gene cluster arrows as vector graphics. So far, this is a static SVG, with some
tooltip boxes added to provide the user with extra context.

SVGene is limited in multiple aspects:
* It can't deal with [introns](https://en.wikipedia.org/wiki/Intron) because it initially written for Bacteria.
* It would be nice to support zooming for large gene clusters.
* It doesn't deal well with multiple overlapping cluster border features

#### Approach

antiSMASH renders gene clusters using the [SVGene](https://github.com/kblin/svgene)
JavaScript library, which in turn is built on top of [D3.js](https://d3js.org/).
D3.js supports controls for pan and zoom that should be used for SVGene.
Gene cluster data for the HTML page is loaded from a JavaScript file included in the static
web page. Additional details should be displayed on a bigger zoom level if available, possibly
on separate tracks.

#### Languages and skill

SVGene is written in JavaScript and making heavy use of the [D3.js](https://d3js.org/)
library for drawing the SVG primitives.
Some Python knowledge might make it easier to extend antiSMASH's precalculated output,
but is not required, as mock inputs can be used for the project.

#### Code
* [antiSMASH on Bitbucket](https://bitbucket.org/antismash/antismash)
* [SVGene on github](https://github.com/kblin/svgene)

#### Difficulty
* {% include difficulty.html difficulty="easy" %} with previous knowledge of D3.js
* {% include difficulty.html difficulty="medium" %} otherwise

#### Mentors
[Kai Blin](https://github.com/kblin), Simon Shaw

## openCOBRA - COBRApy

[openCOBRA](https://opencobra.github.io/) is an open-source, community-developed code base for COnstraint-Based Reconstruction and Analysis as is commonly used in metabolic modeling. A large part of that community is Python based and centered around the [COBRApy package](https://opencobra.github.io/cobrapy) which provides the basis for many other packages within that [community](https://opencobra.github.io/cobrapy/packages). The project ideas presented here show case some of the ways that the tools for the Python community can be improved and cover a diverse set of skills. If you can identify other unmet needs, feel free to contact us and discuss your ideas.

#### Contact

Please get in touch via the [mailing list](http://groups.google.com/group/cobra-pie) and/or our [gitter channel](https://gitter.im/opencobra/cobrapy).

### Publication Ready and Interactive Visualizations

#### Rationale

The genome-scale metabolic models investigated with constraint-based methods are
large, complex systems. The results of various methods typically contain
thousands to tens of thousands of values.

Developing a standard visualization tool that carefully highlights the most
important aspects of the simulation results will help communicate key findings
in a consistent manner that is easier to understand for everybody. Providing
high quality plots will further ease the publication process. Working with
interactive widgets in the browser-based Jupyter notebook will enable
researchers to dig deep into their data.

#### Approach

The results of various methods present in the community often come in the form
of [pandas](https://pandas.pydata.org/) data frames. The ability to easily and interactively inspect the visual information in, for example, widgets for the Jupyter notebook would vastly improve common workflows. Afterwards quickly turning those visuals into appealing plots for publication would further help alleviate pain points.

#### Languages and skill

* Familiarity with one or more plotting libraries is a plus.
* Some knowledge of Javascript in order to work with Jupyter widgets will be
  required.
* Some knowledge of pandas and Python coding will be helpful.

#### Code

* [COBRApy](https://github.com/opencobra/cobrapy)

#### Difficulty

* {% include difficulty.html difficulty="easy" text="Easy" %} with previous knowledge of plotting in
  Python and Jupyter notebooks;
* {% include difficulty.html difficulty="medium" %} otherwise.

#### Mentors

[Moritz Beber](https://github.com/Midnighter), [Nikolaus Sonnenschein](https://github.com/phantomas123)

### Method Implementation

#### Rationale

[COBRApy](https://opencobra.github.io/cobrapy) was first published in 2013 and
since then many new methods have been developed as well as new sub-areas of interest opened up. Examples for new areas include community modeling, thermodynamics-based constraints, and generally more data-driven modeling.

#### Approach

Based on the skill and interest of the applicant the outcome of this project
will be: addition of methods to the existing [COBRApy package](https://github.com/opencobra/cobrapy), implementation of standalone packages built on top of cobrapy, or enhancement of using experimental data with metabolic models.

#### Languages and skill

* Knowledge in Python programming is a must.
* Familiarity with constraint-based optimization is a big bonus.

#### Code

* [COBRApy](https://github.com/opencobra/cobrapy)
* [driven](https://github.com/biosustain/driven)

#### Difficulty

* {% include difficulty.html difficulty="medium" text="Medium" %} with good knowledge of
  Python and optimization problem formulation;
* {% include difficulty.html difficulty="hard" text="very hard" %} otherwise.

#### Mentors

[Moritz Beber](https://github.com/Midnighter), [Nikolaus Sonnenschein](https://github.com/phantomas123)

