<!-- @format -->

# Git workflow for [PROJECT_ID] project



## Gitflow workflow

[@todo] finish this section





## Fixed branch names

There are a few fixed branches in the repository that should not be renamed or
deleted at any time:

- **dev** — development branch, the source for all feature branches, runs on
  dev environment and used for integration testing.

- **qa** — qa branch, runs on qa environment and used for testing by
  qa/testers, can also be used for early user testing.

- **beta** — beta or UAT branch, runs on beta environment and used for user
  acceptance testing and allowing select end users to look at and evaluate the
  site during development.

- **master** — production branch, runs on production environment and after
  initial site launch is the version of the site that is seen by the general
  public.



## Creating a branch

Branches are named for the type of issue being worked on

[@todo] finish this section

```
git status
<deal with any modified or untracked files as needed>
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
```





## Daily/Morning Workflow



```
git status
git add <any file changes>
git commit -m “commit message in proper format"
git rebase -i
git fetch
git merge origin/dev
```

The “git rebase -i” is to remove any extraneous commits before the latest
development branch is merged in. Most developers commit changes frequently to
save intermediate results, often ending up with a lot of commits that ultimately
are redundant, such as “adding debugging code” followed by “removing debugging
code”. Before using “git rebase -I”, make sure you have your editor configured
correctly. When you type that command, your editor will open and you will see
something that looks like:

```
pick f7f3f6d adding debugging code
pick 310154e removing debugging code
pick a5f4a0d updated README formatting and added cat-file

# Rebase 710f0f8..a5f4a0d onto 710f0f8
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

Since the two commits we want to eliminate are in front of the one we want to
keep, move the one to keep to be first. Use the fixup option instead of the
squash option to ignore the commit messages. And use fixup instead of drop in
case there are changes in the commit(s) that aren’t just adding or removing
debugging code.

```
pick a5f4a0d updated README formatting and added cat-file
fixup f7f3f6d adding debugging code
fixup 310154e removing debugging code

# Rebase 710f0f8..a5f4a0d onto 710f0f8
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

After updating the picks to fixup or whatever, save the result and close the tab
in your editor. Git will wait until the editor window is closed before
continuing execution. If nothing appears to be happening, check for an open
editor window with something from git it in.



## Pull Requests

When your development for a branch is complete, the branch needs to be pushed to
BitBucket and a pull request created to have the branch merged into the
development (dev) branch. Prior to pushing the branch to BitBucket, the branch
should have the latest version of the development branch merged into it to
minimize the chances of merge conflicts when the pull request is created. If you
get a merge conflict when merging the latest version of the development branch,
make sure you resolve the merge conflict, and commit the merge conflict
resolution, before pushing your branch.

```
git status
git add <any file changes>
git commit -m “commit message in proper format"
git rebase -i
git fetch
git merge origin/dev
git push origin
```

If you get an error message pushing your branch to BitBucket, git will give you
the command to replace the “git push origin” with.



## Cleaning up Local Tracking Branches

After a pull request is merged on BitBucket, BitBucket _should_ delete the
branch in the repository. But if you were to do a “git branch -a” to look at
all branches, you would likely see the branch on your local machine and probably
see that branch listed as still part of the repository. When you checked out a
remote branch, or pushed a new branch from your machine, git created a remote
tracking branch locally. That stays even if the remote branch it is tracking is
deleted.



### Delete a Local Branch

To delete your local branch, use the command:

```
git branch -D local-branch-name
```



### Delete a Remote Tracking Branch

To delete the remote tracking branch of a branch that has been deleted in the
main repository (this works even if the branch still exists in the repository
since it is just deleting the remote tracking branch that is stored locally),
use the command:

```
git branch -d -r origin/remote-branch-name
```



### Delete any Remote Tracking Branches Not in the Repository

You can actually clean up all the remote tracking branches that have been
deleted from the repository by using the command:

```
git fetch -p
```



## Adding a Module + Configuration

Modules should be enabled one at a time, configured, then the configuration
exported and committed. That allows easy recognition of what configuration files
are associated with, or impacted by, a given module.

```
git status
<deal with any modified or untracked files as needed>
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
lando drush cim
<<in Drupal UI enable module (or use drush to enable) and configure it as necessary>>
lando drush cex
git status
git add <any file changes>
git commit -m “commit message in proper format"
git rebase -i
git fetch
git merge origin/dev
git push origin
```

One file you want to make sure is present in the configuration export you are
committing is the file core.extension.yml, which contains what modules are
enabled. Forgetting to include the core.extension.yml file in your commit may
result in the rest of the configuration associated with a new module being
ignored because Drupal hasn’t enabled the module that configuration is
associated with. Be aware that the core.extension.yml file is a common source
of merge conflicts if anyone else has enabled a module, exported configuration,
committed it, and had their pull request merged since you started your
development on this branch. That is one reason to try to keep your pull
requests as small, and therefore as fast to be merged, as possible to minimize
this possibility.



