---
layout: post
title:      "Rails Project: Coffee Review"
date:       2019-08-30 18:46:23 +0000
permalink:  rails_project_coffee_review
---


As a fan of coffee I thought what better way to express my pleasure and enjoyment for coffee than to create an application that would mimic the ability to buy, track and investigate new types of coffee, while at the same time offering my own notes to the community that could be fostered around this application.

Starting with the DB first, I've created a few tables that are relevant to my application at a basic level. They are as follows:

* Purchase
* Roasts
* Roaster
* Users

As you can probably guess the Purchase table handle the joins of Roasts and Users. The rest basically speak for themselves.

Moving into the models and associations is where I actually started to explore a little bit when it came to meeting that use of ActiveRecord Scope and Query methods. This wasn't entirely obvious to me at first why I should use Scope over a regular class method or why these would be part of the requirements for the project given the simplicity of my application if this would really be required.

As I look back on it I can see the holes in my thinking and some of the advantages to using Scope methods, but still trying to figuring thte best applications for it as a whole. Quick aside, when I realized that I was actuallly thinking in this context made me feel  like I had turned another corner in my development because I no longer just look at the requirement and try to implement, but rather taking the time to actually thinking about how/when I want to use these tools.

For those of you also curious to learn more I found a few interesting blog posts on the topic I'll share below that helped codify these concepts in my brain.

* [Rails Guide](https://guides.rubyonrails.org/active_record_querying.html#scopes)
* [Scopes vs. Class Methods](https://medium.com/le-wagon/what-are-named-scopes-and-how-to-use-them-rails-5-5a0444d8b759)
* [Preload Scopes](https://www.justinweiss.com/articles/how-to-preload-rails-scopes/)
* [Rails Scopes](https://devblast.com/b/jutsu-11-rails-scopes)

A scope method I created in my applications was:

```
class Purchase < ApplicationRecord
       scope :purchased_by, -> (user) {where("user_id == ?", user.id)}

end
```

I'm trying to get back all the roasts purchased by a particular user to then display them all on the user show view.

In the UsersController I have the following:

```
  def show
    @user = find_user(session[:user_id])
    @purchases = Purchase.purchased_by(@user)
  end
```

This creates an instance variable called ```@purchases``` and passes ```@user``` to the ```purchased_by``` method giving me an array of roasts purchased by this particular user.

The view contains a simple loop that iterates over this array and displays all the roasts in an unordered list.

As you may have noted the controller is much cleaner this way than opposed to having ```@purchases``` contain all purchases to then be iterated on and extracted within the view. Too much logic in the view and unscalable with a large DB with rows and rows of coffee....yummmmm.
