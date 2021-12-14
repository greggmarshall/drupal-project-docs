# Git Conventions and Standards

The following conventions and standards will be used by the project.

## Files to be Excluded from Pull Requests

The following files are to be excluded from most pull requests to avoid possible merge conflicts and better manage the enabled modules: 


- composer.json
- composer.lock
- config/default/core.extension.yml

Any general pull request containing any of these files will be declined.

If a change is desired to any of these files, contact the team lead or git master to have a special branch created and merged with the changes.

## Keep Pull Requests Small and Focused

In general pull requests should focus on a single subtask or task and should involve the minimum number of files possible and should only incorporate a single item of functionality (e.g. a single module, a single content type, a single module’s configuration).

Keeping pull requests small and focused will allow the reviewer(s) to more quickly review the pull request and approve it or ask for changes.

## Don’t Mix Custom Code and Configuration

Generally if you have custom code it should be submitted in its own pull request and allowed to be reviewed and merged before submitting any configuration that might depend on that custom code. A common reason for build failures is a pull request that has custom code plus configuration, since the custom code isn’t enabled (due to config/default/core.extension.yml not being included) so the configuration dependent on its functionality can’t be imported. Thus the sequence is:

1.  Create the custom module and submit a PR for that module.

2.  When the custom module is approved and merged, create a Jira task to have the project architect enable the module

3.  When the project architects’s PR for enabling the module is approved and merged, create a PR for the configuration that is dependent on the custom module.

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
