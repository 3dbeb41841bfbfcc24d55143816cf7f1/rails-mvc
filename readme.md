# Intro to Rails + MVC + Asset Pipeline

##Learning Objectives
By the end of this lecture you should be able to...

- Explain Rails
- Articulate the Rails philosophy
- Describe MVC
- Start a new app
- Navigate Rails directory structure
- Link routes, controllers and views
- Explain the Asset Pipeline


<br>


##Explaining Rails
**I do:**

- Whiteboard: What is Rails?
	- Open source web application framework
	- is a framework
	- is a gem
	- has its own interface
	- connects Ruby with HTML, CSS, and JavaScript
- Whiteboard: Why Rails?
	- it’s awesome
	- can make sweet, functional websites ridiculously quickly
	- provides structure and convention over configuration
	- because the structure is well known, any Rails dev can pick up another Rails app with (relative) ease
	- it’s open source
	- it’s automagical (Google the term)
- Whiteboard: Why be skeptic?
	- it’s automagical to a fault sometimes
	- you can become dependent on it like a crutch


<br>
##Rails Philosophy

Rails values...

* DRYness
* Separation of Concerns & Modularity
* Abstraction & encapsulation
* Convention over configuration

### Separation of Concerns

In writing a large application it is important to establish something known as **Separation of Concerns**, *writing modular code where each component focuses on one aspect within the application.*

The benefit of this is similar to idea of **compartmentalization** with respect to a production line, which allows for *more rapid development* by being able to **divide and conquer** the construction of a product. Compartments can focus on one task and optimize functional concerns far outside the scope of other compartments, but still work together to achieve the same product.  Ultimately it reduces the headache of debugging and controlling a large application that can ultimately grow to a level of complexity that no one person could ever fully comprehend (nor want or need to).

### Organizational Principles

In order to manage the development of emerging aspects within a project it is important to construct a guideline that will shape how things are separated, a **design pattern**, which everyone can use to maintain **consistent** organization of different aspects. This is a *conventional* choice that helps to understandably scale a project. Part of the role of a developer is to become familiar with using design patterns, but this takes time (and trust), as different patterns emphasize an array of qualities: scalability, modularity, security, performance, et cetera.

<br>

##MVC

Rails uses an __MVC__ architecture

<b>M</b>odel - The model refers to the data objects that we use. It's the object oriented approach to design. The data in our database will be the most common type of object that we'll put there.

<b>V</b>iew - The view is the Presentation layer. It's what the user sees and interacts with, essentially the web pages. The HTML, the CSS and the JavaScript. The controller processes and responds to user events, such as clicking on links and submitting forms.

<b>C</b>ontroller - The controller will make decisions based on the request and then control what happens in response. It controls the interaction with our models and with our views.

