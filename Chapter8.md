# Chapter 8 - Software Testing: Test-Driven Development

## 8.1 Background: A RESTful API and a Ruby Gem

Testable code tends to be a good code, and vice-versa

## 8.2 FIRST, TDD and Red-Green-Refactor

Nowadays the responsabilities to test code is far more on their own developer. Also testing is also far more automated. Which means they're self-checking: the test code itself can determine whether the code being tested works or not, without requiring a human to manually check test output or interact with the software. A high degree of automation is key to supporting the five principles for creating a good tests, which are summarized by the acronym FIRST:  **F**ast, **I**ndependent, **R**epeatable, **S**elf-checking, and **T**imely.  

* Fast: it should easy and quick to run.  Autotest will be used to help with this.  
Independent: No test should rely on preconditions created by other tests.  
* Repeatable: test bahavior should not depend on external factors such as date or on *"magic constants"* that will break the test if their values change.  
* Self-checking: each test should be able to determine on its own thether it passed or failed, rather than relying on humans to check its output.  
* Timely: test should bre created or updated at the same time as the code being tested.  

Test-driven development(TDD) - Using the test to guide the development. Which can be refered to as *test-first development*.
We'll write tests using RSpec, a domain-specific language for testing Ruby code. A DSL is a small programming language designed to ease tackling problems within a single are(domain) at the expense of generality.  
Example of implementation of RSpec TDD test:

    require 'spec_helper'  
      describe MoviesController do
        describe 'searching TMDb' do  
          it 'should call the model method that performs TMDb search'  
          it 'should select the Search Results template for rendering'  
          it 'should make the TMDb search results available to that template'  
        end  
    end

## Seams, Doubles, and the Code You Wish You Had

1. Before you write any new code, write a test for one aspect of the behavior it should have. since the code being tested doesn't exist yet, writing the test forces you to think about how you wish the code would behave and interact with its collaborators if it did exist. We call this *"exercising the code you wish you had"*.
2. **Red** step: Run the test, and verify that it fails because you haven't yet implemented the code necessary to make it pass.
3. **Green** step: Write the *simplest* possible code that causes *this* test to pass without breaking any existing tests.
4. **Refactor** step: Look for opportunities to refactor either your code or your tests - changing the code's structure to eliminate redundancy, repetition, or to increase readiability.  
5. Repeat until all behaviors necessary to pass a scenario step are complete.

Rspec provides a post method that simulates posting a form to a controller action: the first argument is the action name(controller method) that will receive the post, and the second argument is a hash that will become the params seen by the controller action.  
Example:

    require 'spec_helper'
    describe MoviesController do
      describe 'searching TMDb' do
        it 'should call the model method that performs TMDb search' do
          post :search_tmdb, {:search_terms => 'hardware'}
        end
        it 'should select the Search Results template for rendering'
        it 'should make the TMDb search results available to that template'
      end
    end

Note how the it-end block is an actual test case while the others are remminders of tests to be written.  

In the example above we would need to first create an empty controller method and its corresponding route, so that the action(form subimission by the user) would have somewhere to go. Then we need to create an empty view so that the controller action has something to render.  

In this scenario there is no method created yet, so we would have to mock it.
For a method that will look like this:  

    @movies = Movie.find_in_tmdb(params[:search_terms])

We could use a mock like this one:

    require 'spec_helper' 
    describe MoviesController do
      describe 'searching TMDb' do
        it 'should call the model method that performs TMDb search' do
          fake_results = [mock('movie1'), mock('movie2')]
          Movie.should_receive(:find_in_tmdb).with('hardware').
            and_return(fake_results)
          post :search_tmdb, {:search_terms => 'hardware'}
        end
        it 'should select the Search Results template for rendering'
        it 'should make the TMDb search results available to that template'
      end
    end

In this case the code tested is *search_tmdb*. However, part of the behavior depends on *find_in_tmdb*. Since it's not implemented yet and the test should be *independent* we use RSpec's *mock* method to create an array of two "test double" Movie objects.  

     fake_results = [mock('movie1'), mock('movie2')]

We also use a line of code to express the **expectation** that the Movie class should receive a call to the method *find_in_tmdb* and that method should receive the single argument *'hardware'* whose ony purpose is to track whether it gets called, and if so, whether the right arguments are passed. 

    Movie.should_receive(:find_in_tmdb).with('hardware').
            and_return(fake_results)

Critcally, if a method with the **same name** already existed in the Movie class, it would be temporarily **overwritten** by this **method stub**.
The use of *should_receive* is an example of a **seam**.

>*“a place where you can alter behavior in your program without editing in that place.”* Feathers 2004)

If we deleted the *and_return* part the method stub would return *nil*.
