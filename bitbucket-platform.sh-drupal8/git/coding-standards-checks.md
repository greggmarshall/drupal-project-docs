Coding Standards Checks
=========================

The Drupal community has defined a set of *coding standards* and *best practices* that should be adhered to whenever 
you're writing code for Drupal. These standards provide a set of rules for how your code should be formatted, whether 
you should use tabs or spaces, some guidelines around naming conventions, and the location of files. These coding 
standards ensure consistency in code throughout the project, make it easy for developers to move around from one 
sub-section to another without having to re-learn how to read the code, and most of all help us to spend our time 
debating the functionality and logic contained in the code and not the semantics of whitespace.

PHP_CodeSniffer
----------------------------------------------
*PHP_CodeSniffer* is a library that tokenizes PHP, JavaScript and CSS files and detects violations of a defined set of 
coding standards. It works with Drupal 6, 7, or 8. (After you install Coder Sniffer, see command line options for 
running it here.)

*Coder* contains "sniffs" for PHP CodeSniffer. These "sniffs" tell PHP CodeSniffer whether code meets Drupal coding 
standards or not. Specifically, there are two rulesets, Drupal and DrupalPractice. 

**Check Drupal coding standards**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando phpcs --standard=Drupal --extensions=php,module,inc,install,test,profile,theme,css,info,txt,md /path/to/drupal/example_module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


**Check Drupal coding standards and ignore composer and node.js directories**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando phpcs --standard=Drupal --extensions=php,module,inc,install,test,profile,theme,css,info,txt,md --ignore=node_modules,bower_components,vendor /path/to/drupal/example_module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


**Check Drupal best practices**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando phpcs --standard=DrupalPractice --extensions=php,module,inc,install,test,profile,theme,css,info,txt,md /path/to/drupal/example_module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


**Automatically fix coding standards**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando phpcbf --standard=Drupal --extensions=php,module,inc,install,test,profile,theme,css,info,txt,md /path/to/drupal/example_module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

drupal-check
----------------------------------------------
Built on PHPStan, this static analysis tool will check for correctness (e.g. using a class that doesn't exist), deprecation errors, and more.


Why? While there are many static analysis tools out there, none of them run with the Drupal context in mind. This allows checking contrib modules for deprecation errors thrown by core.

### Usage

This tool works on all Drupal code, but must be executed within the root directory of a Drupal project..

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
drupal-check [OPTIONS] [DIRS]
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Arguments:

**OPTIONS** - See "Options" for allowed values. Specify multiples in sequence, e.g. -ad.

**DIRS** - One or more directories within the root of a Drupal project.

Options:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-a Check analysis
-d Check deprecations (default)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Examples:

Check the address contrib module:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando drupal-check web/modules/contrib/address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check the address contrib module for deprecations:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando drupal-check -d web/modules/contrib/address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check the address contrib module for analysis:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando drupal-check -a web/modules/contrib/address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check the address contrib module for both deprecations and analysis:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
lando drupal-check -ad web/modules/contrib/address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

commit-msg git hook
----------------------------------------------
The hook script is used to check the commit log message. 
Called by "git commit" with one argument, the name of the file that has the commit message. 

The script is being used to run a pre-check considering the following paths:

CUSTOM_DIRECTORY[0]='web/modules/custom'
CUSTOM_DIRECTORY[1]='web/themes/custom'

More paths could be considered by adding a new element to the array.

**Note:**
*Take into account that the script will check the code even if you haven't added the files into the staging area or 
committed the changes.*

pre-push git hook
----------------------------------------------
An example hook script to verify what is about to be pushed.  Called by "git push" after it has checked the remote 
status, but before anything has been pushed.

The script is being used to run a pre-check considering the following paths:

CUSTOM_DIRECTORY[0]='web/modules/custom'
CUSTOM_DIRECTORY[1]='web/themes/custom'

More paths could be considered by adding a new element to the array.

The push will be avoided if there is something that needs to be fixed.

**Note:**
*Take into account that the script will check the code even if you haven't added the files into the staging area or 
committed the changes.*

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
