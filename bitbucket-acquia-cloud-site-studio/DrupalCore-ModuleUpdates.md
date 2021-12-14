# Drupal Core/Module Updates

Drupal is an open source CMS with a very large contributor base. It is made up of Drupal Core and approximately 47,000 community contributed add on modules, with about 6,200 modules Drupal 9 compatible (10,500 are Drupal 8 compatible).

Starting with Drupal 8.0, Drupal Core has a monthly minor release cycle. Bug fix releases are usually released on the first Wednesday of every month. Security releases are usually released on the third Wednesday of every month, although not every month has a security release. In addition, it is common for a security release to contain a small number of bug fixes.

Drupal Core has a six month major release cycle. The next version of Drupal 9, 9.3 is scheduled to be released about December 8, 2021. The last Drupal 9 release, 9.4, is scheduled to be released about June 15, 2022. At the same time the first release of Drupal 10, 10.0.0, will be released about June 15, 2022, but could be delayed as late as December 14, 2022 (Drupal 9.0 came out on time).

Community contributed add on modules are updated whenever the module maintainer(s) decide to release an update. Some modules are very actively maintained and get frequent releases with bug fixes and new features, other modules are minimally maintained or even unsupported by the original maintainer and receive very infrequent, or no, updates. As such contributed module updates can be released at any time. The only scheduled releases for community modules are security updates, which are always released on a Wednesday afternoon.

With almost 100 contributed modules in the project code base it is not uncommon for several contributed modules updates to be released every month.

### Drupal Core + 99 Most Popular Modules -- Releases Since Drupal 8

Drupal 8.0.0 was released on November 19, 2015.  From that date until the end of September 2020, Drupal core and the 99 most popular contributed modules have had over 2,000 releases.  How they break down is shown below.

Releases since Drupal 8 Release
<table>
<tbody>
<tr>
<td>Core</td>
<td>249</td>
</tr>
<tr>
<td>Top 99 Modules</td>
<td>1,801</td>
</tr>
</tbody>
</table>

Months since Drupal 8 release	70

Releases per month
<table>
<tbody>
<tr>
<td>Core</td>
<td>3.5</td>
</tr>
<tr>
<td>Top 99 Modules</td>
<td>26</td>
</tr>
</tbody>
</table>

Security Releases since Drupal 8 Release
<table>
<tbody>
<tr>
<td>Core</td>
<td>49</td>
</tr>
<tr>
<td>Top 99 Modules</td>
<td>416</td>
</tr>
</tbody>
</table>
Security Releases are included in the total number of releases above.


## Best Practice is Keep Drupal and Modules Up To Date

While it might be tempting to continue to use the versions of the modules already installed on the site and already tested, generally it considered to be a bad practice, which experience has proven true. At some point it is likely a needed bug fix or feature update will be required or desired. Waiting until that time and jumping several minor releases in a single update can sometimes be very problematic. In theory, any release of a module might require configuration or database updates that will be run after that release is installed on the site. While jumping several minor releases will run those updates sequentially when the latest version is installed, there have been instances when an update is tied to the code in a specific release that later gets further changed, so running the update in the presence of that later release causes errors, or worse, unreported inconsistencies that are extremely hard to track down.

Generally a good cycle to check for, and implement, Drupal core and contributed module releases would be monthly, probably on the third Wednesday of every month to coincide with the Drupal security update releases, or semimonthly on the first and third Wednesday of every month to coincide with both the bug fix and security release cycle of Drupal core.

## Checking for Available Updates

