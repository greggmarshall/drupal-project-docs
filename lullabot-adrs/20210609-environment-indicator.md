# Environment Indicator

All Drupal websites our team works on have one or more environments. At a minimum, there will be a production and a local development environment. Most projects will have production, staging, development preview, and local environments. Developers and QA often access different environments at the same time. Since making content or configuration changes on the wrong environment can have unintended consequences, it is important to be able to distinguish environments easily.

---

date: 2021-07-23

status: accepted

deciders:
  - Andrew Berry
  - Mateu Aguiló Bosch
  - David Burns

---

## Decision

All client sites will have the [Environment Indicator](https://www.drupal.org/project/environment_indicator) module installed and configured.

Environment colors will be configured as follows:

<table>
<tr><th> Environment    </th><th> Colors          </th><th> Suggested `fg_color` </th><th> Suggested `bg_color`                           </th></tr>
<tr><td> Live           </td><td> White on Red    </td><td> `#fff`               </td><td> <span style="color: #e7131a">█</span>`#e7131a` </td></tr>
<tr><td> Staging        </td><td> White on Orange </td><td> `#fff`               </td><td> <span style="color: #b85c00">█</span>`#b85c00` </td></tr>
<tr><td> Development    </td><td> White on Green  </td><td> `#fff`               </td><td> <span style="color: #307b24">█</span>`#307b24` </td></tr>
<tr><td> Branch Preview </td><td> White on Purple </td><td> `#fff`               </td><td> <span style="color: #905">█</span>`#905`       </td></tr>
<tr><td> Local          </td><td> White on Grey   </td><td> `#fff`               </td><td> <span style="color: #505050">█</span>`#505050` </td></tr>
</table>

## Consequences

Errors will be reduced as all screenshots by authenticated users will indicate the environment. Standard environment colors may conflict with existing site configuration, so each team will need to decide if colors should be changed on existing sites or not. Sites with blue / green deployments will need to determine their own color scheme. Teams deviating from the recommended colours will need to check the accessibility of their custom colors.

## Example Implementation

```php
<?php

// Environment indicator.
// See: https://pantheon.io/docs/environment-indicator#d8tab-id
if (isset($_ENV['PANTHEON_ENVIRONMENT'])) {
  switch ($_ENV['PANTHEON_ENVIRONMENT']) {
    case 'dev':
      $config['environment_indicator.indicator']['name'] = 'Dev';
      // Green-ish background.
      $config['environment_indicator.indicator']['bg_color'] = '#307b24';
      // White text.
      $config['environment_indicator.indicator']['fg_color'] = '#fff';
      break;

    case 'test':
      $config['environment_indicator.indicator']['name'] = 'Test';
      // Orange-ish background.
      $config['environment_indicator.indicator']['bg_color'] = '#b85c00';
      // White text.
      $config['environment_indicator.indicator']['fg_color'] = '#fff';
      break;

    case 'live':
      $config['environment_indicator.indicator']['name'] = 'Live';
      // Red-ish background.
      $config['environment_indicator.indicator']['bg_color'] = '#e7131a';
      // White text.
      $config['environment_indicator.indicator']['fg_color'] = '#fff';
      break;

    default:
      $config['environment_indicator.indicator']['name'] = 'Multidev';
      // Purple-ish background.
      $config['environment_indicator.indicator']['bg_color'] = '#905';
      // White text.
      $config['environment_indicator.indicator']['fg_color'] = '#fff';
      break;
  }
}

// Replace this with however locals are detected.
if (getenv('IS_DDEV_PROJECT') == 'true') {
  $config['environment_indicator.indicator']['name'] = 'Local';
  // Grey-ish background.
  $config['environment_indicator.indicator']['bg_color'] = '#505050';
  // White text.
  $config['environment_indicator.indicator']['fg_color'] = '#fff';
}
```

© 2020-2022 Lullabot, Inc. This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
