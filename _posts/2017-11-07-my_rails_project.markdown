---
layout: post
title:      "My Rails project"
date:       2017-11-07 19:55:37 +0000
permalink:  my_rails_project
---


I try to draw ideas of my current life for my projects. I've recently cleared out cupboards and draws from baby stuff that we no longer need, or my daughter has grown out of. In my ideal world, I would maybe save these, if I ever need them again. However, I like to be organised and as I don't have much storage space, I have just sold or given away lot of stuff. 

## Ideas and planning
This gave me an excellent idea for my Rails project -- a family market place where you can list your baby items for others to borrow. So in simple terms, you list your items such as a stroller, snow suits, baby bouncer etc that you no longer need and you can browse items listed by other users. If you find something you would like to borrow, you can reserve an item with a click of a button and that item is now reserved to you and you can see the contact details of the owner so that you can contact the owner to arrange to collect (and later return) the item. Yes, sorry, at the moment you have to still do this bit manually. 

First of all, I was positively surprised how relatively easy and fun the project was for me. I really pat myself on the back for **planning** my project well before starting to work on it. I used draw.io to map out all the models and associations I knew my app would need. This became one of the best ideas I had. I can't tell how many times I went back to just look at my diagram, showing all the associations and database columns. It also made it really simple for me to write down all
database migrations on one go.

## Pretty with Bulma
CSS styling is not required for this project but I couldn't let my codewise beautiful app be looking like it belongs to the 1995. So once I had most of the project done, I added a CSS framework to my application. This was also fun as I hadn't done this before and I didn't really know how it's supposed to work. Turns out it was much simpler than I thought. I also learned that you need those mystical header tags that are included by default in the application.html.erb file. So whatever you do, don't delete `<%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>` or `<%= csrf_meta_tags %>
`. So which CSS framework did I end up using? I used [Bulma](https://bulma.io/) and I loved it! However, I didn't want to spend too much time on the CSS layout but it's already looking way better than with the default layouts.

### Customising Devise views 

I used Devise for user sign up and authentication. I think it's relatively straightforward, but you have to do few tricks to get a custom CSS framework working for the sign up and login views (in my case) as the default Devise views are bundled inside the gem.

1. run `rails generate devise:views` to make the views such as sign up and login available in the views folder
2. Go to `config/initializers/devise.rb file`, uncomment and set `set config.scoped_views = true` to true inside the 


## Debugging

I had an issue where when I tried to update an item with a tag (via a nested form), I always got a transaction rollback in my log and the tag value wasn't updated. I really struggled to see what was the problem. Once I added `Rails.logger.info(@item.errors.messages.inspect)` to the update action, I immediately figured the issue by looking at the console. Instead of just saying `rollback transaction` I got `rollback transaction {:"tags.name"=>["can't be blank"]}`. Voilà, it was a validation issue.

## Summary

I really had fun time working on the Rails project. The key is to plan your project well before you start it, read the Rails guides and enjoy it! Checkout my Rails project [here](https://github.com/kpiipari/family_market_app).

