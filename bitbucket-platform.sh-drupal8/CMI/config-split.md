<!-- @format -->

# Configuration Split

This module allows to define sets of configuration that will get exported to separate directories when exporting, and get merged together when importing. It is possible to define in settings.php which of these sets should be active and considered for the export and import.

## Steps for recreating the Config Split from scratch

**First Step (Common Config)**

- Enable all modules that will be used on all environments (including config_spit);
- Make sure that you have fallowing line in settings.php: **$config_directories[CONFIG_SYNC_DIRECTORY] = '../config/sync';**
- Run **lando drush cex** for the common configuration export;

**Create a Split**

- Make configuration changes that will be used on particular environment:
  - Enable modules;
  - Make config changes (like error display, caching, etc.)
- Create new folder in /config, same level as sync (ex. /config/dev)
- Open Configuration Split Setting page and create your split:
  - Give it a Label (ex. Dev)
  - Folder (ex. ../config/dev)
  - Remove check for Active
  - Multi select all the modules that were enabled for this split in Modules under Complete Split
  - Make sure to select 'core.extension' item in Configuration Items
  - Select all Configuration Items that will be changed for this environment under Conditional Split
  - Remove check for Split only when different
  - SAVE!
- Run \_\_lando drush csex [slipt_machine_name]
- Check to see the configuration files exported (ex. /config/dev)
- test by running **lando drush cim** - all the testing in Drupal should remain the same

**Enable Split**

- Create environment detection in the settings.php
- Enable desired split based on detected environment like: **$config['config_split.config_split.dev']['status'] = TRUE;**

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
