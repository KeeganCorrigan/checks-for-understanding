## Week Three Recap

### Instructions
Fork this repository. Be sure to pull the latest changes to your local repo. Answer the questions to the best of your ability.

Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week.

Note: When you're done, submit a PR with a reflection in the comments about how this exercise went for you.

### Week 3 Questions

##### 1. What is the entry at the command line to create a new rails app?

```
=> rails new <name_of_project> -T -d="postgresql" --skip-spring --skip-turbolinks
```

##### 2. What do Models generally inherit from in rails?

```
ApplicationRecord
```
##### 3. What do Controllers generally inherit from in a rails project?

```
ApplicationController
```

##### 4. How would I create a route if I wanted to see a specific horse in my routes file assuming I'm sticking to standard conventions and that I didn't want other CRUD functionality?

```
resources :horses, only: [:show]
```

##### 5. What rake task is useful when looking at routes, and what information does it give you?

```
rake routes
```
Provides all available routes specified in your config routes file.

##### 6. What is an example of a route helper? When would you use them?

```
horses_path
```

Would show the index of all horses! You would use the route helper when using link_to as well as in your tests.

##### 7. What's the difference between what `_url` and `_path` return when combined with a routes prefix?

url specifies the protocol, path only returns the uri portion. Url is absolute and path is relative.

##### 8. What are strong params and why are they necessary?

When we send params through a form for instance, we generally only want specific params (like a horse_name, or horse_breed), so in the HorsesController we would establish a private method that only allows certain params to be sent. It also prevents nefarious folk from assigning any value to any attribute.

##### 9. What role does `form_for` play in helping us create our forms?

form_for is a rails form helper that allows us to create or update a specific model.

##### 10. How does `form_for` know where to submit the user's input?

We assign an instance variable, like '@horses' to indicate what the form is for.

##### 11. Create a form using a `form_for` helper to create a new `Horse`.

```
<%= form_for @horse do |f| %>
<%= f.label :name %>
<%= f.text_field :name %>
<%= f.submit %>
<% end %>
```

##### 12. Why do we want to validate our models?

To verify that only valid information is saved to the database.

##### 13. What are the steps of the DNS lookup?

1. Client sends a request to the resolving name server.
2. Resolving name server checks with the root server who sends back more information about the top level domain (.com, .net).
3. Resolving name server checks the top level domain server (google, horse).
5. Resolving name server checks the authoritative name server (horse/index)
6. Resolving name server returns with the IP address after a tough journey. Take a break Resolving name server, you deserve it.


### Review Questions
14. How would you call the method `prance` from within the method `move` on a `Horse` instance?

```
class Horse
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def move
    prance
  end

  def prance
    puts "#{@name} prances"
  end
end
```

##### 15. Given the following hash:

```ruby
furniture = {table: {height: 3, color: "red"}, purchased: true}
```
What is the different between how you would return true vs returning 3?  

To return true:
```
furniture[purchased]
```

To return 3:
```
furniture[table][height]
```
##### 16. What is inheritance?

Passing methods to your children! In CSS, if you specific a body font-family, paragraphs will inherit them. In Ruby, a class and inherit from another class. In Rails, our controllers inherit from ApplicationController.

### Self Assessment:
Choose One:
* I was able to answer most questions independently, but utilized outside resources for a few

Choose One:
* I feel comfortable with the content presented this week
