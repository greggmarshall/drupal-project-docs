# Use Log4brains to manage the ADRs

---

date: 2021-07-04

status: deprecated

tags:
  - dev-tools
  - doc

deciders:
  - Andrew Berry
  - Mateu Aguiló Bosch
  - David Burns

---

## Context and Problem Statement

We want to record architectural decisions made in this project.
Which tool(s) should we use to manage these records?

## Considered Options

- [Log4brains](https://github.com/thomvaill/log4brains): architecture knowledge base (command-line + static site generator)
- [ADR Tools](https://github.com/npryce/adr-tools): command-line to create ADRs
- [ADR Tools Python](https://bitbucket.org/tinkerer_/adr-tools-python/src/master/): command-line to create ADRs
- [adr-viewer](https://github.com/mrwilson/adr-viewer): static site generator
- [adr-log](https://adr.github.io/adr-log/): command-line to create a TOC of ADRs

## Decision Outcome

![Log4brains](../src/images/adrs/Log4brains-logo-full.png)

Chosen option: "Log4brains", because it includes the features of all the other tools, and even more.

© 2020-2022 Lullabot, Inc. This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
