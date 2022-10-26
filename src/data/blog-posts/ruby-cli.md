---
title: A Ruby CLI to Remember 💎
publishDate: 08 Aug 2020
description: Discussing my first coding project.
---

<!-- ![A screenshot of a coding challenge I completed during coding bootcamp](/assets/1*LvslgHSeWM4B50-rSXibvQ.png) -->

<a name="Blockquotes">
“If you wish to make an apple pie from scratch, you must first invent the universe.” — Carl Sagan
</a>

While brainstorming for what I wanted my Ruby API application to do; I was intimidated by the endless possibilities that my project could become. The apprehension was made a little easier by this one simple quote, “don’t try to eat an elephant whole, instead eat it piece by piece.” 

Basically, break down the project so that it is more manageable. With said mantra in mind, I chose to first focus on the overall user experience.

## What did I want to user to be able to do?

I wanted the user to be able to be able to easily access some kind of information through a list menu. When something was selected from the menu the information needed to be displayed for the use. The user should also have the capability to exit the program if they wished.

Now that I decided what I wanted the user to do, I needed to choose a specific type of information to display. I toyed with the idea of using an API focused on the Lord of the Rings (which I felt would be amazing). However, the API that I looked at required authorization keys and I felt like that was a headache that could be avoided.

Luckily, I saw a Pokemon Trading Card Game API, which I felt would be absolutely amazing! After browsing the developer docs and becoming familiar with the parameters that I could search for using JSON.

The slight problem with this was that I could not for the life of me get my API to work. Instead of being bogged down in the mire, I chose to start over with a fresh idea and new API.

The final outcome was using the old and reliable Star Wars API or SWAPI for short! I wanted to display information about the films and species of the creatures that reside in those films.

## Bundle Gem <file_name>

With all the information necessary to start, I first set up the basic directories that I could edit to create my application. In the terminal, I ran bundle gem galaxy_far_away_cli. The bundle gem is a life saver to newbies like myself for creating all the files I needed, including a readme file and a Code of Conduct file!
Now that the basic directories were set up I created a markdown notes file so that I could map out what I needed to create to make this app functional.

I know I needed three classes for this application to work. An API class that gets and creates objects, a film class that knows, stores, and creates films, a species class that does the same but with species and finally a CLI class that is going to be doing the heavy lifting of my app.

## CLI Class

I figured the best place to start was with the CLI class. I created a rudimentary menu that will be used for giving the user options to choose from.

The snippet above shows the basic code that would make the user’s experience while using this app.
The welcome method should serve the purpose of setting the tone for the rest of this app. I used the gem colorize to add a little flair to the program to make the look slightly more appealing (or as appealing as a command line could be).
APIService Class

I used HTTParty gem to do the bulk of the work of getting the API, plus it saved me a few lines of code with an added bonus being that it has the word party in it! Since the endpoint of the API required different params for returning the information I wanted, I had to concatenate to the end of the BASE_URI. Initially I used a fancy .concat but when I would try to run my code it would break! Oh the frustration that caused! Turned out using .concat would create a funny error where it would add up both params together which was just wonky. The old tried and true way of just using a simple + was the right way to go.

```ruby
Film Class
   def initialize(attr_hash)
        attr_hash.each do |k, v|
            self.send("#{k}=", v) if self.respond_to?("#{k}=")
        end
        save
    end
```

This little guy right here is a really higher level way of saying for each key and value of the hash returned from the API, it’s going to return the individual objects designated by the attr_accessor but only if it can find a designated key for it! Oh and the save method being called there is just a way to save the objects being created by the class into an empty array called @@all.

## Conclusion
<a name="Blockquotes">“It was as though you struggled against 
fierce current jagged with debris…” — Robert Hayden</a>

This project was one of the most challenging yet fun things to do! I enjoyed every process of it (including the frustration). At the end of this experience, I believe that building this app has made me understand things about programming that I would not have understood if I had not done this. The concepts I learned throughout the labs were tested throughout this app. However, this app has taught me to understand how those concepts in ruby work.

For those of you going through the bootcamp experience and are about to reach your first project, know that the challenge is worth it, don’t give up, and ultimately always be coding!

