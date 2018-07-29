### Week 5 Questions

Re-pull from this respository. Answer the questions to the best of your ability. Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week (which is a TON!).

Note: When you're done, submit a PR.

### Week 5 Questions
####1. How do we make flash messages display on a page?

In the controller for the action:

```
flash[:alert] = "This is a flash message"
```

In your application.html.erb:

```
<% flash.each do |name, msg| %>
  <%= content_tag :div, msg, class: name %>
<% end %>
```

####2. Where is cart information/temporary information usually stored?

Typically in the session hash.

####3. What might be some reasons not to store a cart in our database? Are there any reasons why we would want to persist that information?

Space constraints in our database might prevent cart storage. I imagine there is valuable data to be collected on un-checked out carts that persist with users.

####4. What is the purpose of the asset pipeline?

A framework to concatenate, minify, precompile, and fingerprint.

####5. Why do we precompile our assets?

Browsers only recognize html, css, and javascript, so if we want to use scss or coffeescript it needs to be precompiled so a browser understands it.

####6. What do each of the following tags do?

```
<%= stylesheet_link_tag "application" %>
```

Allows every view to access all of our css (or scss) files.

```
<%= javascript_include_tag "application" %>
```

Allows every view to access all of our .js files.

```
<%= image_tag "rails.png" %>
```

This is an image tag that links to an image stored in assets.

####7. What are some of the elements of a great read me? What are some of the benefits of taking the time to update a readme for our project?

README's should include:

* What the app/gem/code is and what problem it solves
* How to configure and setup the app/gem/etc.
* Created by and contact information

A proper readme allows other users to actually, you know, use the thing you built. Without a proper readme using a complex gem would be impossible.

####8. What are the top four accessibility issues that we as developers should be aware of?

I don't know if this was covered specifically in class or if there was a reading on it, but there are far, far more than four:

 * screen readers require syntactic tagging
 * color scheme should not be essential
 * images require alt tags
 * literacy should not be assumed
 * buttons and icons should be large, easy to see, and easy to interact with

and that's just off the top of my head.

####9. `before_save` is an example of a what? Where in our Rails application would we find a `before_save`?

This is a call_back and will generally be found in the model.

####10. Given the following object, how would we create a scope for all users who are active?

```ruby
User.create(name: "Happy", active: true)
```

```ruby
class User < ActiveRecord::Base
  scope :user, -> { where(active: true) }
end
```

####11. What is the difference between a scope and a class method?

My understanding from my brief reading seems to indicate that scopes ARE class methods. It sounds like internally Rails converts a scope into a class method.


### Review Questions:  
####12. Given the following hash:  

```ruby
{cart: {"17" => 4, "204" => 52, "29" => 22}}
```

  12a. How would you add item with id of 48 with a quantity of 4?

  ```ruby
  session = {cart: {"17" => 4, "204" => 52, "29" => 22}}
  session[cart][item.id] = quantity OR
  session[cart]["48"] = 4
  ```

  12b. How would you increase the quantity of item 29?

  ```ruby
  session = {cart: {"17" => 4, "204" => 52, "29" => 22}}
  session[cart]["29"] += 1
  ```

  12c. How would you find out how many items your user is thinking about purchasing?   

  ```ruby
  session = {cart: {"17" => 4, "204" => 52, "29" => 22}}
  session[cart].values.sum
  ```

####13. What is polymorphism? How does it relate to duck-typing? What are two ways you use this in everyday Rails applications?  

Polymorphism is the ability to redefine variables or methods. .to_s can be redefined within a class to perform a different function.

Duck typing allows for runtime polymorphism, also you don't need a type in order to invoke an existing method on an object - if a method is defined on it, you can invoke it.

####14. How would you clean the string "(630) 854-5483" to "630.854.5483"?  

```ruby
"(630) 854-5483".gsub(/[^0-9]/, "").insert(3, ".").insert(7, ".")
```


### Self Assessment:
Choose One:
* I was able to answer a few questions independently, but relied heavily on outside resources

Some of these felt like they weren't covered in module 1 or 2, duck typing specifically, but also accessibility issues and scope.

Choose One:
* I feel comfortable with the content presented this week