The Project Drupal project is being managed by Composer and Composer should be used to check for available updates. The Drupal core update module has been uninstalled and will not check for, or notify, about core and module updates. A similar service for Composer projects is [Violinist](https://violinist.io/). Finally do not use the command line tool Drush (e.g. drush update:status) to check for module updates and especially to attempt to update modules since it is incompatible with Composer.

To check for core and module updates in the project Drupal project, navigate to the project root on the command line and type the command:

    $ composer outdated -D

Using the -D option (or --direct) limits composer to checking only the packages in the composer.json file.

Generally the consensus in the Drupal community is indirect dependencies shouldn’t be updated until the Drupal core or module that they are dependencies of is updated and requires the updated version. The feeling is updating a dependency first might introduce changes that are incompatible with the module using them, causing hard to identify issues.

The result of the composer outdated command might look like the following:

    $ composer outdated -D    
     Color legend:
      - patch or minor release available - update recommended
      - major release available - update possible
     composer/installers v1.11.0 v2.0.0 A multi-framework Composer library installer
     drupal/core-composer-scaffold 9.2.2 9.2.3 A flexible Composer project scaffold builder.
     drupal/core-dev 9.2.2 9.2.3 require-dev dependencies from drupal/drupal; use in addition to drupal/core-recommended to run tests from drupal/core.
     drupal/core-recommended 9.2.2 9.2.3 Locked core dependencies; require this project INSTEAD OF drupal/core.
     drupal/easy_breadcrumb 1.15.0 2.0.1 Adds configuration to the system breadcrumbs.
     mglaman/phpstan-drupal 0.12.11 0.12.12 Drupal extension and rules for PHPStan
     phpstan/phpstan 0.12.93 0.12.94 PHPStan - PHP Static Analysis Tool
     phpunit/phpunit 9.5.7 9.5.8 The PHP Unit Testing framework.

The output is color coded (not shown here) with available versions in yellow (patch or minor release) recommended to be routinely updated. Available version in red (major release available) need to be evaluated to see if the update will cause issues since major releases often change the module's API or other functioning. In the above example composer/installers and drupal/easy\_breadcrumb are red and would require investigation before being implemented. Generally with the version constraints common in Drupal the major releases also require a different process to update and would not result in any updates (unless there is a minor release that isn’t shown because of the major release) using the composer update process below.

## Updating Drupal Core and Contributed Modules--Minor Releases

To update Drupal core the command to use is:

    $ composer update drupal/core "drupal/core-\*" --with-all-dependencies

Note the --with-all-dependencies will take care of updating any indirect packages that are a result of Drupal core.

To update a Drupal module, module\_name, the command to use is:

    $ composer update drupal/module\_name --with-all-dependencies

In the example above several additional packages need to be updated as well, simply replace drupal/module\_name with the package description, e.g. phpstan/phpstan. Note the --with-all-dependencies will take care of updating any indirect packages that are a result of a given module or package, including any in the composer.json that are dependent on the package and not updated yet. As an example, updating mglaman/phpstan-drupal will also update phpstan/phpstan and possibly phpunit/phpunit depending on the dependency tree. It is helpful to run the composer outdated -D command after every update just to see what might already have been updated.

## Updating Drupal Core and Contributed Modules--Major Releases

Most Drupal modules and packages listed in composer.json are version constrained by the caret (^) symbol along with the version originally installed (any updates are usually only in the composer.lock file). That version constraint will allow minor releases (changes in the third numbers) to be installed with composer update but won’t allow a major release (changes in the first or second numbers) to be installed with composer update, they must be installed with composer require. To do that, the command is, using composer/installers as an example:

    $ composer require composer/installers:^2.0.0

## Running any Updates to Drupal Database/Configuration after Updating

Prior to running any of the following commands it is recommended that the local environment or Cloud IDE being used to generate the update should be sync’d to the latest database using the command for a Cloud IDE

    $ blt drupal:sync

Or the command for a local environment assuming DDEV is being used

    $ ddev start
    $ ddev blt drupal:sync

Then to run any Drupal database or configuration updates use the command

    $ drush updatedb or

    $ ddev drush updatedb

Note as the updates are being deployed to Acquia via Git and the deployment process, each environment receiving that update will also have dru sh updatedb run from a cloud hook.

Finally to export any configuration changes resulting from the update use the command

    $ drush config:export or

    $ ddev drush config:export

## Git Considerations for Updates

How the changes will be committed and merged using Git will depend on the timing of the update relative to the development release process. A high priority update, such as a critical or highly critical security update, should probably be released using a [Hotfix]() change then immediately merged into the development branch(es). Lower priority updates, and perhaps major releases, that can wait and would benefit from additional testing before being released, can be implemented by creating a feature branch (a good way is create a Jira ticket for a task to perform the updates and use it to create the branch) and opening a pull request to be merged into the appropriate development branch. Some care should be exercised not to let core or module updates go more than a very few months before being deployed to all environments, including PROD.

To identify what files have changed during the update, remembering that Drupal core, contributed modules and dependencies are excluded from the Git repository, run the command

    $ git status

At a minimum the composer.lock file will have been modified. If a major release was implemented the composer.json file will also be modified. If the database/configuration updates changed any configuration then one or more configuration files in /config/default might have changed or possibly, but rarely, created as untracked files in /config/default. The modified files should be added to the commit and the commit made, then pushed to Bitbucket and merged via an appropriate pull request.

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
