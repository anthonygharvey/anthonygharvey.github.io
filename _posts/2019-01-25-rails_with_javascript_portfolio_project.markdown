---
layout: post
title:      "Rails with JavaScript Portfolio Project"
date:       2019-01-26 03:28:27 +0000
permalink:  rails_with_javascript_portfolio_project
---


Refactoring my previous Rails app to respond with JSON and be more dynamic through JavaScript was challenging and rewarding.  It was challenging mainly because I put the project on hold and had to relearn some of the material.  It was rewarding because I was finally able to complete something that took a long time to.

One of the challenges I faced after starting the project again was how to pass parameters from the search box from JavaScript back to Rails, then filter the Item objects and render the result as JSON.  After a lot of trial and error (and Googling!) I came across the jQuery .serialize() helper function.

I originally placed the search functionality in ItemsController#index, but for this project I moved it to a private method and refactored it.

Original:

![alt text](https://anthonygharvey.com/assets/img/items_controller_original.png "Original Items Controller")


Current:

![alt text](https://anthonygharvey.com/assets/img/items_controller_current.png "Current Items Controller")




Overall, this was a fun project to work on and I’m excited to learn about React and Redux and start on the final one!

The repository for this project is located [here](https://github.com/anthonygharvey/shelter-gifts/tree/jQuery)