(Ref: [Hartl MVC](https://www.railstutorial.org/book/toy_app#fig-mvc_detailed))

![MVC Diagram](https://softcover.s3.amazonaws.com/636/ruby_on_rails_tutorial_3rd_edition/images/figures/mvc_detailed.png)

##Railstaurant Metaphore
The **client** is a customer eating in the restaurant, the **server** is the waiter, the **router** is waiter who hands off orders, the **controller** is the kitchen, the **database** is the giant walk-in refrigerator with ingredients, the **model** is the person fetching ingredients from the refrigerator, the **view** is the chef who makes the meal look pretty and relays it back to the customer.

<br>

##Setup

### How to create a rails project

`rails new NAME_OF_APP`

But then it says, bundle install at the end, so, it's created all the files, and now it's telling bundler to install all of the gems that might be missing.

### Bundler

Bundler is a separate gem from Rails, and can be used outside of
Rails, but Rails is going to depend on it to manage the RubyGems that
our application needs. The first thing that you need to know is that
there are two files that matter to bundler - Gemfile and Gemfile.lock.
Look at Gemfile. This contains configuration information about what
gems we want to load. And, specifically, what version of gems as well.
This might look similar to the package.json file from our Node/Express
days.

Bundler is going to sort all of those out for us, and it's going to
create a tree of gems that it ought to load with all the dependencies
that ought to be loaded with it. And, after it creates that list, or
manifest file, it's going to store it in Gemfile.lock. We can take a
look at that file as well. You'll see, it looks very similar in
content, but the format is very different.

You never want to edit Gemfile.lock yourself. That's Bundler's file to
put its results in. Gemfile is the one that you'll edit. Now, how do
you tell Bundler to take your Gemfile and turn it into Gemfile.lock?
Well, with one simple command: `bundle install`. You'll remember that
when we created our rails application at the end of the process, it
ran Bundle Install for us.


`bundle exec` - run this before `rake db:migrate` if you're having issues

### Start a server

`rails server`

or the equivalent but shorter:

`rails s`

This will start a server on localhost:3000

<br>

## Experiment

- create a new rails app: `rails new NAME_OF_APP`
- run `rails server` and see what happens
- open `localhost:3000` in your favorite browser


<br>

## Create a controller and view

- `rails generate controller demo index`
- add "Hello, World!" in the erb page
- now how do we get to this page? What do we need? A route!
- go to `routes.rb` see that we have a `/demo/index`
- start the server (`rails s`) and go to `http://localhost:3000/demo/index` to see hello world!

<br>

## Rails File Structure

![Rails File Structure](http://i.imgur.com/whOL4DQ.png)

- app - most important directory
	- models, views, controllers are all in here
	- helpers is where you put helper code for views
	- mailers - for sending emails
	- assets -> where we put static files
- bin
	- bundle, rails, rake our binary files
- config
	- Application configuration, set config files for routes, db and environments
- db
	- store code related to db - Migrations go here!
- gemfile/gemfile lock
	- Gems are like NPMs. You have to put any gem you want to use in your Gemfile. You have to run bundle anytime you change your Gemfile. Your rails server needs to be restarted after any changes to your Gemfile.
- doc - Documentation for the application
- lib - Library modules
- log - Application log files
- public - simple html files here (anything here will be visible to the public),
	- Data accessible to the public (e.g., web browsers), including images and cascading style sheets (CSS)

- test for testing
- tmp - temp files for rails to store stuff
- vendor - Third-party code such as plugins and gems, much less used because of gems
- README - A brief description of the application
- Rakefile	- Utility tasks available via the rake command



<br>

##Asset Pipeline

[Ninefold Article](https://ninefold.com/blog/2014/07/01/rails-and-the-warped-asset-pipeline/)

- Allows for pre-processors such as Coffee, Sass, and ERb
- Minifies JS and CSS files
- Combines them all into one, so there are less requests to the server
- Browsers allow 10 parallel requests at any time, so if you have 15+ JS/CSS files, it can become a serious hindrance to load time

***How it works in a Nutshell***

- Your Javascript files and CSS files all get compressed into 2 files: application.js and application.css.
- Those compressed files get sent down to the public/assets directory and are served up for your viewing pleasure.
- Your images and other files in app/assets get sent down the pipe to public/assets as well and are served from there.

***Three Features***

- Concatenation
	- Rails uses Sprockets, a fancy term for puppetmaster, to take all your Javascript files and merge it into one single .js file. It does the same thing for CSS. This is brilliant because serving up less files means load times are that much faster.
	- 15 Javascript or CSS files take longer than 1 Javascript or CSS file to load.

- Compression
	- Once those files have been merged together, they undergo a metamorphosis and are shrunk down to a more manageable size. Extra whitespace and comments are removed.
	- When we code, our CSS files are formatted in a way to make things look pretty and visually appealing. But when you’re a machine, you don’t need comments or pretty indents and spaces. You’re a machine! And all this equates to faster loading times, since it’s less bits being transferred.

- Precompilation (of high-level languages)
	- Some of the best things about being a web developer right now is being able to use handy new next-gen higher-level languages. No longer do we have to survive by actually writing out every. single. HTML tag by hand. No longer do we have to write out lines and lines of code and make sure you get every bracket, comma, and semi-colon right.
	- Now we have meta-languages like Coffeescript, Sass, ERB, HAML, and the list goes on! At this stage, our Rails Coffeescript and Sass files get converted – precompiled – to vanilla Javascript and CSS.


<br>

## Routing

- in `routes.rb` we include our routing (very similar to `app.js` in express)

- simple route or match route
	- `get "demo/index"`
	- the same as match `"demo/index"`,
		- `:to => "demo#index"`,
		- `:via => :get`

- root route:

`root :to => 'demo#index'`
or
`root "demo#index"`

- remember, routes in Rails are like express in that they start from the top and go to bottom

<br>

## Rendering templates

- in the `DemoController` add:

```ruby
def index
  # will automatically look for a view in app/views/demo/index.html.erb and render it
end
```
Always check out the terminal for request/response!

Just to make something render in our app, let's add the following to our `index` action:

```ruby
render text: "Hello World!"
```

If we refresh the page and goto our `/` (root) and we should see "Hello World!".

<br>

## Template file names

`index.html.erb`

- Template name: index
- Process with: ERB
- Output format: HTML

<br>

## Instance variables for data into our views

- Inside a controller action include
- `@` infront of a Ruby variable makes it an instance variable

	```ruby
	@hello = "Hello World!"
	@instructors = ['Mike', 'Bruce', 'Marc']
	```
- Instance variables from the controller are available in the cooresponding view that the controller action renders
- Go into our `index.html.erb` and load our instance variables via embedded Ruby tags (ERB).

	```ruby
	<h1><%= @hello %></h1>

	<ul>
 	 <% @instructors.each do |instructor| %>
   	   <li><%= instructor %></li>
	<% end %>
	</ul>
```

<br>

## Making our app look even better using bootswatch

It's time to start paying attention to how our app looks. We've been learning and using Bootstrap for a little while now, so let's style our application! There is a wonderful resource called bootswatch that lets us use free templates which means we can use bootstrap and not have our app look like every other bootstrap page!

#### Getting Started

We need to include a couple gems in order to get started. In our Gemfile let's include

```ruby
gem `bootstrap-sass`
gem `bootswatch-rails`
```

After running `bundle` in the terminal, let's create a new file in our `app/assets/stylesheets` folder named `custom.css.scss` so that we can include our scss extentions. Now paste in the following code

```ruby
// The following will import variables, bootstrap itself, then the bootswatch style

@import "bootswatch/journal/variables";
@import "bootstrap";
@import "bootswatch/journal/bootswatch";

// If you want to import your own styles just use

@import "name_of_scss file"

// Here are the free themes you can use:

// Amelia
// Cerulean
// Cosmo
// Cyborg
// Darkly
// Flatly
// Journal
// Lumen
// Paper
// Readable
// Sandstone
// Simplex
// Slate
// Spacelab
// Superhero
// United
// Yeti
```
## Homework


- Start reading Hartl

