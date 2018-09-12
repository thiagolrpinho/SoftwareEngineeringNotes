
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


  [1]:https://www.pivotaltracker.com/
  [2]:https://trello.com/