# Acquia's Drupal Spec Tool

Link to Drupal Spec Tool spreadsheet for Project **INSERT LINK HERE**

Link to Acquia blog post explaining the tool, especially the spreadsheet, [https://dev.acquia.com/blog/a-specification-tool-for-drupal-8-/30/05/2018/19606](https://dev.acquia.com/blog/a-specification-tool-for-drupal-8-/30/05/2018/19606)

Link to Drupal Spec Tool documentation and Behat testing contexts <https://github.com/acquia/drupal-spec-tool>

## Tracks Content Types/Fields, Media/Images, Views/Workflow

The spreadsheet automatically generates the Gherkin for Behat tests that are part of the Project code base and will be automatically run on every build.

<div class="notice">

**If you make a change to a content type, its fields, media types, images, views, views displays, or workflow in Drupal and commit that configuration to the code base, make sure you also update the Google sheet for the project Drupal Spec Tool <span class="underline">AND</span> copy the corresponding Gherkin from the Behat tab of that sheet to the corresponding .feature file in /tests/behat/features/drupal-spec-tool/.**

</div>

Those files are:

*  content\_model.feature (content types and fields) 
*  media.feature (media types and image styles)
*  menus.feature (Drupal menus)
*  views.feature (Views and View Displays)
*  workflow.feature (Content Moderation Workflows)
 
<!---- Use this text if a very large project results in exceeding the Google sheets character limit, see https://github.com/acquia/drupal-spec-tool/issues/11#issuecomment-802017294
 Note, if you change a content type, paragraph type or field, notice the special instructions on the Behat tab of the Drupal Spec Tool sheet. The fields are on a separate tab due to the number of fields and the 50,000 character limit on Google sheets. You copy the cell from the Behat tab of the sheet into the content\_model.feature, then select and copy the A column of the Behat Fields tab and paste it below the cell’s content. There likely will be blank lines at the end of the file, they should be deleted.
--->

## Run Tests Locally Before Submitting Pull Requests

If you are developing locally using DDEV, then you have already run the ./scripts/dev-setup.sh script and should be ready to go, just type

    $ ddev blt tests:behat

If you are developing using a Cloud IDE, and you haven’t already run the setup script, from your project root run:

    $ ./scripts/ide-setup.sh

Then to run the Behat tests you can type

    $ blt tests:behat

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
