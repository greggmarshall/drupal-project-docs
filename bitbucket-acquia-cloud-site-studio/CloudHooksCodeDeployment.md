# Cloud Hooks Code Deployment

Acquia has Cloud Hooks that are executed every time code is updated or deployed, as well as when a database is copied or files or copied from another environment.

While all the directories are present, we are only using the common cloud hooks, primarily those for updating or deploying code. While there are separate hooks for both updating or deploying, in actuality the BLT commands executed end up being equivalent.

The equivalent Drush commands executed by the cloud hooks for code deployment are:

    # blt artifact:ac-hooks:post-code-deploy
    # blt artifact:ac-hooks:post-code-update
    # blt artifact:update:drupal:all-sites
    # set site UUID to exported value to ensure configuration compatibility
    drush updb
    drush cache-rebuild 
    drush en config_split 
    drush config:import 
    drush config:import
    # check drush config:status, should not have any configuration differences
    # blt project:ssi
    drush sync:import --overwrite-all drush cohesion:import
    drush cohesion:rebuild
    drush state:set system.maintenance_mode 0 --input-format=integer 
    drush cache:rebuild

Note that line 10 in the above steps is a common place where builds and deploys fail due to some piece of configuration that doesn’t change during import with the error

    [error] Configuration in the database does not match configuration on disk. This indicates that your configuration on disk needs attention. Please read https://support.acquia.com/hc/en-us/articles/360034687394--Configuration-in-the-database-does-not-match-configuration-on-disk-when-using-BLT

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
