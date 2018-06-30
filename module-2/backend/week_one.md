## Week One - Module 2 Recap

Fork this respository. Answer the questions to the best of your ability. Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week (which is a TON!).

Note: When you're done, submit a PR.

### Week 1 Questions

1. List the five common HTTP verbs and what the purpose is of each verb.

GET - Retrieves data from a web server.
PATCH - Changes a part of a resource.
PUT - Creates a resource, completely replacing what is at the URL (PUT is idempotent - crazy word!).
POST - Changes/creates a resource (update, change, or alter). Is NOT necessarily idempotent.
DELETE - Removes a resource (or requests that a resource be removed).

2. What is Sinatra?

A light work ruby framework used for writing web applications.

3. What is MVC?

Model, view, controller. A design philosophy that is common in the software industry, and taught at Turing.

4. Why do we follow conventions when creating our actions/path names in our Sinatra routes?

It's nicer for everyone if everything is consistent, and makes for easier data manipulation (I hope).

5. What types of variables are accessible in our view templates without explicitly passing them?

Instance variables. Yay for instance variables! Locals as well I suppose. I imagine global variables would work too, but I can already feel my mod 1 teachers glaring at me for mentioning global variables.

6. Given the following block of code, how would I pass an instance variable `count` with a value of `1` to my `index.erb` template?

  ```ruby
  get '/horses' do
    @count = 1
    erb :index
  end
  ```

  in ERB:

  ```
  <p><%= @count %></p>
  ```

7. In the same code block, how would I pass a local variable `name` with a value of `Mr. Ed` to the view?

```ruby
get '/horses' do
  @count = 1
  erb :index
  locals: {:name => 'Mr.Ed'}
end
```

8. What's the purpose of ERB?

Embedded Ruby! It allows us to combine html and ruby, to create some sort of super ruby/html hybrid. It also allows us to easily create templates for our web application.

9. Why do I need a development AND test database?

Testing often requires sanitizing a database with a gem like 'databasecleaner'. This becomes especially important when we're testing CRUD functions like create and destroy. We wouldn't want to manipulate ACTUAL customer data.

Not to mention loading a 15 million row database every time we run a test might get a little cumbersome.

10. What is CRUD and why is it important?

Create, read, update, destroy. It is the primary functionality required to have an app that isn't wholly terrible.

11. What does HTTP stand for?

Hypertext Transfer Protocol

12. What are the two ways to interpolate Ruby in an ERB view template? What's the difference between these two ways?

<% I'm a ruby method! I do stuff, but the user can't see me! %>

<%= I'm visible to the user! %>

13. What's an ORM? What does it do?

Object-relational mapping connects objects to tables in a relational database.

14. What's the most commonly used ORM in ruby (Sinatra & Rails)?

Rails! Sinatra died in 1998.

15. Let's say we have an application with restaurants. There are seven verb + path combinations necessary to provide full CRUD functionality for our restaurant application. List each of the seven combinations, and explain what each is for.

#### Create:
get '/restaurants/new': gets a form to create a new restaurant
post '/restaurants': creates a new restaurant based on form input

#### Read:
get '/restaurants': retrieves a list of all restaurants
get '/restaurants/:id': finds a single restaurant

#### Update:
get '/restaurants/edit/:id': gets a form to update an existing restaurant
put '/restaurants/:id': updates an existing restaurant based on form input

#### Delete:
delete '/restaurants/:id': deletes an existing restaurant

16. What's a migration?

An update to a schema. What's a schema you ask? A schema is how the data in a database is organized. Great question me!

17. When you create a migration, does it automatically modify your database?

Not necessarily. It merely updates the schema. We would need to seed the database or perform some other action to actually affect the contents of the database.

18. How does a model relate to a database?

A model represents a resource(row) in a database.

19. What is the difference between `#new` and `#create`?

New doesn't actually save anything to the database. You would have to say 'Foo.new' and then 'Foo.save'. Create can do both!

### Review Questions:  
20. Given a CSV file (“films.csv”) with these headers [id, title, description], how would you load these into your database to create new instances of Film?  

`
require 'csv'

CSV.foreach('films.csv', headers: true, header_converters: :symbol) do |row|
  Film.create(id: row[0],
              title: row[1],
              description: row[2]
              )
end

`

21. Given the following hash:
```
activities = {
  hiking: {cost: $0, supplies: ['hiking shoes', 'water', 'compass']},
  karaoke: {cost: $10, supplies: ['courage', 'microphone']},
  brunch: {cost: $35, supplies: ['mimosa flutes']},
  antiquing: {cost: $200, supplies: ['list of antique stores']}
}
```
How would I add 'granola bar' to things you should have when hiking?

`activities[:hiking][:supplies] << "granola bar"`

22. What are the 4 Principles of OOP? Give a one sentence explanation of each.

Encapsulation, abstraction, polymorphism, and inheritance.

Real talk, I had to look this up.

Encapsulation - Putting only relevant data in a single class and restricting the information it has access to.
Abstraction - Hiding unessential data from user.
polymorphism - The ability of an object to change behavior on runtime. A way for a subclass to override the methods of a parent class.
Inheritance - A way to reuse code (and keep your code DRY). Creating a new class by extending an existing class.


### Self Assessment:
Choose One: (erase the others)
* I was able to answer most questions independently, but utilized outside resources for a few

Choose One:
* I feel comfortable with the content presented this week
