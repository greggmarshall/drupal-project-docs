<!-- @format -->

# Best Practices

"How should I write code?"

_This document is a work in progress._ Unlinked items are planned topics, feel
free to contribute.

- [Standards](#standards)

- [Exporting configuration](#exporting-config)

- [Configuration updates](#config-updates)

- [Caching strategies](#caching)

- [Patching](#patching)

- [Building Views](#views)

- [Logging](#logging)

- [Building content types](#content-types)

- [Naming conventions](#naming-conventions)

## Standards

All work must conform to established best practices and coding standards. Code
quality is ensured in a variety of ways:

- All code must conform to [Drupal Coding
  Standards](https://www.drupal.org/coding-standards). This is enforced via
  local git hooks and code checks performed during continuous integration.

- All front end code must follow Drupal Theming Best Practices.

- All code must be reviewed by a peer or established integrator before being
  merged into the master branch.

- All new features must covered by an automated test that mirrors the ticket
  acceptance criteria.

Please peruse the [examples](examples) directory for examples of various coding
best practices.

## Exporting configuration

All site functionality should be represented in version-controlled code. This
includes all configuration. See the documentation in the CMI directory of the
documentation.

- Each export should be as discrete and independent as possible. Configuration
  dependencies should be carefully considered! All dependencies should be
  one-way. Circular dependencies should never exist.

Common mistakes:

- Creation of large exports that encompass many un-related components. E.g.,
  multiple un-related content types, views, roles, permissions are all bundled
  into a single feature.

- Poor design of dependencies, e.g., creation of circular dependencies.

- Each export has too many dependencies, so no one export can be merged in
  isolation, or a single export creates merge conflicts with exports from
  other developers. E.g., the "Workflow" configuration depends on the "Press
  Room" configuration because it requires field_xyz which is provided by
  "Press Room."

## Configuration updates

- When configuration changes, that change needs to be exported to code.

- Before making any configuration changes, make sure to pull the latest DEV
  branch, and import any configuration changes in that branch, then create
  your feature branch from there and make/export the configuration changes.

- Keep configuration change exports as small as possible to avoid merge
  conflicts with other configuration changes from other developers.

- Updates should to be actively monitored. This should be done using NewRelic,
  SumoLogic, Logstreaming, and/or other monitoring tools.

- When an update is merged into the DEV branch, export your configuration
  changes, make sure to pull the latest version of the DEV branch from
  Bitbucket, and merge it into your branch before pushing your branch. Watch
  for merge conflicts that indicate the configuration changes you are making
  are in conflict

## Caching

Without caching, Drupal is slow. As a general rule of thumb, _try to cache
everything that you can_ and _try to invalidate that cache only when it is
likely to be stale_.

Caching is complex. Because caching is so complex, it's difficult to provide
general guidelines for caching strategies. Here are the factors the should be
considered when making caching decisions:

- What is serving the cache? E.g., CDN, Varnish, Memcache, DB, APC, etc.

- What is being cached? An entire page, one component of a page, bytecode,
  etc.

- Is the cache context-aware? I.e., is there only one version of the cached
  data or might it differ depending circumstances? E.g., the "Welcome
  [username]" block changes depending on the logged-in user.

- What circumstances render the cached data stale? E.g., a cached view of
  press releases is stale when a press release is updated.

- How should the cache be invalidated? E.g., invalid after X minutes,
  triggered by a user action, etc.

Specifically, ensure that you are properly caching data at every level possible,
including:

- Page caching (Varnish)

- Database query caching (Redis)

- Views caching

- Block caching

- Panels caching

- Entity caching

- Twig caching

- CDN (Content Delivery Network)

See the [Drupal 8 Cache API](https://www.drupal.org/developing/api/8/cache)
documentation for information in implementing your caching strategy. This is
especially important for custom modules to make sure you are properly updating
cache tags so Drupal can communicate with Varnish and/or the CDN to make sure
they aren’t serving out of date content.

## Patching

All modifications to core or contributed code should be performed via a patch.
For detailed information on how to patch projects, please see
[../patches/README.md] (../patches/README.md). Patches to core or contributed
code should be hosted on drupal.org if at all possible. Exceptions must be
cleared with the technical architect and documented in the /patches/README.md)

## Views

Please see [views.md](views.md).

## Logging

- Any configuration changes from custom modules should be logged to watchdog
  (also [Acquia Library
  recommendations\|https://docs.acquia.com/articles/how-audit-authenticated-user-actions-better-risk-management])

- Any destructive actions **must** be logged

## Building content types

@todo Document: \* Appropriate time to use fields \* Audit for overly complex
content types \* Reason: All fields loaded for each node load \* Use case: Needs
translations, user-facing form, revisions, etc.

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
