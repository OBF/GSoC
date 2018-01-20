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

## Taking the <i>fastest sequence transforming software in the world</i> to the next level

In 2012 we created [sambamba](https://github.com/biod/sambamba) as the
fastest software that could parse and transform different file formats
as coming out of a sequencer. Sambamba is used today as time critical
software for analysing all types of DNA data, for example in the
context of plant research and human disease diagnostics. Sequencing is
a rapidly growing effort involving more and more researchers - we want
to make sambamba even faster and support columnar data storage such as
provided by [Parquet](http://parquet.apache.org/) - similar to what
Google uses for large data. Sambamba is written in D and C++. D is a
perfect fit for writting performant code in a high-level programming
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
[Spark dataframe](https://spark.apache.org/docs/latest/sql-programming-guide.html)
into Python, R, or Scala, thus providing easy scaling.

The provided BAM → ADAM converter is rather slow, taking about half an
hour (8 threads) to convert a 10GB BAM file. This is a barrier for
adoption: for comparison, recompressing the same file with sambamba
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
sambamba codebase, and all the libraries involved. After that the
writing codepath can be added.  Optionally, filtering in the reader
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

* This is <span class="hard">challenging</span> project for someone
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
* <span class="medium">medium</span> mostly PureScript and JavaScript, but Python and Elixir may come in handy

#### Mentors
[Christian Fischer](https://github.com/chfi/), [Pjotr Prins](https://github.com/pjotrp), [Danny Arends](https://github.com/dannyarends) and [Karl Broman](https://github.com/kbroman)

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

<span class="medium">medium</span>

#### Mentors

[Julian Mazzitelli][thejmazz], [Bruno Vieira][bmpvieira], [Max Ogden][maxogden], [Mathias Buus][mafintosh]

[thejmazz]: https://github.com/thejmazz
[maxogden]: https://github.com/maxogden
[mafintosh]: https://github.com/mafintosh
[bmpvieira]: https://github.com/bmpvieira


#### Contact

- [gitter](https://gitter.im/bionode/bionode)
