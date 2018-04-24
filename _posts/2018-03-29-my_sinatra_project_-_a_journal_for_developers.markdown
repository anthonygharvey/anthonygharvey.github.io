---
layout: post
title:      "My Sinatra Project - A Journal for Developers"
date:       2018-03-29 16:37:35 -0400
permalink:  my_sinatra_project_-_a_journal_for_developers
---


For my Sinatra project, I chose to build an app that I’ve wanted to use but haven’t quite found.  Since I’ve been in Flatiron’s full stack developer program I’ve wanted to keep track of what I’m learning, see my learning/coding “streaks” and set goals for myself.  I’ve used a combination of [Day One](http://dayoneapp.com) for journaling, [Quiver](http://happenapps.com/) for organizing my notes and different goal tracking iOS apps.   Individually, these apps worked for their purposes, but they were too cumbersome for what I wanted; so I decided to make an app with the features I was looking for.

## The project requirements were:
1. Build an MVC Sinatra Application
2. Use ActiveRecord with Sinatra
3. Use Multiple Models
4. Use at least one `has_many` relationship on a User model and one `belongs_to` relationship on another model
5. Must have user accounts. The user that created a given piece of content should be the only person who can modify that content
6. Must have the ability to create, read, update and destroy any instance of the resource that belongs to a user
7. Ensure that any instance of the resource that belongs to a user can be edited or deleted only by that user
8. You should also have validations for user input to ensure that bad data isn't added to the database. The fields in your signup form should be required and the user attribute that is used to login a user should be a unique value in the DB before creating the user.# Enter your title here


## Getting Started
My first step was to map the models and relationships.  I wanted to be able to set goals with a specific time frame to commit and write journal entries to document my progress towards specific goals.

[image:80D65984-A76D-4280-B7E2-02B22FE470F6-6572-000019DE683A2AAD/E7C2AE90-F7BC-4A9F-8CB6-49FE1BB66541.png]

After that I used [Corneal](https://github.com/thebrianemory/corneal) to quickly setup the Sinatra scaffolding.  Thanks to [Brian Emory]([thebrianemory (Brian Emory) · GitHub](https://github.com/thebrianemory) for creating an awesome Ruby gem!

## Migrations and Models
Next I created the migrations and models for `user`, `entry` & `goal` and added the Bcrypt gem to allow users to have secure passwords saved to the database.

One thing I’ll remember for future Sinatra apps is that ActiveRecord comes with two awesome class methods: `validates_presence_of` and `validates_uniqueness_of`.  I spend some time creating helper methods to do what these functions already do in ActiveRecord out of the box.  Lesson learned.

[validates_uniqueness_of](http://api.rubyonrails.org/classes/ActiveRecord/Validations/ClassMethods.html#method-i-validates_presence_of) - Validates that the specified attributes are not blank and, if the attribute is an association, that the associated object is not marked for destruction. Happens by default on save.

[validates_uniquness_of](http://api.rubyonrails.org/classes/ActiveRecord/Validations/ClassMethods.html#method-i-validates_uniqueness_of) - Validates whether the value of the specified attributes are unique across the system

```ruby
class User < ActiveRecord::Base
	has_secure_password
	has_many :goals
	has_many :entries, through: :goals
	validates_presence_of :username, :email, :password, :first_name, :last_name
	validates_uniqueness_of :username, :email
end
```

After that, I used the tux gem to test the models and associations to make sure they were wired up correctly.

## Controllers and Views
Next I started on the controllers and views, building them incrementally and testing/verifying my assumptions along the way:
* stubbing a controller action and associated view to make sure the route is correct
* using `<% binding.pry %>` to make sure instance variables are being passed to the view correctly.
* building a form in the view and using `raise params.inspect` or `binding.pry` in the controller to verify params.

## Styling
I added Bootstrap at the end of the Fwitter lab and decided to include it early on with this project.  The CLI project was fun but I was ready to make an actual web app and adding styling to it would make it feel all the more real as I was building it.  I used the [Lumen](https://bootswatch.com/lumen/) theme from Bootswatch; which was straightforward to add to the project by including the `bootstrap.css`  link in the `<head>` tag in the `layout.erb` file and the `bootstrap.js` file at the end of the `<body>` tag; just before the closing `</body>` tag.

### Entry Content
I wanted to use something more than a `<textarea>` tag for the entry content.  I searched for both markdown and WYSIWYG editors.  After trying a few I settled on the Bootstrap WYSIWYG editor by [summernote](https://summernote.org/).  It was by far the most straightforward one to include and it has great documentation.

## Conclusion
Overall, this was a very fun project.  It was hard at times but well worth it to take an idea for an app I wanted to seeing it in front of me with the features I had in mind!  Well, most of the features…. a code editor with syntax highlighting would be nice!  The [Summernote Syntax Highlighting](https://epiksel.github.io/summernote-highlight/) plugin and [Ace](https://ace.c9.io/) editor look promising.

I’m still using Quiver (I have too many notes and snippets to switch) but I recently realized you can link to individual notes in MacOS, even from outside of the Quiver app!

The repository for this project is [here](https://github.com/anthonygharvey/developer_journal).

My next step is to deploy this app to Heroku.  It helped solve a problem for me and hopefully it will help others developers on their coding journey.
