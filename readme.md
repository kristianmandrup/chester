# Chester

A MVC framework for Titanium Developer.

The purpose of this framework is to organize your Titanium Developer projects in a model-view-controller pattern.

# Why

Titanium Developer is an awesome javascript sdk for building mobile applications, but there is no conventions on how to organize your code.  We build web applications using Ruby on Rails, and being able to organize our iPad applications using the same patterns will enable us to process and maintain our software projects more effectively.

# Requirements

* node.js
* coffeescript

# Install

<pre>
  <code>
gem install chester
  </code>
</pre>  

# Add to any Titanium Developer Project

Just run chester install, and it will create the chester.coffee file in your Resources folder.
 
<pre>
  <code>
chester install ./Resources
  </code>
</pre>

# Easy to compile the coffee files to javascript

<pre>
  <code>
cd ./Resources
chester brew
  </code>
</pre>


# Easy to generate models|views|controllers

<pre>
  <code>
cd ./Resources
chester generate model person
chester generate controller people
chester generate view people index
  </code>
</pre>

These generators will make the following objects:

- models
  - person.coffee
  
<pre>
  <code>
class Person
  name: 'Person'
  # Insert your code here
  
Chester.Application.Models.add(new Person())
  </code>
</pre>

Just a quick run down on what is going on here, inorder for chester to know your model, you must have an attribute called name, which should act as a name that chester can understand, then the model needs to be registered to the application object so that chester can find your model when you request it.


- controllers
  - people.coffee
  
<pre>
  <code>
class PeopleController extends Chester.Controller
  name: 'PeopleController'

# Register Controller to application
Chester.Application.add(new PeopleController()) 

  </code>
</pre>

Same as the model the controller needs to have an attribute called name that is the actual name used for chester to recognize the controller.

- views
  - people
    - index.coffee
    
<pre>
  <code>
class PeopleIndex extends Chester.View
  name: "index"
  render: ->
    # TODO: add your presentation code here.

  # Register view to Patients Controller
Chester.Application.find("PeopleController").add(new PeopleIndex())
    
  </code>
</pre> 


# Framework

The object hierarchy is very straight forward.  Chester has a base object that has a collection called children, and a add method that adds a object to the children array and a find method that locates and returns the object based on the name of the object.

## Base

This is the core class definition that all other classes share.

## Application

This objects children are controllers, with the add method you can add new controller to this object.  And with the find method you can locate the controller by the name of the controller.  There is another array of objects attached to this class.  They are called models, these are basic classes that can added to the Models array.

## Controller

This objects children are views, these are not the same as views in titanium, these are simple JavaScript classes that are used to contain the user interface code to manage your mobile application.

## View

This will be the most confusing class, because the ui objects in titanium are user views.  the Chester views are more like code containers that help isolate your user interface code from your business logic and domain logic.

## Application.run

This is the main routing method that makes the whole application work.  It takes the following parameters as a JavaScript object.

Controller: string,
Action: string,
Params: object

This method simply finds the controller and executes the action method on the controller , passing the params object as the parameter.

Chester is built using coffee, because it is much easier to maintain, but you don't need to use coffeescript to use Chester, you can use JavaScript just fine.
