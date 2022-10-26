---
title: OOP in JavaScript
publishDate: 07 Feb 2021
description: Talking about Object-Oriented Programming using JavaScript
---

## What is an Object?

Ruby programming language is often referred to as being the language where everything is an Object.

```ruby
2.6.1 :001 > Class.ancestors
=> [Class, Module, Object, Kernel, BasicObject]
```

If you look at this code snippet taken from a terminal, we are calling .ancestors to trace the inheritance of Class . This reveals the parent tree to us and allows us to see that in fact, all Ruby is actually an Object that you can trace all the up to the BasicObject. Well, JavaScript is similar in that literally almost everything in JS is an Object. You can spend hours debating the pros and cons of this or discussing how when JS was created it was not expected to be as popular as it is today, so they made everything Objects.

```javascript
> typeof{Function}
'object'
```
But I digress, JS is in fact all Objects, and well what in the world is an Object? Objects are ways to contain data and code that can be used to represent real-world things (objects) into our code. 

In Object-Oriented Programming (OOP), programmers ask themselves how can this object be best represented? What makes this object unique, how can you best recognize it?

For example, how would one represent a Dog in code? Do we have to think about what makes a dog a dog? What are the attributes associated with being a dog? We know a dog can have a name, it can speak by barking, it can wag its tail. To best represent this, we use Classes and constructors to add these attributes to a dog whenever a program creates it.

```javascript
// assume a constructor was created to give a dog instance these methods and attributes //
let sparky = new Dog("Sparky", "woof")
sparky.name = "Sparky"
sparky.speak = "Woof"
```

In JS OOP, you can use ‘dot-notation’ to call methods onto the instance of the object. So object.method() in our sparky example, sparky.name(“Sparky”) we are using that fancy dot-notation to call the name method on sparky which is an instance of the Dog class. In the parenthesis, we are assigning the value of “Sparky” as the name.
Coding in OOP can get really meta and philosophical which strikes up my alley with having a background in History.

## What is Syntactic Sugar?

ES6 introduced a familiar (if you know other languages) concept to the world of JavaScript programming, the introduction of Classes. As previously noted, Classes are commonly found in other programming languages such as Java, Ruby, C#, and PHP. When you write these Classes you are mimicking these languages to format your code in a new way. Under the hood, JavaScript classes are still those same Prototypes, Inheritance, and that ES5 syntax. Hence the name syntactic sugar, a convenient syntax that lets you write that syntax that is familiar to those other languages!

## My JS Project using OOP

Here is an example of a Post class I used in my JS project.

```javascript
class Post {
  static allPosts = []
  constructor(post){
    this.id = post.id
    this.content = post.attributes.content
    this.comments = post.attributes.comments
    Post.allPosts.push(this)
  }
}
```

I am declaring the Post class by using <strong> class Post {} </strong> as soon as an instance of my Post is fired up, we immediately call the <strong>constructor(){}</strong> method to assign attributes to the post.

## This?

In the code snippet above, you may have noticed the <strong>this.id = post.id </strong>. Well, what is this? This is one of those topics that can get really meta, but the this keyword refers to the object that it belongs to. This can have multiple meanings and associations but this is where context is very important in JavaScript. So in this.id = post.id the this keyword is referring to the Post class object and it's assigning the value to it. This can get really murky and muddy but always remember the context of where this is being used.
