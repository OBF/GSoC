---
layout: page
title: Project Ideas
permalink: /ideas/
---

# Google Summer of Code 2017 Project ideas

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
"Bio*" projects (listed below), this year we are also accepting a category of
"cross-project" ideas that cover multiple programming languages or projects.
These collaborative ideas are broadly defined and can be thought of as
"unfinished" — interested students should adapt the ideas to their own
strengths and goals, and are responsible for the quality of the final proposed
idea in their application.

**Feel free to propose your own entirely new idea.**

## GeneNetwork Genome Browser (biodalliance)

[GeneNetwork.org](http://gn2.genenetwork.org/) (GN) is a Web2.0
environment for genetic analysis in mouse, rat and human (QTL mapping
and GWAS). GN is used daily by scientists with over a thousand
publications citing it.

[Biodiallance.org](http://www.biodalliance.org/) is a state-of-the-art
Javascript genome browser. It is a fast, interactive, genome
visualization tool that's easy to embed in web pages and
applications. It supports integration of data from a wide variety of
sources, and can load data directly from popular genomics file formats
including bigWig, BAM, and VCF. Biodiallance has been adopted by some
major bioinformatics websites including, for example,
[UK10K](http://www.uk10k.org/dalliance.html).

#### Rationale

To improve user experience and improve biomedical discovery we are
improving advanced genome visualisation and embedding the
state-of-the-art [biodiallance genome
browser](http://www.biodalliance.org/) into GN with several new
*tracks* for visualizing mapped QTL, underlying genotypes and SNP
density.

![Biodalliance](https://sagebionetworks.jira.com/secure/attachment/24449/biodalliance%20widget%20output.png)

#### Approach

BioDiallance has good abstractions for tracks and fetching data. We
will add fetching data on-the-fly from GN backends through a
REST interface and/or cache locally. Also we will add interaction that
when a user
[clicks on a QTL](http://kbroman.org/qtlcharts/example/iplotScanone.html),
for example, the browser can display additional information and even
initiate some back-end processing.

We will use continuous
[open channels](http://www.phoenixframework.org/) between the browser
and the backend.

#### Languages and skill

Biodiallance is written in Javascript and the latest tracks support
[PureScript](http://www.purescript.org/). GeneNetwork is mostly python
and Javascript.  The GN REST interface is written in Elixir.

#### Code

* [Genenetwork.org](https://github.com/genenetwork)
* [Biodalliance](https://github.com/dasmoth/dalliance)

#### Difficulty
* <span class="medium">medium</span> mostly PureScript and Javascript, but python and elixir may come in handy

#### Mentors

[Pjotr Prins](https://github.com/pjotrp), [Danny Arends](https://github.com/dannyarends)  and
[Karl Broman](https://github.com/kbroman)

#### Contact

* IRC: `#genenetwork` on [Freenode](http://freenode.net/)
* [Mailing list GeneNetwork](http://listserv.uthsc.edu/mailman/listinfo/genenetwork-dev)
* [Mailing list Biodalliance](https://groups.google.com/forum/#!forum/biodalliance-dev)
* Direct: pjotr.public345 at thebird.nl
