---
layout: page
title: Project Ideas
permalink: /ideas/
---

# Google Summer of Code 2016 Project ideas

The details of each of our project ideas are listed below, including potential
mentors. Interested mentors and students should subscribe to the OBF/GSoC
mailing list and announce their interest.

See the [main OBF Google Summer of Code page](../) for more information about the GSoC
program and additional ways to get in touch with us.

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


### Automated tool wrapper/converter for CWL

#### Rationale

The [Common Workflow Language](http://commonwl.org/) has so far defined a standard and a reference implementation to that standard, as opposed to the common practice of creating a system and then (not) trying to standardize it.

Defining [workflows](https://github.com/common-workflow-language/workflows) is a work in progress for CWL, but a more daunting task looms ahead of its adoption: wrapping tools.

Analogous to the packaging problem, we think that wrapping tools from already established systems such as Galaxy or Taverna is a task best done by machines. Unfortunately, there are no (automated) converters between those systems.

#### Approach

This project aims to solve part of that by taking [gxargparse](https://github.com/common-workflow-language/gxargparse), a proof of concept for the python tools command line ecosystem.

Internally, gxargparse, masquerading as argparse attempts to find and import the real argparse. 
It then stores a reference to the code module for the system argparse, and presents the user with all 
of the functions that stdlib argparse provides. Every function call is passed through the system argparse.

However, gxargparse captures the details of those calls and when a tool definition (Galaxy Tool XML in 
the case of the original code base) is requested, it builds up the tool definition according to community standards.

Another small proof of concept within the python ecosystem involves the docopt package and 
[rabixator](https://github.com/stefanristeski/rabixator). Furthermore, other similar instrumentation 
is being discussed to, for example, explore and optimize the parameter/flag space of i.e, bioinformatic
aligners with [Teaser](http://biorxiv.org/content/early/2015/09/01/025858).

Last but not least, if this approach could be generalized to tools written in other languages such as Java, 
C, Perl, among others, it would not only ease the migration of (bioinformatics) tools to newer workflow
systems, but for instance test the quality and robustness of several bioinformatics tools automatically.

#### Languages and skills
Python
Python troubleshooting

#### Code
https://github.com/common-workflow-language/gxargparse
https://github.com/common-workflow-language/common-workflow-language/issues/175#issuecomment-183332827

#### Mentors
[Roman Valls Guimera](https://github.com/brainstorm)
[Michael R. Crusoe](https://github.com/mr-c)
