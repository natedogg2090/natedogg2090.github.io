---
layout: post
title:      "Rails-JS Project: Reading Log SPA"
date:       2019-12-15 05:03:52 +0000
permalink:  rails-js_project_reading_log_spa
---


As an avid reader I thought it would be a great idea for me to create a basic reading log application that would help me keep track of the books I want to read and the books I've already read. The functionality is pretty simplistic, but it accomplishes a lot of the core pieces I'd want in a book log. Essentially, keep track of the book title, a brief summary, author and genre.

Additionally, I wanted to stay inline with the Single Page Application concept and thus, the simpler the features, models, etc. the better. In fact, this was something I found I had to spend some time thinking through as I began to code in an effort to minimize unnecessary work.

Once I had my three models in place (i.e. book, author and genre) I was ready to start coding.

I first began with the Book model has a title, summary and acts as my join table for the application with references to author and genre. You'll see this theme again when looking at my frontend code where my Books class does a lot of the heavy lifting in terms of functionality.

The Book Controller handle much of the functionality, but I also have index routes for Author and Genre in their own controllers to keep my code clean.

Skipping over the serializers, let's move into the frontend code.

Here I followed a similar patter creating files for Books class that instantiates a Book and pushes them into an array I access frequently with all my books. I've also instantiated Authors and Genres classes to both maintain clean code and separation of functions within their respective classes, but also the ability to utilize that funcationality with my Books class where users will spend the majority of the time interacting with my app.

As far as the fetch calls, I have a GET request to the index route to get all Books, Authors and Genres. I also have a POST route for creating new Books that also checks for Authors and Genres using find_or_create_by. Finally, I have a simple Update method that listens for a checkbox to change, i.e. become checked to then make a PATCH request to the API updating the "complete" status in the DB to obviously indicate I've read this book.

Check it out: [reading-log-spa](https://github.com/natedogg2090/reading-log-spa)


