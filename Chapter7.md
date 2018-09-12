
# Chapter 7

## Requirements: Behavior-Driven Design and User Stories

### Concepts

  1. User Stories
  2. Low-Fidelity(Lo-fi) user interfaces and storyboards.
  3. Points to turn users stories in estimate schedule.
  4. Velocity to measure and stimate schedule.
  5. Using the tool **Cucumber** to transform user stories into acceptance tests.
  6. Using the tool **Pivotal Tracker** to track project progress, to calculate velocity, and to  estimate time to milestones.

### 7.1 Introduction to Behavior-Driven Design and User stories

  "*Behavior-Driven Testing is Test-Driven Development done correctly.*"
                                                                    --Anonimous

  We start the agile lifecycle with Behavior-Driven Design(BDD). The goal of BDD is **validation**(Build the right thing) not just **verification**(Build the thing right).
  The BDD Version of requiriments is **user stories**, which describe how the application is expected to be used. In BDD the stories take the place of design documents in plan-and-document.

  By concentrating on *behavior* of the application versus the *implementation* of application.
  The general guidelines for the user stories is that they must be **testable**, **small** to be implemented in one iteration and have **business value**.

* **User Story Format**

    Feature name
      as a [kind of stakeholder],
      so that [I can achieve some goal],
      I want to [do some task]

### 7.2 Points, Velocity, and Pivotal Tracker
  The **backlog** is the name of the collection of stories that have not yet been completed in this iteration.
  **Velocity** measures work rate based on the team's self-evaluation. As long as the team rates user stories consistently, it doesn't matter whether the team is completing 5 points or 10 points per iteration. The purpose is to give all stakeholders an idea how many iterations it will take a team to add the desired set of features, which hepls set reasonable expectations and reduces chances of disappointement.
  
  [Pivotal Tracker][1] is a service that tracks user stories and velocity. You can also use 
  [Trello][2] which offer some of it's features for free.

### 7.3 SMART User Stories
  SMART is an acronym for **S**pecific, **M**easurable, **R**elevant, and **T**imeboxed.

* **Specific**
  Feature: User can search for a movie (vague)
  Feature: User can search for a movie by title (specific)

* **Measureble**
  Feature: RottenPotatoes should have good responsive time (unmeasurable)
  Feature: When adding a movie, 99% of Add Movie Pages should appear within 3 seconds (measurable)

* **Achievable**
  User stories should be implemented in one iteration. If you're getting less than one story per iteration, then they are too big and you need to subdivide these stories into smaller ones.

* **Relevant**
  A user story must have business value to one or more stakeholders. One technique is the five recursive "Whys" to know if it has real business value.

* **Timeboxed**
  Timeboxing means that you stop developing a story once you've exceeded the time budget. Either you give up, divide the user story into smaller ones, or reschedule what is left according to a new estimate. If dividing looks like it won't help, consider asking the stakeholders what part of the story has the highets value so you can do it quickly.

One important concept expands upon the R of SMART is the *minimun viable product*(MVP). It's a subset of the full set of features that when completed has business value in the real world.

### 7.4 Lo-Fi User INterface Sketches and Storyboards
  The HCI community recommend using a low-tech approach to user interaces(**Lo-Fi UI**) and **sketches**. It consists of paper, crayons, scissors and other kindergarten tools fo UI mockups.
  Ideally, you make sketches for all the user stories that involve a UI. It may seem tedious, but eventually you are going to have to specify all the UI details using HTML to make the real UI, and it's a lot easier to get it right with pencil and paper than with code.
  To show how the sketches work together as users interacts with a page we use **storyboarding**. Instead of a linear sequence of images, the storyboard for a UI is tipically a tree or graph of screen driven by different user choices.

  To make it you need:
    * Pages or sections of pages.
    * Forms and buttons
    * Popups

### 7.5 Agile Cost Estimation

  The books gives an example of how Pivotal Labs works. They explain how they work in a phone call of 30 to 60 minutes. If the client and their team feels comfortable, they do a *scoping". Scoping is a roughly 90 minutes conversations with potential client, preferably in person. The Agile team ask the client to bring everyone who would give valuable information about the project. During it, the Agile team asks what what the client want done and a series of questions to identify risks, external integrations and so forth.  The lesser the risks and external integrations higher is the precision of weeks they give the client.


