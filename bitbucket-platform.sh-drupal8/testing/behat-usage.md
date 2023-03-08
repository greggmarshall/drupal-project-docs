# Instructions for using behat within the project code

## 1. Setup & Installation  

## 2. Usage - Running tests
### Running all tests: 
For running all the available tests run this command: 
    
    lando behat

### Running a single test    
For running only one single test you can specify the name of the specific scenario: 

    lando behat --name "ScenarioName"

* Example: 

For this single scenario  written in Gherkin

    Scenario Outline: Login with incorrect credentials
        When I fill in "edit-name" with "<Username>"
        And I fill in "edit-pass" with "<Password>"
        And I press the "edit-submit" button
        Then I should not see "<Username>"
        
        Examples:
        | Username  | Password |
        | username  | pass1234 |

The execution will be the following:

    lando behat --name "Login with incorrect credentials"

or with single quotes

    lando behat --name 'Login with incorrect credentials'

The result will show only the execution of the scenarios including the text in their titles.  

### Running several tests
For running several tests (or even only one in some cases) we can help us with tags: 

    lando behat --tags @tagName

* Example:

For the two scenarios below: 

    @upcoming_event
    Scenario: Validate upcoming event block is visible 
    Given I am on the events page 
    Then I should see the upcoming event block

    @upcoming_event
    Scenario: Validate content on upcoming event block
        Given I am on the events page 
        Then I should see the upcoming event block
            And The upcoming event block should contain title, date, location and link

The execution will be the following:

    lando behat --tags @upcoming_event

The result will show only the execution of all the scenarios under the tag "@upcoming_event".

You can add more than one tag if needed with different formats for filtering the execution of tests.

For an "OR" operation:

    lando behat --tags '@upcoming_event,@past_event'

or 

    lando behat --tags 'upcoming_event,past_event'

For an "AND" operation: 

    lando behat --tags '@upcoming_event&&@past_event'

For a "NOT" operation: 

    lando behat --tags '~@upcoming_event'

## 3. Main commands 
| Command | Description |
| --- | --------- |
| lando behat -dl | List of all step definitions available |
| lando behat | Execution of all tests |
| lando behat --name "scenarioName" | Execution of tests with the specified name in their titles |
| lando behat --tags @scenarioTag | Execution of tests under the specified tags |

## 4. Adding tests

For adding scenarios you should go to the corresponding folder located under the path **/tests/behat/features**
Within these folders you will find feature files where you can add a new test case or scenario. 

### Using default step definitions 
The easiest and fastest way to create a new test case is by using the steps definitions already included in the framework. 


Examples: 

Here are two examples showing the usage of default step definitions
```
# Element info should be raplaced in a second iteration.
@upcoming_event
Scenario: Validate upcoming event block is visible 
  Then I should see an "div[class='field field--name-field-banner-view field--type-viewsreference field--label-hidden field--item']" element    
    And the "div[class='viewsreference--view-title']" element should contain "Upcoming event"
    And I should see "Upcoming event" in the "div[class='viewsreference--view-title']" element
```
```
@upcoming_event   
Scenario Outline: Validate upcoming event block contains title, date, location and link
  Then I should see an "<Element>" element
Examples:
| Name      | Element | 
| Title     | div[class='views-field views-field-title'] |
| Date      | div[class='views-field views-field-field-event-course-date-1'] |
| Location  | div[class='views-field views-field-field-course-location'] |
| Link      | div[class='views-field views-field-view-node'] |
```

### Using custom step definitions 
A second option is to create your own step definitions. This will require to create the definitions itself in PHP code, including all the classes and objects needed.

Example: 
```
Scenario: Login as Administrator 
  Given I am logged in as Administrator
  ...
```
The steps above don't have a default step definition created so each one will need to be defined following the example below:

    /**
     * @Given I am logged in as Administrator$/
     */
    public function iAmLoggedInAsAdministrator()
    {
        $this->visit('/login');
        $this->fillField('Login', 'Administrator')
        $this->fillField('Password', 'AdminPassword1234');
        $this->pressButton('Login');
    }

## 6. Report 
Uncomment the report formatter extension to get an html report under the path _'/tests/behat/report/Execution Behat Report.html'_, it will be updated after each execution and will contain the details including passed and failed scenarios.

## 7. Maintenance and new additions 
Maintenance and new plugins added to the framework will require to modify the __composer.json__ file and run __composer install__ for updating references. )

The file behat.yml might need to be updated as well, depending on the addition to the framework. 

#### **IMPORTANT:**
Do this changes consciously as they can affect the whole project causing compilation problems.

## 8. References

* [Behat documentation](http://behat.org/en/latest/guides.html)
* [Behat html formatter plugin](https://github.com/dutchiexl/BehatHtmlFormatterPlugin)


## 9. Integration with Platform

(Pending...)

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
