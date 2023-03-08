# Workflow

Export configuration for specific environment:

* enable module and/or set configuration if required;
* edit Configuration Split in Configuration > Development > Configuration Split Setting;
* add new module in Complite Split. Make sure you add to the existing list (contol + click);
* for specific configuration only (like image styles, error logging, etc.), select related item under Conditional Split. Make sure you add to the existing list (contol + click);
* in terminal run __lando drush csex [env_id]__ (env_id: _local_, _dev_, _qa_, _prod_)
* test your new configuration by running __lando drush cim__

## Testing different environment

I you need to test different environment configuration on your local, please uncomment following line in settings.php and set the variable to one of the env_id (env_id: _local_, _dev_, _qa_, _prod_):
__//$current_environment = 'qa';__

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
