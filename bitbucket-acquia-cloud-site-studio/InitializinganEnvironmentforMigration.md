# Initializing an Environment for Migration
 
 The process for each higher environment has been to start with an “empty” Drupal installation then run the content migrations to make sure the latest content is being used. That “empty” Drupal installation has the configuration of a recent development build until the release tag is deployed.

1.  The initialization process starts with deploying a recent tag from a development build to have the correct code and configuration for the next steps.

2.  The remainder of the steps are a series of Drush commands using Drush aliases. The Drush aliases for the project are of the form @project.environment where environment is dev, stage, prod. The following steps show the Drush alias for the prod environment.


    drush @project.prod site-install minimal install_configure_form.enable_update_status_module=NULL --sites-subdir=default --site-name='Project Company' --site-mail=site_email@project.com -- account-name=do.not.use --account-mail=shared.email@project.com -- locale=en --no-interaction -v --ansi
    drush @project.prod config:set system.site uuid 9fc2dc41-3dac-4ad7-924c-e0c7dcc31b0b --no-interaction -v --ansi
    drush @project.prod pm-enable config_split --no-interaction -v -- ansi
    drush @project.prod config-import sync --no-interaction -v --ansi drush @project.prod config-import sync --no-interaction -v --ansi drush @project.prod cache:rebuild
    drush @project.prod sync:import --overwrite-all --no-interaction -- ansi
    drush @project.prod cohesion:import --no-interaction --ansi 
    drush @project.prod cohesion:rebuild --no-interaction --ansi 
    drush @project.prod cache:rebuild
    PASSWORD=$(date +%s|sha256sum|base64|head -c 20) echo "Automatically generated password " $PASSWORD
    drush @project.prod user:create developer1 --mail=mailto:developer1@project.com --password=$PASSWORD
    drush @project.prod user:role:add "administrator" developer1 
    drush @project.prod user:create developer2 --mail=mailto:developer2@project.com --password=$PASSWORD
    drush @project.prod user:role:add "administrator" developer2 
    .
    .
    .
    drush @project.prod user:block do.not.use

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
