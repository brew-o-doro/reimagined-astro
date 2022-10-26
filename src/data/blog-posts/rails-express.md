---
title: All Aboard the Rails Express
publishDate: 08 Dec 2020
description: Talking about the infamous Ruby on Rails
---

This blog post will be focused on:
Rails Nested Resources
ActiveRecord Query Methods

This blog post will be discussing these through the lens of my own Brew-Ti-Ful Reviews Rails App.

### What is Brew-Ti-Ful Reviews?
To put it simply, Brew-Ti-Ful Reviews is an app built with Rails that allows users to add coffees they have tasted or have yet to taste and give them reviews.

### Rails Nested Resources
Nested resources in rails give us the ability to document parent/child relationships directly in our routes.
```ruby
class Coffee < ApplicationRecord
  has_many :reviews
end 
class Review < ApplicationRecord
  belongs_to :coffee
end
```
Here we have the parent (Coffee) and the child(Review) taken from the two models User and Review. Nested routes are another way of capturing these relationships through your routing. This means that our URLs will look aesthetically pleasing and not a random string of numbers and characters.
```ruby
resources :coffees do
    resources :reviews, only: [:new, :index, :show]
end
```

This action will create routes for our coffees and this will also route our reviews to a ReviewsController. Nested Routes will also provide us with those aesthetically pleasing URL paths I had mentioned earlier.

```ruby
coffee_reviews GET    /coffees/:coffee_id/reviews(.:format)                                                    reviews#index
new_coffee_review GET    /coffees/:coffee_id/reviews/new(.:format)                                                reviews#new
coffee_review GET    /coffees/:coffee_id/reviews/:id(.:format)                                                reviews#show
coffees GET    /coffees(.:format)                                                                       coffees#index
```
So if we wanted to view all the reviews for a particular coffee, the URL would look like /coffees/1/reviews in your browser.

 This handy method will also create routing helpers such as new_coffee_review.

Nested Resources can also have deep nesting like this:
```ruby
resources :coffees do
    resources :reviews, only: [:new, :index, :show]
      resources :photos
end
```
However, doing these deeply nested resources is a good way to get yourself lost with all these cumbersome route helpers and URL paths. So in keeping up with good programming practices, it would be best to avoid deeply nesting routes.

With Nested Resources, you can utilize this powerful tool to help keep your routes neat, tidy, and dynamic.

### ActiveRecord::Query Methods

Before entering the Rails mod for Flatiron I had gotten used to writing methods with traditional Ruby syntax. It was not until this project that I discovered the fascinating world of ActiveRecord Query Methods.
One of my favorite things about programming has been discovering new ways to do things that I have previously already learned how to do. So when I found these new query methods to write code similar to what I was doing with the plain old ruby syntax I was astonished. ActiveRecord Query Methods fire up commands and do them through the database essentially speeding up your commands by doing it in the database.

Here are some of my favorite query methods that I learned while working on this project.

#### build
The build method is the equivalent of calling .new on an object. Just like new, build does not automatically save it to the database so you will need to call a save method on the variable.
```ruby
@review = @coffee.reviews.build
```

#### find_or_create_by

The find_or_create_by the method checks whether a record with the specified attributes exists. If it doesn't, then create is called. Essentially, this is telling our database to find something if that something exists then proceed, however, if there is no record in the database then create a new entry in the database for it. Really nifty method here!
```ruby
@user = User.find_or_create_by(email: user_email)
```
Here’s an example of where I used this query method in my project to create a controller action for omniauth.
With these new query methods, I feel like I have added a new tool to my developer belt! I definitely recommend you take a look at the Rails Guides here for way more query method goodness!

