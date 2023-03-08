<!-- @format -->

# Git commit message format

We use a git commit message that is formatted in a consistent way:

```
[PROJECT_ID]-123: Updated code that does something important.
```

Breaking down the commit message format:

- [PROJECT_ID]- is the project identifier and should always be "[PROJECT_ID]" and separated from
  the JIRA ticket number by a dash.

- 123 is the JIRA ticket number of the task/story being worked on. It must be
  only digits and separated from the project identifier by a dash in front of
  the ticket number and from the commit message by a colon (:) and a space
  after the JIRA ticket number.

- Commit message is a short description of the commit. It must be at least 15
  characters long, shouldn't be more than 60 characters (any longer and use a
  multi-line commit message), and must end with a period. Keep commit messages
  informative to **why** a commit is being made.

To commit using the above git commit message you would type:

```
git commit -m "[PROJECT_ID]-123: Updated code that does something important."
```



## When a single line commit message isn't enough

**Before using this method, make sure you have your git client properly
configured (see git-configuration.md)**

Instead of using the -m "[PROJECT_ID]-123: Updated code that does something important."
form of a git commit, you can use the interactive git message, which can be
created with Visual Studio Code by typing:

```
git commit
```

That will open your Visual Studio Code with something that looks like:

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch dev
# Your branch is up to date with 'origin/dev'.
#
# Changes to be committed:
#   new file:   documentation/development/code-review.md
#   new file:   documentation/development/oss-contribution.md
#   new file:   documentation/development/web-accessibility-checklist.md
#   new file:   documentation/git/commit-messages.md
#   new file:   documentation/git/git-configuration.md
#   new file:   documentation/setup/local-setup.md
#   new file:   documentation/setup/project-setup.md
#
```

Every line starting with a pound sign (\#) will be deleted in the actual commit.
You can include that information by removing the \# signs.

Make sure you include the properly formatted commit message as the first line of
the file you are editing!

```
[PROJECT_ID]-123: Updated code that does something important.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch dev
# Your branch is up to date with 'origin/dev'.
#

Changes to be committed:
new file:   documentation/development/code-review.md
new file:   documentation/development/oss-contribution.md
new file:   documentation/development/web-accessibility-checklist.md
new file:   documentation/git/commit-messages.md
new file:   documentation/git/git-configuration.md
new file:   documentation/setup/local-setup.md
new file:   documentation/setup/project-setup.md
#
```

When you are done editing the commit message, save it and close the file in
Visual Studio Code, that will then tell git that you are done with the commit
message, the file will be checked for a valid commit message (ideally as the
first line of the file), and, if it passes, will make the commit. **Note that if
the commit message isn't properly formatted the commit is ignored, including all
the changes you made in the editor**. _It is recommended to copy the commit
message to a new Visual Studio Code window before saving and closing the
COMMIT_EDITMSG window, just in case to avoid losing any work if the commit is
rejected._ As soon as the commit is accepted you can delete the extra Visual
Studio Code window.

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
