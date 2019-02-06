---
layout: page
title: Project Ideas
permalink: /ideas/
---

# Google Summer of Code 2019 Project ideas

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
"Bio\*" projects (listed below) we also accept
"cross-project" ideas that cover multiple programming languages or projects.
These collaborative ideas are broadly defined and can be thought of as
"unfinished" — interested students should adapt the ideas to their own
strengths and goals, and are responsible for the quality of the final proposed
idea in their application.

**Feel free to propose your own entirely new idea.**

## Add Variant Graph (VG) support to BioD

BioD is a programming language that has the performance of C/C++ but
with improved high-level programming constructs for parallel
computing. In this project we want to add variant graph support that
can be used for novel algorithms by porting and improving the existing
[C++ code base](https://github.com/vgteam/vg).

#### Rationale

#### Approach

We'll take the existing [vg code base](https://github.com/vgteam/vg)
as the starting point. We may use the D redland bindings to hold graphs
in memory (RDF/semantic web).

#### Languages and skill

The student should have an interest in using different programming
languages and functional programming techniques, but good knowledge of
C++ or similar is enough.

The deployment and programming environment will be handled by the
functional package manager
[GNU Guix](https://www.gnu.org/software/guix/) which can run on any
Linux distribution, including Ubuntu and Fedora.

#### Code

* [BioD](https://github.com/biod)
* [Graph lib](http://librdf.org/)
* [D redland bindings](https://codereview.stackexchange.com/questions/212017/a-d-wrapper-around-c-library-librdf-code)
* [D package for semantic web](https://forum.dlang.org/thread/ghyrtlbybyxghnambffl@forum.dlang.org)

#### Difficulty

This is {% include difficulty.html difficulty="hard" text="challenging" %} project for someone
who wants to be a hard core coder!

#### Mentors

[Pjotr Prins](https://github.com/pjotrp),
[George Gitinji](https://github.com/george-githinji).

We will also ask Erik Garrison (VG) and Victor Porton (D redland bindings) to help mentor.

## Sambamba + BioD

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

[Christian Fischer](https://github.com/chfi/), [Pjotr Prins](https://github.com/pjotrp),
[Danny Arends](https://github.com/dannyarends) and [Karl Broman](https://github.com/kbroman)


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

### Create interactive Yeoman generator for BioJS components


BioJS is a library of over one hundred JavaScript components enabling developers to visualize and process data using current web technologies. BioJS makes it easy for them to integrate their visualizations into their own website or web application. BioJS is a community that spans multiple countries and multiple high profile bioinformatics organisations.

#### Rationale
Web standards have moved on a little since the [BioJS slush generator](https://github.com/biojs/slush-biojs) was created (ES2015 support has improved, as has support for WebComponents), so we're in the processes of updating the BioJS standard to version 3.0. We've created a scaffold wrapper tool to update older BioJS components to work as WebComponents, but we still have more features in mind. This task would involve updating the yeoman generator with options to create command-line based tools and brand new tools, as well as clearly documenting the process with tutorials. You can see the [BioJS 3.0 working draft](https://hackmd.io/j8y-Ht9_TP2yaDhYdUeIEQ#) for more information.

If you like like to work on the infrastructure of an international, respected open source data visualisation bioinformatics code, this is your project.

#### Mentors

- [Sarthak Sehgal](https://github.com/sarthak-sehgal)
- [Yo Yehudi](https://github.com/yochannah)

#### Difficulty

{% include difficulty.html difficulty="medium" %}

#### Goals
The primary goal is to:

* Create a fully-featured BioJS standard-compliant yeoman generator to allow people to generate the starter files for BioJS 3.0 tools easily.
* Fully documented tutorials for the generator, walking people through creating their first component.

There is also a fair amount of flexibility with this project to allow the student to inject their own ideas and introduce new features and functionality.

#### Skills/Prerequisites

* Basic knowledge of NodeJS/Javascript/HTML/CSS
* Ability to work independently and to report to a group and discuss theories and results
* Basic git skills required as working with github is mandatory

#### Student Benefits

* We aim to ensure that each student gets a great learning experience tailored to their ability, interest and experience.
* Hands on experience in providing a major change to a web-based application that is used around the world.
* Practical experience in NodeJS, Javascript, HTML and CSS for a software project that is used around the world
* Gain understanding of how real-world software is developed and how priorities are established
* Improving your oral and written communication skills in a team environment

#### How to Apply

* Provide a cover letter that explains why your skills would be a good fit. If you don’t have the skills, explain why you would like to learn those skills. 2 pages maximum.
* Provide a resume with a list of skills and experience. 2 pages maximum.
* Provide a breakdown of how you'd run this project - i.e. Features A, B delivered in the first two weeks, Features C, D delivered in later weeks. Show your proposal to mentors for feedback as they may be abe to suggest improvements!
* Provide links to any code you might have contributed to eg. github, bitbucket repos/commits
* If you have any questions, please ask us here - https://gitter.im/biojs/biojs


## antiSMASH

[antiSMASH](http://antismash.secondarymetabolites.org) is a tool to mine the
genomes of micro-organisms for biologically interesting gene clusters, so-called
secondary metabolites, to help find new antibiotics. It is a python-based  open
source tool that is developed at the Technical University of Denmark and Wageningen
University.

Project ideas around antiSMASH range from very close to applied biology to more
general software engineering projects.

### Redesign the antiSMASH submission page using web components and Redux

While antiSMASH can be installed and run as a command line tool, many users interact
with a cloud instance hosted at https://antismash.secondarymetabolites.org/.
This cloud instance provides a submission website that should be converted to
web components.

#### Rationale

We actuallly run multiple instances of the submission page, depending on whether
people want to analyse bacterial or fungal sequences, or run the production or
development version. Those sites are very similar, but differ slightly in what
features are offered. Currently this causes a lot of code duplication.

The goal of this project would be to redo the various submission pages using web
components to enable re-using the shared components between the different sites.

#### Approach

Individual components of the submission page should be identified and converted
into web components using LitElement and Typescript. All of the components
should be connected using a global event handling library like Redux.

All components should come with tests and appropriate build infrastructure.

#### Languages and skills
* Typescript
* LitHTML/LitElement
* Redux

#### Code
* [antiSMASH submission UI on github](https://github.com/antismash/bacterial-ui)

#### Difficulty
* {% include difficulty.html difficulty="easy" %}

#### Mentors
[Kai Blin](https://github.com/kblin), [Simon Shaw](https://github.com/SJShaw)


### Rework the antiSMASH web service infrastructure to be more robust

The antiSMASH web service allows users to submit microbial genomes for analysis.
Once their analysis job is finished, users are presented with a web page
displaying the results of the analysis job.

The antiSMASH web service is run on a collection of microservices that
communicate via a central Redis service, with data provided via a distributed
file system.

#### Rationale

The antiSMASH webapi service accepts job submissions from the antiSMASH webapp.
Job data can be uploaded by the user or can be downloaded from a third party
database. If data needs to be downloaded, the job is passed to a downloader
service. Once all data is present, the job gets passed to a dispatcher service
that in turn runs the antiSMASH software from a docker container.
 Currently this system is a bit fragile, and there are no automated
integration and end-to-end tests.

The goal of this project is to make the infrastructure more robust, make it
easier to spin up the complete set of services for testing, and build automated
integration and end-to-end tests.

#### Approach

End-to-end testing in a microservices setting is a difficult topic. Asa first
step, this project would evaluate available tools for building test
environments.

Once a good test framework is identified, end-to-end tests should be built.

Finally, issues identified during the testing concering the robustness of
the individual services should be fixed to get the overall system into a
healthier state.

#### Languages and skills
* Python 3
* Docker
* docker-compose

#### Code
* [antiSMASH webapi](https://github.com/antismash/websmash)
* [antiSMASH downloader](https://github.com/antismash/downloader)
* [antiSMASH dispatcher](https://github.com/antismash/dispatcher)

#### Difficulty
* {% include difficulty.html difficulty="medium" %}

#### Mentors
[Kai Blin](https://github.com/kblin), [Simon Shaw](https://github.com/SJShaw)
