---
layout: post
title:      "Sinatra Project: Newborn Nap Tracker"
date:       2019-01-08 23:18:20 -0500
permalink:  sinatra_project_newborn_nap_tracker
---


My wife and I recently had a baby boy and as is common we were not getting much sleep, or consistent sleep anyway. We both felt like zombies plodding through our daily lives and one of the struggles I had was committing a bunch of timestamps to short term memory remembering when was his last nap, how long was it and what was he like from day-to-day depending on how he had slept either the day previous or the length of his previous nap.

Needless to say, I wanted to come up with a solution for us to track my son's sleeping patterns without relying on our own memories, which if we're being honest were pretty unreliable in a state of sleep deprivation. Remembering how many naps a day, how long, did he go down easily or was he fussy to then make any sort of assessments or conclusions about patterns was nearly an impossible task.

So, I thought why not apply my newfound knowledge to a real world problem by creating a simple application to track his naps, i.e. the Newborn Nap Tracker (title is a work in progress).

For the project, I began by mapping out my mapping out my application, which resulted in three models: Users, Babies and Naps with the following relationships:

* User has_many Babies
* Babies belongs_to User
* Babies has_many Naps
* Naps belongs_to Babies

Once I had mapped out the models and relationships I was ready to establish the framework for my application. Using [Corneal](http://thebrianemory.github.io/corneal/) I was able to quickly generate a Sinatra template to begin my project and jumped right into working on setting up my DB schema for each model using ActiveRecord via rake migration commands directly from the terminal. The resulting schema:

```
ActiveRecord::Schema.define(version: 20181119031833) do

  create_table "babies", force: :cascade do |t|
    t.string  "name"
    t.date    "birthday"
    t.integer "user_id"
  end

  create_table "naps", force: :cascade do |t|
    t.datetime "start_time"
    t.datetime "end_time"
    t.text     "notes"
    t.integer  "baby_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "name"
    t.string "email"
    t.string "password_digest"
  end

end
```

Now that I had my DB and corresponding models established it was time to start working on the application controllers. I have setup my application to have an Application Controller handling GET requests for the main index and welcome pages along with PATCH and DELETE requests. I've also created a separate controller file for Users, Babies and Naps to handle the GET and POST requests which I then mounted in the `config.ru` file.

Finally, it came time to start adding my views, which were built in parallel with the controller requests. File tree for reference:
```
| views
	| babies
		|- edit
		|- index
		|- new
	| naps
		|- edit
		|- index
		|- new
		|- show
	| users
		|- login
		|- signup
```

A functional application to add some order to a disorderly, monotonous and tiresome task. Although my son still isn't consistently sleeping through the night, we'll be better prepared to make decisions about how to eventually get him there.
