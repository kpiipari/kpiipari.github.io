---
layout: post
title:  "Baby Steps - Sinatra portfolio project"
date:   2017-08-27 21:29:16 +0000
---


Deciding on the Sinatra portfolio project idea was surprisingly easy for me. Having a one year old daughter who is about to start walking and saying some meaningful words, my life has, and still is all about the first miletones. The first smile, the first roll over on her tummy, the first tooth, the first steps and words... 

What could be a better way to track all the firsts than a simple Sinatra web application?! So what can you do exactly?

1. Sign up as a parent
2. Add your child to your account
3. Enter milestones for your child

You can fork or clone Baby Steps from [here](https://github.com/kpiipari/baby-steps)


How did I get started? Once I had decided on a project, I quickly noted down what I wanted to have in my application.
It should have Parents, Children and Milestones. Parents should have a `username`, `email` and `password`. Children should have a `name` and a `date of birth`. Parents have many children and children can have many parents.
Milestones consists of `content`, `date` and `age` (the age of the child during the milestone). Milestones belong to a child and a child can have many milestones. Lastly, I quickly designed some layouts in [Sketch](https://sketchapp.com/) to decide what I should display on each route.


Here are few interesting facts that I learned during this project. After I had created my models, including a Child class I realised that the database needs be pluralized and when describing the relationship between the Parent and Child models I should, of course, be using the pluralized version.
I thought first that I would have to just use Childs (yikes) but luckily, I discovered that ActiveRecord automatically handles the [pluralized](https://apidock.com/rails/v3.0.0/ActiveRecord/Associations/ClassMethods/JoinDependency/JoinAssociation/pluralize) versions directly. This mean that I could have a Child class but in my Parents class I could describe the Parent's relationship as `has_many children` and my database table was named as `children`. 

Another little thing I learned was about using a `date type` as a database data type. Once I had completed the first migrations, I dropped into the console to play around with my models. One of my model classes, a `Child` has a name (`string` type) and a date of birth (`date` type). When I wanted to enter a date of birth, I got puzzled about what should I actually enter? Well, the answer was simpler than I though. I just had to enter a date as a string and Active Record converts it automatically to a correct Date object. However, note that you have to enter the date as as Date-Month-Year or Year-Month-Date format.

```
[1] pry(main)> child = Child.create(:name => "Franklin", :dob => "28/04/2015")
=> #<Child:0x007fa386610d88 id: 7, name: "Franklin", dob: Tue, 28 Apr 2015>

 pry(main)> child = Child.create(:name => "Joanna", :dob => "2015-01-30")
=> #<Child:0x007fa386b7f620 id: 14, name: "Joanna", dob: Fri, 30 Jan 2015>

pry(main)> child = Child.create(:name => "Marie", :dob => "1 August, 2016")
=> #<Child:0x007fa3863b9738 id: 10, name: "Marie", dob: Mon, 01 Aug 2016>
```

Lastly, I wanted to find a way to ensure that when a parent enters any data, all the leading and trailing white spaces are trimmed before the data is saved to the database. Luckily I found a nice gem [`auto_strip_attributes`](https://github.com/holli/auto_strip_attributes) to this job for me.  All you have to do is to add `gem "auto_strip_attributes", "~> 2.1"` to your Gemfile and `auto_strip_attributes :[attribute_name]` for each of your model classes. In my case, I added `auto_strip_attributes` to my Parent, Child and Milestone classes.

```
class Child<ActiveRecord::Base
    auto_strip_attributes :name
    has_many :child_parents
    has_many :parents, through: :child_parents
    has_many :milestones
	end
```

```
class Parent<ActiveRecord::Base
    auto_strip_attributes :username, :email, :password_digest
    has_many :child_parents
    has_many :children, through: :child_parents
    has_secure_password
	end
```

```
class Milestone<ActiveRecord::Base
    auto_strip_attributes :content, :age
    belongs_to :child
end
```

