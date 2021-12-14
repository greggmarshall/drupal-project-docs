# Custom Module Naming and Packaging

The general philosophy of the project build is to favor community functionality, which leverages the open source nature of Drupal, over custom functionality without specific reasons. The order of preference for a given functionality is:

1.  Using functionality of Drupal core (along with any configuration)

2.  Using functionality of a Drupal contributed module (along with any configuration)

3.  Developing a custom Drupal module general enough to contribute to drupal.org

4.  Developing a custom Drupal module specific to the project

## Module Naming

Modules are given a name that is descriptive, yet as short as possible. Take a look at the modules on [drupal.org](http://drupal.org/) for ideas how to name a module. Usually a module’s name is a couple of words long, however another option is a longer, more descriptive human readable name coupled with a shorter machine name. The human readable name is defined in the module’s info.yml file with the key “name”. The machine name is defined by the module’s directory name (e.g. machine\_name) and echoed in the various files inside that directory (e.g. machine\_name.info.yml, machine\_name.module which are inside the directory machine\_name).

More information on how to define a module name is documented at [https://www.drupal.org/docs/creating-custom-modules/let-drupal-know-about-your-module-with-an-infoyml-file](https://www.drupal.org/docs/creating-custom-modules/let-drupal-know-about-your-module-with-an-infoyml-file).

If the intent is the module is to be contributed back to the Drupal community, a quick search on [drupal.org](http://drupal.org/) for the intended name to make sure it is available. The easiest way is to go to the URL <http://drupal.org/project/machine_name>, substituting the chosen machine name for machine\_name. Note that even if the machine name is available at project start, there is no guarantee the name will still be available when it is time to submit the module.

**Project custom modules will use the convention of prefixing the machine name with xyz\_ (e.g. xyz\_machine\_name).**

## Package Naming

Modules are displayed by Drupal on the Extend administration page grouped by package, starting with the package core used to group the modules included in Drupal core.

The package used by Drupal is defined in the modules info.yml file using the key “package”. **All custom project modules should use the package “Project Custom Modules”.**

More information on how to define a module package is documented at [https://www.drupal.org/docs/creating-custom-modules/let-drupal-know-about-your-module-with-an-infoyml-file](https://www.drupal.org/docs/creating-custom-modules/let-drupal-know-about-your-module-with-an-infoyml-file).

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
