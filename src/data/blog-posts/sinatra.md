---
title: Fly Me To The Moon- Sinatra with Ruby Will Take You Places!
publishDate: 05 Oct 2020
description: Discussing sinatra and ruby.
---
![ An illustration of a person with an idea ](/assets/pixeltrue-idea-1.png)

Hello, readers! I am back with some more coverage of my projects for Flatiron Schools. This article will be discussing my first try at creating a full-stack web application using Ruby and Sinatra!

### Sinatra? Isn’t that a singer?
While you are not wrong in recognizing Sinatra as the singer, however, the Sinatra we’ll be talking about is the DSL(domain specific language) that’s implemented on top of Ruby and Rack, similar to a lightweight version of Rails. Sinatra is designed to simple and easy to get started creating web applications from the ground up with minimal efforts.

Essentially, Sinatra is Ruby Gem which speeds up the process of creating web apps considerably. It is really effective in the methods it uses for working with nested directories.

### Sinatra & Corneal what is not to love?
I have to shout-out a special Sinatra skeleton that creates the basic file structures for a creating a quick web application. Corneal is literally a life save that takes out all the intitial tedious work that is related towards creating a basic application. Corneal will set up a file structure in this manner:

```plaintext
Directory structure:

├── config.ru
├── Gemfile
├── Gemfile.lock
├── Rakefile
├── README
├── app
│   ├── controllers
│   │   └── application_controller.rb
│   ├── models
│   └── views
│       ├── layout.erb
│       └── welcome.erb
├── config
│   ├── initializers
│   └── environment.rb
├── db
│   └── migrate
├── lib
│   └── .gitkeep
└── public
|   ├── images
|   ├── javascripts
|   └── stylesheets
|       └── main.css
└── spec
    ├── application_controller_spec.rb
    └── spec_helper.rb
```

What I found to be especially helpful was that Corneal comes with some default CSS styling that makes it really easy to see your project while you are busy creating your controllers in the MVC model. I found this incredibly helpful for when I was setting up my database and models to easily see if my code was working as intended.
Corneal also has this awesome method built in for creating easy rake migrations.
corneal [model/scaffold] NAME name:string age:integer

This simple command does two things. First, it creates a rake migration file. Second, it writes the table for you. Essentially, saving you so much of your precious time. Say goodbye to:

```bash
rake db:create_migration NAME=[migration_name]
```


```ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      t.age :integer

      t.timestamps null: false
    end
  end
end
```

So, huge thanks to Brian Emory for creating this life saving tool.

### What about some controller action?

In the Models Views Controllers (MVC) format, Controllers can be viewed as the waiter that gives/returns orders from the cooks in the back of the restaurant and takes/returns orders to and from the customers or the Views. Which really illustrates just how important the Controllers are towards a functioning web application. When you are creating your web app, you can be guaranteed to spend most of your time working on these controllers.

In Sinatra, controllers are written in Ruby and consist of ‘routes’ that take requests sent from the browser (“GET this data”, “POST that data”), run code based on those requests by using models, and then render the .erb (view) files for the user to see. Moreover, the application_controller.rb file is where your program will inherit from Sinatra::Base making all these awesome Sinatra methods available to your application.

### What about helpers?

Speaking of controllers in Sinatra, utilizing a helper methods in your application_controller allows your web application to get rid of some “code smell” or redundancy in your methods. Something I have really grasped to as a developer in training is that developer’s do not like to repeat themselves, repeating yourself makes your program look messy. Remember keep your code DRY (don’t repeat yourself)! So creating helper methods really allows us as developers to write a code once and still be able to use it throughout our entire web application.


```ruby
helpers do

def logged_in?
    !!current_user
end
def current_user
    User.find_by(id: session[:user_id])
end
def authorized_to_edit?(post)
    post.user == current_user
end
end
```

The current_user helper method above allows us to relate the current user :id to the current_user method. This method is incredibly useful when paired with the logged_in? method which turns the value of current_user into a boolean which would either return true or false for whether the current_user is logged in at the time.
An example of how this would be used in the posts_controller.rb file:

```ruby
get '/posts/new' do
if logged_in?
    erb :'/posts/new'
else
    flash[:error] = "You must be logged in to create a review"
    redirect '/'
end
end
```

Naturally, this allows us to use the logged_in? method to render the /posts/new form only if the value of logged_in? is equal to true, making so that only a person who is logged in can create new posts!

You might have noticed the,

```ruby
flash[:error] = "You must be logged in to create a review"
```

This is a super awesome gem that lets the user know when there was a problem, otherwise the user will never know what actually happened. Sinatra-Flash has a lifecycle of one refresh, meaning once the user refreshes the page the message will dissappear! This is another super handy thing that lets the program be even more dynamic!

### The Verdict?

Sinatra is a really awesome DSL for creating quick web apps with minimum effort! I really enjoyed creating and learning using Sinatra. Though I must admit that Sinatra is not perfect. One of the biggest things that annoyed me was when you are creating your routes, ORDER MATTERS! If you do not have your routes in the particular way that Sinatra wants you to have them you will get strange errors, or as Sinatra likes to say “Sinatra doesn’t know this ditty.” Aside from that strange quirk Sinatra is really fun to code with!
