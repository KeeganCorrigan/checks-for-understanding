## Week Two - Module 2 Recap

Fork or re-pull this respository. Answer the questions to the best of your ability. Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week (which is a TON - YOU are a web developer!!!).

Note: When you're done, submit a PR.


### Week 2 Questions

####1. At a high level, what is ActiveRecord? What does it do/allow you to do?

Active record is an ORM that allows us to query a SQL database in sinatra/rails.

####2. Assume you have the following model:

```ruby
class Team << ActiveRecord::Base
end
```

What are some methods you can call on `Team`? If these methods aren't defined in the class, how do you have access to them?

```
.count, .all, .group, .sort, .where, .find, .join, .maximum, .minimum (and more!)
```

The class inherits from Active Record so we have access to the vast library of Active Record methods.

####3. Assume that in your database, a team has the following attributes: "id", "name", owner_id". How would you find the name of a team with an id of 4? Assuming your class only included the code from question 2, how could you find the owner of the same team?

```
Team.find_by(id: 4).name
```
All we have is the owner ID, and since I see no other tables, and the team does not 'belongs_to :owner' so technically we can't find the owner. I'm going to assume owner_id is a foreign key that belongs to an owner table and that I can find the owner via id, so:

IF owner knows about the team

```
Owner.find(4).name
```

OR

```
Owner.find_by(id: Team.find(4).owner_id)
```

OR (if Team belongs_to :owner)

```
team_1 = Team.find(4)
team_1.owner
```

4. Assume that you added a line to your `Team` class as follows:

```ruby
class Team << ActiveRecord::Base
  belongs_to :owner
end
```

Now how would you find the owner of the team with an id of 4?

Oops! See above!

```
team_1 = Team.find_by(id: 4)
team_1.owner
```

5. In a database that's holding students and teachers, what will be the relationship between students and teachers? Draw the schema diagram.

If students only have 1 teacher at a time, the model will look like:

```ruby
class Student << ActiveRecord::Base
  belongs_to :teachers
end
```

```ruby
class Teacher << ActiveRecord::Base
  has_many :students
end
```

The schema looks like:

```ruby
  create_table "students"
    t.string "first_name"
    t.string "last_name"
    t.integer "teacher_id"
    t.integer "current_score"

    t.timestamps
  end

  create_table "teachers"
    t.string "last_name"
    t.integer "course_id"
    t.string "disposition"

    t.timestamps
  end
```

Here's some table *ASCII* art

```
Students table 		| Teachers Table
______________		| ______________
ID					| disposition
first_name			| last_name
last_name			| course_id
teacher_id----->	| ID
current_score		|

```

####6. Define foreign key, primary key, and schema.

##### Foreign Key - 
A primary key from another table in a database as a column in a different table. The relationship part of a relational database.

##### Primary Key - 
The unique ID value assigned to each row of a table.

##### Schema - 
The organization of data in a database.

####7. Describe the relationship between a foreign key on one table and a primary key on another table.

The foreign key on one table is the unique primary key on a different table. It provides the link between the tables.


8. What are the parts of an HTTP response?

The head and body.

In the head you will have:

```
The protocol - HTTP/1.1
The status code (2** good, 4** bad)
Content length (120)
Content type (text)
```

### Optional Questions

####1. Name your five favorite ActiveRecord methods (i.e. methods your models inherit from ActiveRecord) and describe what they do.

How can I pick, I love them all like my children.

```
AS
```
This was a new one, but it allows us to create a new column in a table and call it whatever we want. Seems to work well a .joins.


```
JOINS
```

Still getting used to this one, but it allows us access to another tables (specified) columns so that we can perform interesting queries using columns from two or more tables.

```
COUNT
```

Super simple but very powerful. It will tally up the number of rows matching the query. 

```
Students.where(first_name: "Sam").counts
=> 4
```

```
GROUP 
```
Returns an array of rows that are, get this, grouped. Plays well with others, like count.

Student.group(teacher_id)


```
CREATE
```
New *and* SAVE in one place, what will they think of next? Allows us to skip a step when adding a row to a table.


####2. Name your three favorite ActiveRecord rake tasks and describe what they do.

```
rake db:create_migration NAME=create_<insert table name> 
```
Creates our migration file! We build out what data types our table will have, and what the column names will be here. 


```
rake db:migrate
```
Performs the actual table migration and updates the schema.

```
rake db:{drop,create,migrate,seed}
```
This is less of a task and more like... uh, 4 tasks. Learning that we could string multiple rake database tasks together in curly braces was powerful.

####3. What two columns does `t.timestamps null: false` create in our database?

```
created_at and updated_at!
```

####4. In a database that's holding schools and teachers, what will be the relationship between schools and teachers?

```
class Teacher 
	belongs_to :school
end

class School 
	has_many :teachers
end
```
####5. In the same database, what will you need to do to create this relationship (draw a schema diagram)?

```
  create_table "teachers"
    t.string "last_name"
    t.integer "school_id"
    t.integer "level_of_despair"

    t.timestamps
  end

  create_table "schools"
    t.string "school_name"
    t.string "address"

    t.timestamps
  end
```

Here's some table *ASCII* art

```
Teacher table 		| Teachers Table
______________		| ______________
ID					| school_name		
last_name			| address
school_id----->		| ID
level_of_despair	|

```

####6. Give an example of when you might want to store information besides ids on a join table.

A table that holds customer_ids and order_ids might also hold totals or sub-totals for easy access.


####7. Describe and diagram the relationship between patients and doctors.

```
class Patient
	belongs_to :doctor
end
```

```
class Doctor
	has_many :patients
end
```


```
  create_table "Patient"
    t.string "first_name"
    t.string "last_name"
    t.integer "doctor_id"
    t.integer "how_much_does_it_hurt_on_a_scale_of_1_to_10?"

    t.timestamps
  end

  create_table "doctors"
    t.string "last_name"
    t.integer "hospital_id"
    t.string "address"

    t.timestamps
  end
```

####8. Describe and diagram the relationship between museums and original_paintings.

```
class Museum
	has_many :original_paintings
end
```

```
class OriginalPainting
	belongs_to :museum
end
```

```
  create_table "Museums"
    t.string "name"
    t.string "address"

    t.timestamps
  end

  create_table "original_paintings"
    t.string "title"
    t.integer "artist_id
    t.integer "museum_id"
    t.bigint "cost"

    t.timestamps
  end
```

####9. What could you see in your code that would make you think you might want to create a partial?

Every nav bar ever. 

Forms. Footers. Any sort of repeated code in erb documents that spans more than a few lines.

KEEP IT DRY.

That means, don't repeat yourself.

#####I'll say it again:

don't repeat yourself.

### Self Assessment:
####Choose One:

* I was able to answer most questions independently, but utilized outside resources for a few

####Choose One:

* I feel comfortable with the content presented this week

