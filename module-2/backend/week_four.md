## Week Four Recap

### Instructions
Fork or re-pull this repository. Answer the questions to the best of your ability.

Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week.

Note: When you're done, submit a PR with a reflection in the comments about how this exercise went for you.

### Week 4 Questions

####1. What is a cookie?

A cookie is a small text file stored on the client's computer when visiting a website that stores information (up to 4KB).

####2. What’s the difference between a session and a cookie?

Session's are stored on the server, and cookie's are stored on the client's computer.

####3. What’s a flash and when do you want to use flashes?

A flash is a way to display messages and alerts in actions. For example, you would want to use a flash message when a user fails to log in (perhaps by displaying a message that indicates the password or email are incorrect).

####4. Why do people say “HTTP is stateless”?

HTTP requests have no memory or context. They require a session or a cookie to be truly useful to users.

####5. What’s authentication? Explain.

Verification that the user is who they say they are. When I pick up a package at the post office, they might request my ID - this authenticates that I am who I say I am.

####6. What’s the difference between authentication and authorization?

Authentication is verifying my identity. Authorization is verifying the access that identity affords.

####7. What’s a before filter?

You can use a before filter, like before_action, to indicate that you would like to perform a method before a controller action. For example, if I frequently find a User, with "User.find(params[:id])" I might indicate that I would like to perform that action before show, destroy, create, and update.

####8. How do we keep track of a user once they’ve logged in?

By creating a session! We store their user ID as a session ID, which we can use to determine which part of the website they're authorized to visit.

####9. When do you want to namespace a resource? When do you want to nest a resource? What's the differences between those two approaches?

Namespace will preface the url with the parent path, and allow you to nest a controller. This seems to be most useful for organizational purposes, but in particular for building resources that only an admin can access.

####10. At a high level, what tools can you use to implement authorization? How would you use them?

I'm assuming you're talking about tools like Bcrypt, to encrypt a password, or sorcery or devise as a more full featured authentication and authorization platform. You can use namespace to nest admin controllers, admin? and current_user? helper methods in the application controller for authorization purposes, and conditional statements in individual controllers (and the view!).

####11. What's an enum, and what advantages does it offer? What data type needs to be in your database to use an enum? Where do you declare an enum?

It is NOT an enumerator. An enum is declared at the model level and can turn an attribute integer value (like a 0 or 1) into a string from an array in the corresponding index position. We have used it to determine a user's role (default or admin, or 0 or 1 respectively).

####12. What are some strategies you can use to keep your views DRY?

Partials are valuable. I also think that re-using classes and keeping a consistent style can help limit the amount of chaff in the view. Also, when using conditionals ( like <% if current_user && current_user.admin?) build appropriate methods. Also, using the & safe browsing operator in ruby can help save space (and also prevent nil errors when a page is loading).


### Reviews Questions
13. Given the following array of hashes, how would I print an alphabetical list of holidays?
```ruby
[
 {holiday: {name: "St Patrick's Day", supplies: ["Corned Beef and Cabbage"]}},
 {holiday: {name: "Halloween", supplies: ["Candy", "Costume"]}},
 {holiday: {name: "Hanukkah", supplies: ["Menorah"]}}
]
```  

given array_of_hashes

```ruby
array_of_hashes.inject([]) do |collector, holiday|
  collector << holiday[:holiday][:name]
  collector
end.sort.join(", ")

```


14. How would you clean incoming data to ensure "$300" or "300.00" is stored as 300?

```ruby
"$300".gsub(/\D/,'').to_i
```
### Self Assessment:
Choose One:
* I was able to answer most questions independently, but utilized outside resources for a few

Choose One:
* I feel comfortable with the content presented this week
