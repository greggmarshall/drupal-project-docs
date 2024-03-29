# List of default steps definitions

Given I am an anonymous user
Given I am not logged in
Given I am logged in as a user with the :role role(s)
Given I am logged in as a/an :role
Given I am logged in as a user with the :role role(s) and I have the following fields:
Given I am logged in as :name
Given I am logged in as a user with the :permissions permission(s)
Then I should see (the text ):text in the :rowText row
Then I should not see (the text ):text in the :rowText row
Given I click :link in the :rowText row
Then I (should )see the :link in the :rowText row
Given the cache has been cleared
Given I run cron
Given I am viewing a/an :type (content )with the title :title
Given a/an :type (content )with the title :title
Given I am viewing my :type (content )with the title :title
Given :type content:
Given I am viewing a/an :type( content):
Then I should be able to edit a/an :type( content)
Given I am viewing a/an :vocabulary term with the name :name
Given a/an :vocabulary term with the name :name
Given users:
Given :vocabulary terms:
Given the/these (following )languages are available:
Then (I )break
Then I should see the error message( containing) :message
Then I should see the following error message(s):
Given I should not see the error message( containing) :message
Then I should not see the following error messages:
Then I should see the success message( containing) :message
Then I should see the following success messages:
Given I should not see the success message( containing) :message
Then I should not see the following success messages:
Then I should see the warning message( containing) :message
Then I should see the following warning messages:
Given I should not see the warning message( containing) :message
Then I should not see the following warning messages:
Then I should see the message( containing) :message
Then I should not see the message( containing) :message
Given I run drush :command
Given I run drush :command :arguments
Then drush output should contain :output
Then drush output should match :regex
Then drush output should not contain :output
Then print last drush output
Then I should see the button :button in the :region( region)
Then I should see the :button button in the :region( region)
Then I( should) see the :tag element in the :region( region)
Then I( should) not see the :tag element in the :region( region)
Then I( should) not see :text in the :tag element in the :region( region)
Then I( should) see the :tag element with the :attribute attribute set to :value in the :region( region)
Then I( should) see :text in the :tag element with the :attribute attribute set to :value in the :region( region)
Then I( should) see :text in the :tag element with the :property CSS property set to :value in the :region( region)
Given I am at :path
When I visit :path
When I click :link
Given for :field I enter :value
Given I enter :value for :field
Given I wait for AJAX to finish
When /^(?:|I )press "(?P<button>(?:[^"]|\\")*)"$/
When I press the :button button
Given I press the :char key in the :field field
Then I should see the link :link
Then I should not see the link :link
Then I should not visibly see the link :link
Then I (should )see the heading :heading
Then I (should )not see the heading :heading
Then I (should ) see the button :button
Then I (should ) see the :button button
Then I should not see the button :button
Then I should not see the :button button
When I follow/click :link in the :region( region)
Given I press :button in the :region( region)
Given I fill in :value for :field in the :region( region)
Given I fill in :field with :value in the :region( region)
Then I should see the heading :heading in the :region( region)
Then I should see the :heading heading in the :region( region)
Then I should see the link :link in the :region( region)
Then I should not see the link :link in the :region( region)
Then I should see( the text) :text in the :region( region)
Then I should not see( the text) :text in the :region( region)
Then I (should )see the text :text
Then I should not see the text :text
Then I should get a :code HTTP response
Then I should not get a :code HTTP response
Given I check the box :checkbox
Given I uncheck the box :checkbox
When I select the radio button :label with the id :id
When I select the radio button :label
Given /^(?:|I )am on (?:|the )homepage$/
When /^(?:|I )go to (?:|the )homepage$/
Given /^(?:|I )am on "(?P<page>[^"]+)"$/
When /^(?:|I )go to "(?P<page>[^"]+)"$/
When /^(?:|I )reload the page$/
When /^(?:|I )move backward one page$/
When /^(?:|I )move forward one page$/
When /^(?:|I )follow "(?P<link>(?:[^"]|\\")*)"$/
When /^(?:|I )fill in "(?P<field>(?:[^"]|\\")*)" with "(?P<value>(?:[^"]|\\")*)"$/
When /^(?:|I )fill in "(?P<field>(?:[^"]|\\")*)" with:$/
When /^(?:|I )fill in "(?P<value>(?:[^"]|\\")*)" for "(?P<field>(?:[^"]|\\")*)"$/
When /^(?:|I )fill in the following:$/
When /^(?:|I )select "(?P<option>(?:[^"]|\\")*)" from "(?P<select>(?:[^"]|\\")*)"$/
When /^(?:|I )additionally select "(?P<option>(?:[^"]|\\")*)" from "(?P<select>(?:[^"]|\\")*)"$/
When /^(?:|I )check "(?P<option>(?:[^"]|\\")*)"$/
When /^(?:|I )uncheck "(?P<option>(?:[^"]|\\")*)"$/
When /^(?:|I )attach the file "(?P<path>[^"]*)" to "(?P<field>(?:[^"]|\\")*)"$/
Then /^(?:|I )should be on "(?P<page>[^"]+)"$/
Then /^(?:|I )should be on (?:|the )homepage$/
Then /^the (?i)url(?-i) should match (?P<pattern>"(?:[^"]|\\")*")$/
Then /^the response status code should be (?P<code>\d+)$/
Then /^the response status code should not be (?P<code>\d+)$/
Then /^(?:|I )should see "(?P<text>(?:[^"]|\\")*)"$/
Then /^(?:|I )should not see "(?P<text>(?:[^"]|\\")*)"$/
Then /^(?:|I )should see text matching (?P<pattern>"(?:[^"]|\\")*")$/
Then /^(?:|I )should not see text matching (?P<pattern>"(?:[^"]|\\")*")$/
Then /^the response should contain "(?P<text>(?:[^"]|\\")*)"$/
Then /^the response should not contain "(?P<text>(?:[^"]|\\")*)"$/
Then /^(?:|I )should see "(?P<text>(?:[^"]|\\")*)" in the "(?P<element>[^"]*)" element$/
Then /^(?:|I )should not see "(?P<text>(?:[^"]|\\")*)" in the "(?P<element>[^"]*)" element$/
Then /^the "(?P<element>[^"]*)" element should contain "(?P<value>(?:[^"]|\\")*)"$/
Then /^the "(?P<element>[^"]*)" element should not contain "(?P<value>(?:[^"]|\\")*)"$/
Then /^(?:|I )should see an? "(?P<element>[^"]*)" element$/
Then /^(?:|I )should not see an? "(?P<element>[^"]*)" element$/
Then /^the "(?P<field>(?:[^"]|\\")*)" field should contain "(?P<value>(?:[^"]|\\")*)"$/
Then /^the "(?P<field>(?:[^"]|\\")*)" field should not contain "(?P<value>(?:[^"]|\\")*)"$/
Then /^(?:|I )should see (?P<num>\d+) "(?P<element>[^"]*)" elements?$/
Then /^the "(?P<checkbox>(?:[^"]|\\")*)" checkbox should be checked$/
Then /^the "(?P<checkbox>(?:[^"]|\\")*)" checkbox is checked$/
Then /^the checkbox "(?P<checkbox>(?:[^"]|\\")*)" (?:is|should be) checked$/
Then /^the "(?P<checkbox>(?:[^"]|\\")*)" checkbox should (?:be unchecked|not be checked)$/
Then /^the "(?P<checkbox>(?:[^"]|\\")*)" checkbox is (?:unchecked|not checked)$/
Then /^the checkbox "(?P<checkbox>(?:[^"]|\\")*)" should (?:be unchecked|not be checked)$/
Then /^the checkbox "(?P<checkbox>(?:[^"]|\\")*)" is (?:unchecked|not checked)$/
Then /^print current URL$/
Then /^print last response$/
Then /^show last response$/
Then exactly the following roles should exist
Then exactly the following content entity type bundles should exist
Then exactly the following fields should exist
Then exactly the following image styles should exist
Then exactly the following image effects should exist
Then exactly the following menus should exist
Then exactly the following views should exist
Then exactly the following views displays should exist
Then exactly the following workflows should exist
Then exactly the following workflow states should exist
Then exactly the following workflow transitions should exist

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
