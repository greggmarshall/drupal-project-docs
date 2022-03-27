# Lullabot Architecture Decision Records

I first read about Lullabot's use of Architecture Decision Records (ADRs) in their blog post [Improving Team Efficiency with Architecture Decision Records](https://www.lullabot.com/articles/improving-team-efficiency-architecture-decision-records "Improving Team Efficiency with Architecture Decision Records").  That blog post led me to [Documenting Architecture Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) by Michael Nygard.

Lullabot publishes their ADRs on a Gatsby generated website at [https://architecture.lullabot.com/](https://architecture.lullabot.com/).  I reached out to them about getting the "source code" for the ADRs and they were kind enough to share the MDX files.  Since MDX is an extension of Markdown that assumes some Javascript supporting components, I slightly modified the files so they wouldn't require the component(s).

ADRs are small and meant to capture the reasons for various architectural decisions.  This group of ADRs is a good start at codifying common Drupal best practices.  The assumption is these ADRs will be evaluated and, if agreed by the development team for a project, incorporated or adapted as needed.  Not all will fit, as an example the decision not to use the Config Split module is likely to be somewhat controversial.

Also note the Lullabot ADRs are released under the Creative Commons Attribution "only" license and do not include the share alike clauses the rest of the documents in this repository have.
