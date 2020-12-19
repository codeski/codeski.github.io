---
layout: post
title:      "Sinatra Application Building & Protecting"
date:       2020-12-18 20:13:29 -0500
permalink:  building_a_sinatra_application
---

Sinatra has allowed me to create an application with a Domain Specific Language(DSL) using Models, Views, and Controllers(MVC). Basically, you can play with the application in the browser.
## What my app does
#### The application is called the ***Hobby Gear App*** 
It's an app where users can log in/out, create, read, update and delete hobbies that will associate to the user and items that will belong to a specific hobby. All of these model objects will be stored in a database using Active Record.

My 3 models: 
```
class User < ActiveRecord::Base
    has_secure_password
    validates :name, presence: true
    validates :email, presence: true
    validates :email, uniqueness: true

    has_many :hobbies
    has_many :items, through: :hobbies
end

class Hobby < ActiveRecord::Base
    validates :name, presence: true
    
    belongs_to :user
    has_many :items
end

class Item < ActiveRecord::Base
    validates :name, presence: true
    
    belongs_to :hobby
end
```

Our User passwords are encrypted with the `gem 'bcrypt'`, which allows us to call the method `has_secure_password`. In order for this to work the password needs to be saved as a `t.string :password_digest` in the users table.  With this gem no one will be able to view actual passwords that are saved to our database.

No bad data can be persisted into the database because of our Active Record validations written in our models. User must have a name, email, and that email must be unique. A hobby or item must at least have a name `validates :name, presence: true`. If someone enters bad data it will trigger error messages to display in the view. 

## My biggest takeaway
#### Making an application hackerproof
The `has_many` / `belongs_to` relationships combined with the helper methods help make the applications Views and Controllers hacker proof. 
```
helpers do

   def logged_in?
      !!session[:user_id]
   end

   def current_user
      @current_user ||= User.find_by(id: session[:user_id])
   end
	 
end
```
All post, patch and delete requests are protected using 
```
if logged_in? && current_user == hobby.user
     or
if logged_in? && current_user == item.hobby.user
```
These high level relationships allow us to make sure the User associated with the object and current_user are identical and have the permission to navigate to that View and/or Controller. All post, patch and delete requests must be protected in the views and controllers to make sure we can't be hacked in the dev tools or through our routes. 
