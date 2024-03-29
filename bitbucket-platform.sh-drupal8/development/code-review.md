<!-- @format -->

# Code Review

"How do I perform a code review?"

This document provides guidance for performing a review of another developer's
code. This should occur on BitBucket via a Pull Request. See the Development
Workflow document (dev-workflow.md) for information on how to submit Pull
Requests, and how they fit into the development workflow.

Code review is both an art and a science. All code merged into this project
should be reviewed.

In addition to ensuring that the code being reviewed meets the established
standards, the code reviewer must consider whether the work is being
accomplished in the best way given the project priorities and constraints.

It is not possible to create an exhaustive list of all things that should be
checked in a code review. Rather, we will enumerate the major considerations
that a code reviewer should make and include a few high level examples for each:

- **Purpose and scope** Does the code do the right things?

  - Does the code meet the requirements of the ticket?

  - Does the code affect only what needs to be changed for the scope of the
    ticket--nothing more or less?

  - Is it clear how functional changes can verified?

- **Implementation** Does the code achieve its goal in the right way?

  - Is the code in the right place?

  - Does it correctly leverage the correct APIs, variables, etc? Common
    issues:

    - Use of global \$language, LANGUAGE_NONE instead of 'und'

    - Use of t()

  - Does it follow basic code principles? E.g.,

    - Functions are logically amotic with low cyclomatic complexity

    - Logic is being performed at the correct layer. E.g., no logic in the
      presentation layer.

    - Are its components re-usable?

  - Verify [best practices](best-practices.md) are being used. E.g.,

    - Views

    - Features

    - Configuration updates

- **Code style and standards** Does the code meet [Drupal coding standards]
  (https://www.drupal.org/coding-standards) and stylistic expectations?

  - All code has been validated via
    [Coder](https://www.drupal.org/project/coder)

  - Note that Drupal has coding standards for:

    - [PHP](https://www.drupal.org/coding-standards)

    - [PHP OOP](https://www.drupal.org/node/608152)

    - [SQL](https://www.drupal.org/node/2497)

    - [JS](https://www.drupal.org/node/172169)

    - [Twig](https://www.drupal.org/node/1823416)

    - [CSS](https://www.drupal.org/coding-standards/css)

    - [HTML](https://groups.drupal.org/node/6355)

    - [YML](https://www.drupal.org/coding-standards/config)

  - Classes, properties, methods, etc. are named logically and consistently.

- **Security**

  - Consider most popular vulnerabilities:

    - [SQL Injection](https://www.drupal.org/node/101495)

    - [XSS](https://docs.acquia.com/articles/introduction-cross-site-scripting-xss-and-drupal)

    - [CSRF](https://www.drupal.org/node/178896)

  - Ensure that Drupal security best practices are being used:

    - [D8](https://www.drupal.org/node/2489544)

  - Verify that any contrib modules being added have stable releases and do
    not have outstanding [security
    advisories](https://www.drupal.org/security/contrib).

- **Performance** How does the code impact site performance?

  - Code should [implement caching](best-practices.md#caching) whenever
    possible

    - Caution with using `$_SESSION`, which invalidates page cache

  - Code should not be needlessly expensive

    - Caution with full node/entity loads, particularly in loops

      - Use of Entity API, in particular `entity_metadata_wrapper()` as
        a way to access and traverse entity properties and fields. Make
        sure to wrap usages in `try { ... } catch (EntityMetadataWrapperException $e) { ... }`

    - Caution with `hook_init()` and `hook_boot()`

- **Test coverage** Does the pull request include required [automated
  tests](../tests/README.md)?

  - All application functionality should be covered by a functional test via
    either Behat or PHPUnit

  - All custom libraries should be covered using unit tests via PHPUnit

- **Documentation**

  - Minimum documentation requirements set forth by Drupal Coding Standard
    should be met.

  - The code itself should be correctly self-documenting: [Code Tells You
    How, Comments Tell You
    Why](http://blog.codinghorror.com/code-tells-you-how-comments-tell-you-why/)

  - Additional user-facing documentation is included where necessary

- Configuration management

  - All configuration should be managed in code. Databases are never pushed
    upstream.

  - All required configuration changes should be managed in code via update
    hooks. In most cases, it should not be necessary for the Release Master
    to run anything beyond `drush updb` when running a release.



## Resources

- [A Quick Guide for Code
  Reviews](https://www.lullabot.com/articles/a-quick-guide-for-code-reviews)

- [How to review Drupal code](http://colans.net/blog/how-review-drupal-code)


© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
