#  Config Split Definition

The project Acquia Cloud subscription contains the following environments: DEV STAGE PROD CI (Acquia Pipelines) IDE (Acquia Cloud IDE) or a Local environment (DDEV or Lando based)

By convention, there is usually a local environment is defined for environments that are not part of the project Acquia Cloud subscription, although Acquia Cloud IDE environments are part of an Acquia Cloud subscription.

The Drupal community module Config Split is used to manage optional or variable configuration that changes depending on what environment is being used.

<table>
<tbody>
<tr class="odd">
<td></td>
<td>
<p><strong>Local, IDE</strong></p>
</td>
<td>
<p><strong>CI</strong></p>
</td>
<td>
<p><strong>Dev</strong></p>
</td>
<td>
<p><strong>Stage QA</strong></p>
</td>
<td>
<p><strong>Prod</strong></p>
</td>
</tr>
<tr class="even">
<td>Devel Module</td>
<td>Y</td>
<td>Y\*</td>
<td>Y</td>
<td>N</td>
<td>N</td>
</tr>
<tr class="odd">
<td>Search API Solr Devel</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>N</td>
</tr>
<tr class="even">
<td>Views UI</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>N</td>
</tr>
<tr class="odd">
<td>Field UI</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>N</td>
</tr>
<tr class="even">
<td>Caching</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
</tr>
<tr class="odd">
<td>Aggregation</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
</tr>
<tr class="even">
<td>Errors</td>
<td>ALL</td>
<td>Silent</td>
<td>ALL</td>
<td>ERRORS</td>
<td>Silent</td>
</tr>
<tr class="odd">
<td>Environment Color</td>
<td>Blue</td>
<td>Green</td>
<td>Yellow</td>
<td>Orange</td>
<td>Red</td>
</tr>
<tr class="even">
<td>Stage File Proxy</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>N</td>
<td>N</td>
</tr>
<tr class="odd">
<td>Shield</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
<td>N</td>
</tr>
<tr class="even">
<td>SMTP</td>
<td>Y</td>
<td>Y</td>
<td>N</td>
<td>N</td>
<td>N</td>
</tr>
<tr class="odd">
<td>DBLOG</td>
<td>Y</td>
<td>Y\*</td>
<td>Y</td>
<td>Y</td>
<td>N</td>
</tr>
<tr class="even">
<td>SYSLOG</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
</tr></tbody>
</table>
 
DBLOG and Devel modules are enabled in CI to allow Behat tests to pass.

### Modules Being Controlled by Config Split

* Advanced aggregation (advagg) 

* Database logging (dblog)

* Devel (devel) Field UI (field\_ui)

* PHP Authentication Shield (shield)

* Search API Solr Devel (search\_api\_solr\_devel) 

* SMTP (smtp)

* Stage File Proxy (stage\_file\_proxy) 

* System Logging (syslog)

* Views UI (views\_ui)

### Configuration Controlled by Config Split

* system.performance (aggregation and caching) 

* system.logging (error level being displayed)


© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
