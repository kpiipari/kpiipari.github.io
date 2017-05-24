---
layout: post
title:  Grater - your CLI cooking friend
date:   2017-05-24 20:11:32 +0000
---


My first portfolio project, a CLI Data Gem Project is finally finished, yay :) The purpose of the project was to build my own Command Line Interface (CLI) application that accesses data from an external web source. 

My first task was to think of an application I would like to use myself. I like cooking and I often look at cooking recipes online but it's annoying to read the instructions and ingredient list from websites full of advertisements. That's how I settled with Grater. A neat CLI application that prints a list of recipes from which a user can choose a recipe. Once a user has told Grater their chosen recipe, Grater prints out the list of ingredients, followed by cooking instructions. 

Now that I knew what I wanted my application to do, I needed to find a website with recipes. Well, at least I wasn't short of options to choose from. There are literally thousands of online cooking resources. I first shortlisted about 3-5 sites. I then compared how they were constructed and inspected the websites with developer tools. I wanted to find a good data source that would be relatively straightforward to scrape, but a complex enough that allowed me to go at least two levels deep into the data structure.

I finally settled with [BBC goodfood](https://www.bbcgoodfood.com/), knowing that it would have at least one challenging part which I am going to talk about a bit later. 

BBC goodfood is a large site with countless recipes. I actually don't like to navigate [the main recipe page](https://www.bbcgoodfood.com/recipes) which contains over 10 different recipe categories such as [Healthy](https://www.bbcgoodfood.com/recipes/category/healthy), [Cakes & baking](https://www.bbcgoodfood.com/recipes/category/cakes-baking) and [Cuisines](https://www.bbcgoodfood.com/recipes/category/cuisines). Each category contains anywhere from 10 to over 60 recipe collections and each collection contains tens of different recipes. For example the [Cakes & baking](https://www.bbcgoodfood.com/recipes/category/cakes-baking) category has 32 recipe collections such as [Brownie](https://www.bbcgoodfood.com/recipes/collection/brownie) with 26 recipes, [Cheesecake](https://www.bbcgoodfood.com/recipes/collection/cheesecake) with 40 recipes and [Gluten-free cake](https://www.bbcgoodfood.com/recipes/collection/gluten-free-cake) with 18 recipes.

As you can notice, BBC goodfood can be divided up to three levels -- categories, collections and individual recipes with ingredient lists and methods. This is exactly what Grater offers to its user.

When a user starts Grater, it lists 12 different categories to choose from. Users interact with Grater by typing the number corresponding to a category. Once a user types in a category number, Grater lists all collections beloging to that category. By typing the collection number, Grater lists all the recipes for the chosen collection. Finally, the user can choose a recipe and Grater prints out the list of ingredients and steps to follow the recipe.

One of the most challenging part of the project was find a way to scrape the ingredients list correctly. Many of the ingredients include a mouse hover effect to a glossary with details about the ingredients. My first attempts scraping the recipe sites included all the glossary information, grrr. Finally after a lot of reseach and `pry`ing I discovered that I can remove child nodes, hurrah. The rest of the actual scraping part was easy after this discovery.

I wish I had watched the walkthrough vidoes and other linked videos before I embarked on my project as it would have made it easier to understand how to set up everything. I also found it challenging to create a gem that can be executed. However, I'm proud to say that I manged it in the end and I published my [recipe-grater](https://rubygems.org/gems/recipe-grater) gem at [RubyGems.org](https://rubygems.org). Checkout [recipe-grater](https://rubygems.org/gems/recipe-grater) next time you want to cook or bake something new.







