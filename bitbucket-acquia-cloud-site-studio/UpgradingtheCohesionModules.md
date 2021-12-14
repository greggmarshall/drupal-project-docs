# Upgrading the Cohesion Modules

Many times upgrading the Site Studio (Cohesion) modules is the same process as upgrading any other Drupal modules.

However because Cohesion keeps a configuration item, last\_entity\_update, in certain configuration objects and their exported YAML files in /config/default, sometimes after doing an update and running drush updatedb then doing a configuration export with drush config: export, those changed last\_entity\_update items are not included, with no indication it has happened or why.

That becomes an issue during the next blt drupal:sync or during Acquia Pipelines builds because the configuration gets updated in the active configuration store but isn’t updated in the file store which causes BLT to report a configuration mismatch that isn’t resolved during configuration imports. They reference a documentation article, [https://support.acquia.com/hc/en-us/articles/360034687394--Configuration-in-the-](https://support.acquia.com/hc/en-us/articles/360034687394--Configuration-in-the-database-does-not-match-configuration-on-disk-when-using-BLT) [database-does-not-match-configuration-on-disk-when-using-BLT](https://support.acquia.com/hc/en-us/articles/360034687394--Configuration-in-the-database-does-not-match-configuration-on-disk-when-using-BLT) , that doesn’t seem to align with what is observed.

After experimenting with various techniques to get the last\_entity\_update to match I discovered a work around that is ugly but appears to work. Instead of starting with a populated database via blt drupal:sync, I start with a freshly created Drupal site using the minimal install profile, import the configuration and update the database then do the exports again. Occasionally the process needs repeating.

Here are the steps I generally use to resolve this issue, they are using DDEV because I found it easier to destroy and create a new installation than the Cloud IDE but in theory without the ddev in front of the commands they should work in a Cloud IDE.


    $ ddev composer install
    $ ddev drush @self site-install minimal install\_configure\_form. enable\_update\_status\_module=NULL --sites-subdir=default --site-name='My [BLT site' --site-mail=project.architect@project.com](mailto:--site-mail%3Dproject.architect@project.com) --account-name=gregg. marshall [--account-mail=project.architect@project.com](mailto:--account-mail%3Dproject.architect@project.com) --locale=en --no- interaction -v --ansi
    $ ddev drush @self config:set system.site uuid 9fc2dc41-3dac-4ad7-924c- e0c7dcc31b0b --no-interaction -v --ansi
    $ ddev drush @self pm-enable config\_split --no-interaction -v --ansi
    $ ddev drush @self config-import sync --no-interaction -v --ansi
    $ ddev drush @self config-import sync --no-interaction -v --ansi
    $ ddev drush @self cr
    $ ddev drush @self updb -y
    $ ddev drush @self config-import sync --no-interaction -v --ansi
    $ ddev drush @self sync:import --overwrite-all
    $ ddev drush @self cohesion:import
    $ ddev drush @self cohesion:rebuild
    $ ddev drush @self cex -y
    $ ddev drush @self sync:export
    $ ddev drush @self cohesion:import
    $ ddev drush @self cohesion:import
    $ ddev drush @self cex -y
    $ ddev drush @self sync:export
    $ git status
    $ git add config/default/cohesion*
    $ git add config/sitestudio/*

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