## Adding a Paragraph Type

Paragraph types should be enabled one at a time, configured, then the
configuration exported and committed. That allows easy recognition of what
configuration files are associated with, or impacted by, a given paragraph type.
Each new paragraph type should also result in a pull request to keep the number
of configuration files in any one pull request manageable. The workflow can be
summarized as:

```
git status
<deal with any modified or untracked files as needed>
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
lando drush cim
<<in Drupal UI create paragraph type, fields and configure as necessary>>
lando drush cex
git status
git add <any file changes>
git commit
git rebase -i
git fetch
git merge origin/dev
git push origin
```

In more detail, you want to start with the latest version of the DEV branch to
avoid as many merge conflicts as possible. “Development” that is largely
configuration that is exported from Drupal after setting the configuration via
the Drupal administrative UI often involves files that overlap between what
appear as two distinct configuration additions or changes. To start the
process:

```
git status
```

Deal with any modified or untracked files that might show up at this point. You
really want to have a clean git index to start from.

```
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
lando drush cim
```

The above steps are getting the latest DEV branch from the repository and making
sure any configuration changes that are included in that branch are reflected in
your Drupal database. The net result of these steps is if you did a “lando
drush cex”, Drush would report there is nothing to output, and a “git status”
would show no modified or untracked files.

At this point you can log into Drupal as an administrator and create the
paragraph type and the fields that are required for that paragraph type. You
should be using the Acquia Spec Tool spreadsheet for the project as your sole
source of truth, it will also be used to generate the behat tests to validate
the paragraph type later. **Unless you are sure a field is to be reused** (e.g.
the courses date and the events date should use the same field so a combined
list of courses and events, sorted by date, can be generated with Views, **you
should always create new fields.** Make sure the machine name matches the
Acquia Spec Tool spreadsheet, you might need to edit it. After you have
completely built the paragraph type and done a thorough review of the settings
to make sure they are correct, you can finish the process from the command line.

```
lando drush cex
git status
```

Note that you might notice some configuration that was exported, or modified,
during the export that doesn’t actually belong to the new paragraph type but is
a side effect of copying a database from production and running it on a local
environment. For instance the following example shows

```
On branch delete-me
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    config/local/core.extension.yml
	deleted:    config/local/system.performance.yml
	modified:   config/sync/core.extension.yml
	modified:   config/sync/system.performance.yml

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	config/sync/core.entity_form_display.paragraph.background_image.default.yml
	config/sync/core.entity_view_display.paragraph.background_image.default.yml
	config/sync/field.field.paragraph.background_image.field_bkg_image.yml
	config/sync/field.field.paragraph.background_image.field_title.yml
	config/sync/field.storage.paragraph.field_bkg_image.yml
	config/sync/field.storage.paragraph.field_title.yml
	config/sync/paragraphs.paragraphs_type.background_image.yml

no changes added to commit (use "git add" and/or "git commit -a")
```

The core.extension.yml and system.performance.yml file changes are changing
environments and should not be included in the commit/pull request. Add the rest
of the configuration files one at a time to make sure you are not accidentally
adding any configuration files you don’t intend.

```
git add config/sync/core.entity_form_display.paragraph.background_image.default.yml
git add config/sync/core.entity_view_display.paragraph.background_image.default.yml
git add config/sync/field.field.paragraph.background_image.field_bkg_image.yml
git add config/sync/field.field.paragraph.background_image.field_title.yml
git add config/sync/field.storage.paragraph.field_bkg_image.yml
git add config/sync/field.storage.paragraph.field_title.yml
git add config/sync/paragraphs.paragraphs_type.background_image.yml
```

At this point we want to commit the results, but we want to use the editor
version of the commit so we can have an extended commit message that lists the
configuration files in the commit. **Before doing this step, make sure you have
configured your editor (see git-configuration.md) or you will be using VIM for
the edits.** Instead of the usual commit with message command, just use:

```
git commit
```

Which will open Visual Studio Code (assuming you set that to be your editor)
with a tab/file COMMITMSG that looks like:

```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch delete-me
# Changes to be committed:
#	new file:   config/sync/core.entity_form_display.paragraph.background_image.default.yml
#	new file:   config/sync/core.entity_view_display.paragraph.background_image.default.yml
#	new file:   config/sync/field.field.paragraph.background_image.field_bkg_image.yml
#	new file:   config/sync/field.field.paragraph.background_image.field_title.yml
#	new file:   config/sync/field.storage.paragraph.field_bkg_image.yml
#	new file:   config/sync/field.storage.paragraph.field_title.yml
#	new file:   config/sync/paragraphs.paragraphs_type.background_image.yml
#
# Changes not staged for commit:
#	deleted:    config/local/core.extension.yml
#	deleted:    config/local/system.performance.yml
#	modified:   config/sync/core.extension.yml
#	modified:   config/sync/system.performance.yml
#
```

In the first, blank, line, put the normal commit message, formatted as required
(note: double check, if it isn’t formatted correctly the commit will be rejected
and all your edits lost!). Then uncomment the section between On branch …. and
the end of the file so it looks like this:

```
[PROJECT_ID]-1: Adding configuration for Background Image Paragraph Type.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch delete-me

Changes to be committed:
new file:   config/sync/core.entity_form_display.paragraph.background_image.default.yml
new file:   config/sync/core.entity_view_display.paragraph.background_image.default.yml
new file:   config/sync/field.field.paragraph.background_image.field_bkg_image.yml
new file:   config/sync/field.field.paragraph.background_image.field_title.yml
new file:   config/sync/field.storage.paragraph.field_bkg_image.yml
new file:   config/sync/field.storage.paragraph.field_title.yml
new file:   config/sync/paragraphs.paragraphs_type.background_image.yml

Changes not staged for commit:
deleted:    config/local/core.extension.yml
deleted:    config/local/system.performance.yml
modified:   config/sync/core.extension.yml
modified:   config/sync/system.performance.yml
#
```

Save the file and close the tab, which will finish the commit. Note at this
point the commit will be validated, so the first line needs to be in the
enforced format, see commit-messages.md. After the commit is done, merge one
more time with the DEV branch from the repository in case someone else had a
pull request merged while you were building the paragraph type, and you likely
don’t need the “git rebase” if you only did one commit, push the branch and
create a pull request.

```
git rebase -i
git fetch
git merge origin/dev
git push origin
```

Ideally you want to create, commit and have merged each paragraph type before
starting on the next one so you minimize the chances of merge conflicts or
errors during the configuration import or export. You might want to line up
your pull request reviewers in advance to expedite the review and merge.



## Adding a Content Type

Content types should be enabled one at a time, configured, then the
configuration exported and committed. That allows easy recognition of what
configuration files are associated with, or impacted by, a given content type.
Each new content type should also result in a pull request to keep the number of
configuration files in any one pull request manageable. **Note it is desirable
to create any referenced paragraph types before defining the corresponding
content type since to create the paragraph field in the content type you want to
configure which paragraphs may be used.**

```
git status
<deal with any modified or untracked files as needed>
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
lando drush cim
<<in Drupal UI create content type, fields and configure as necessary>>
lando drush cex
git status
git add <any file changes>
git commit
git rebase -i
git fetch
git merge origin/dev
git push origin
```

In more detail, you want to start with the latest version of the DEV branch to
avoid as many merge conflicts as possible. “Development” that is largely
configuration that is exported from Drupal after setting the configuration via
the Drupal administrative UI often involves files that overlap between what
appear as two distinct configuration additions or changes. To start the
process:

```
git status
```

Deal with any modified or untracked files that might show up at this point. You
really want to have a clean git index to start from.

```
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
lando drush cim
```

The above steps are getting the latest DEV branch from the repository and making
sure any configuration changes that are included in that branch are reflected in
your Drupal database. The net result of these steps is if you did a “lando
drush cex”, Drush would report there is nothing to output, and a “git status”
would show no modified or untracked files.

At this point you can log into Drupal as an administrator and create the content
type and the fields that are required for that content type. You should be
using the Acquia Spec Tool spreadsheet for the project as your sole source of
truth, it will also be used to generate the behat tests to validate the
paragraph type later. **Unless you are sure a field is to be reused** (e.g. the
courses date and the events date should use the same field so a combined list of
courses and events, sorted by date, can be generated with Views, **you should
always create new fields.** Make sure the machine name matches the Acquia Spec
Tool spreadsheet, you might need to edit it. After you have completely built
the content type and done a thorough review of the settings to make sure they
are correct, you can finish the process from the command line.

```
lando drush cex
git status
```

Note that you might notice some configuration that was exported, or modified,
during the export that doesn’t actually belong to the new paragraph type but is
a side effect of copying a database from production and running it on a local
environment. You may also notice the configuration export was confused and put
part of the configuration in the /config/sync folder and part of the
configuration in the /config/local folder. You can move the configuration files
from /config/local to /config/sync where they belong, before adding them to the
git commit. For instance the following example shows

```
On branch delete-me
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    config/local/core.extension.yml
	deleted:    config/local/system.performance.yml
	modified:   config/sync/core.extension.yml
	modified:   config/sync/system.performance.yml

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	config/sync/core.entity_form_display.node.blade_page.default.yml
	config/sync/core.entity_view_display.node.blade_page.default.yml
	config/sync/core.entity_view_display.node.blade_page.teaser.yml
	config/sync/field.field.node.blade_page.field_blade_blades.yml
	config/sync/field.storage.node.field_blade_blades.yml
	config/sync/language.content_settings.node.blade_page.yml
	config/sync/node.type.blade_page.yml

no changes added to commit (use "git add" and/or "git commit -a")
```

The core.extension.yml and system.performance.yml file changes are changing
environments and should not be included in the commit/pull request. Add the rest
of the configuration files one at a time to make sure you are not accidentally
adding any configuration files you don’t intend.

```
git add config/sync/core.entity_form_display.node.blade_page.default.yml
git add config/sync/core.entity_view_display.node.blade_page.default.yml
git add config/sync/core.entity_view_display.node.blade_page.teaser.yml
git add config/sync/field.field.node.blade_page.field_blade_blades.yml
git add config/sync/field.storage.node.field_blade_blades.yml
git add config/sync/language.content_settings.node.blade_page.yml
git add config/sync/node.type.blade_page.yml
```

At this point we want to commit the results, but we want to use the editor
version of the commit so we can have an extended commit message that lists the
configuration files in the commit. **Before doing this step, make sure you have
configured your editor (see git-configuration.md) or you will be using VIM for
the edits.** Instead of the usual commit with message command, just use:

```
git commit
```

Which will open Visual Studio Code (assuming you set that to be your editor)
with a tab/file COMMITMSG that looks like:

```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch delete-me
# Changes to be committed:
#	new file:   config/sync/core.entity_form_display.node.blade_page.default.yml
#	new file:   config/sync/core.entity_view_display.node.blade_page.default.yml
#	new file:   config/sync/core.entity_view_display.node.blade_page.teaser.yml
#	new file:   config/sync/field.field.node.blade_page.field_blade_blades.yml
#	new file:   config/sync/field.storage.node.field_blade_blades.yml
#	new file:   config/sync/language.content_settings.node.blade_page.yml
#	new file:   config/sync/node.type.blade_page.yml
#
# Changes not staged for commit:
#	deleted:    config/local/core.extension.yml
#	deleted:    config/local/system.performance.yml
#	modified:   config/sync/core.extension.yml
#	modified:   config/sync/system.performance.yml
#
```

In the first, blank, line, put the normal commit message, formatted as required
(note: double check, if it isn’t formatted correctly the commit will be rejected
and all your edits lost!). Then uncomment the section between On branch …. and
the end of the file so it looks like this:

```
[PROJECT_ID]-1: Adding configuration for Blade Page Content Type.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch delete-me

Changes to be committed:
new file:   config/sync/core.entity_form_display.node.blade_page.default.yml
new file:   config/sync/core.entity_view_display.node.blade_page.default.yml
new file:   config/sync/core.entity_view_display.node.blade_page.teaser.yml
new file:   config/sync/field.field.node.blade_page.field_blade_blades.yml
new file:   config/sync/field.storage.node.field_blade_blades.yml
new file:   config/sync/language.content_settings.node.blade_page.yml
new file:   config/sync/node.type.blade_page.yml

Changes not staged for commit:
deleted:    config/local/core.extension.yml
deleted:    config/local/system.performance.yml
modified:   config/sync/core.extension.yml
modified:   config/sync/system.performance.yml
#
```

Save the file and close the tab, which will finish the commit. Note at this
point the commit will be validated, so the first line needs to be in the
enforced format, see commit-messages.md. After the commit is done, merge one
more time with the DEV branch from the repository in case someone else had a
pull request merged while you were building the content type, and you likely
don’t need the “git rebase” if you only did one commit, push the branch and
create a pull request.

```
git rebase -i
git fetch
git merge origin/dev
git push origin
```

Ideally you want to create, commit and have merged each content type before
starting on the next one so you minimize the chances of merge conflicts or
errors during the configuration import or export. You might want to line up
your pull request reviewers in advance to expedite the review and merge.



## Adding a View

Views should be enabled one at a time, configured, then the configuration
exported and committed. That allows easy recognition of what configuration files
are associated with, or impacted by, a given view. Each new paragraph type
should also result in a pull request to keep the number of configuration files
in any one pull request manageable.

```
git status
<deal with any modified or untracked files as needed>
git checkout dev
git pull
git checkout -b feature/[PROJECT_ID]–9999-jira-created-branch
lando drush cim
<<in Drupal UI create view and configure as necessary>>
lando drush cex
git status
git add <any file changes>
git commit -m “commit message in proper format"
git rebase -i
git fetch
git merge origin/dev
git push origin
```

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