### 7.6 Introducing Cucumber and Capybara
  
  **Cucumber** turns customer-understandable user stories into **acceptance tests** and **integrations tests**. The first is to ensure the customer is satisfied and the later is to ensure that the interfaces between modules have consistent assumptions and communicate correctly.
  In the Cucumber context we will use the term **user story** to refer to a single **feature** with one or more **scenarios** that show different ways a feature is used. Feature and Scenario idetify the respective components. Each scenario is in turn composed of a sequence of 3 to 8 **steps**.

  **Cucumber Keywords** - **Given**,**When**, **Then**, and **But** have diffrerent names just for benefit of human readers, but they are all aliases to the same method.

  Each step of a scenario start with its own keyword. * Steps that start with **Given** usually set up some precoditions, such as navigating to a page.
  * Steps that start with **When** typically use one of Cucumber's built-in web steps to simulate the user pressing a button, for example.
  * Steps that start with **Then** will usually check to see if some condition is true. 
  * The conjunction **And** allows more complicated versions of Given, When, or Then phrases. The only other keyword you see in this format if **But**.

  **Example**
    Feature: User can manually add movie

    Scenario: Add a movie
      Given I am on the RottenPotatoes home page
      When I follow "Added new movie"
      Then I should be on the Create New Movie page
      When I fill in "Title" with "Men in Black"
      And I select "PG-13" from "Rating"
      And I press "Save Changes"
      Then I should be on the RottenPotatoes home page
      And I should see "Men in Black"
  
  A separate set of files defines the Ruby code that tests these steps. These are called **step defitinitions**. Generally, many steps can use a single step definition.

  Cucumber match the steps of the scenarios with the step definitions using regular expressions or **regexes**(Chapter 3). They match the English phrases in the steps of the scenarios to the step definitions of the testing harness.

  In the Rails world, **Capybara** simulates a user interaction and integrates seamlessly with Cucumber. It takes actions in a simulated web browser, for example, clicking on a link or button. Capybara can interact with the app to receive pages, parse the HTML, and submit forms as a user would.

### 7.7 Running Cucumber and Capybara

  A major benefit of user stories in Cucumber is **Red-Yellow-Green analysis**, Once a user story is written, we can try to run it immediately. In the the beginning, steps may initially be highlighted either in Red(for failing) or Yellow(for passing), by incrementally adding what's needed to make it pass.
  **Cucumbers are green** The test-passing color of the cucumber plant gives this tool its name.

  **Piece of code to use cucumber on your application**
    group	:test,	:development	do				
      gem	'cucumber-rails'
      gem	'cucumber-rails-training-wheels'	#	some	pre-fabbed	step	definitions
      gem	'database_cleaner'	#	to	clear	Cucumber's	test	database	between	runs
      gem	'capybara'									#	lets	Cucumber	pretend	to	be	a	web	browser
      gem	'launchy'										#	a	useful	debugging	aid	for	user	stories
    end

  Copy it to to your *gemfile* and run *bundle install*.
  Cucumber comes with a *generator*, to set the directories and files that Capybara and Cucumber needs. To run the generators go to your app's directory and run:
    rails generate cucumber:install capybara
    rails generate cucumber_rails_training_wheels:install
  Then you must update your database.
    rails db:migrate
    rails db:test:prepare
  After you add to your AddMovie.feature file this user story
    Feature: User can manually add movie

    Scenario: Add a movie
      Given I am on the RottenPotatoes home page
      When I follow "Add new movie"
      Then I should be on the Create New Movie page
      When I fill in "title" with "Men in Black"
      And I select "PG-13" from "rating"
      And I press "Save Changes"
      Then I should be on the RottenPotatoes home page
      And I should see "Men In Black"
  
  I had some problems using the gem Uglifier so I needed install nodejs
    sudo apt install nodejs
  And after that i18n gem had to be updated so I run
    bundle update
  Then I run
    cucumber
  And edited the features and paths until I got all steps green.

  [1]:https://www.pivotaltracker.com/
  [2]:https://trello.com/