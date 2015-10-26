# Building Nested Hashes

## Objectives

In this lesson, we'll be taking a closer look at multidimensional, or nested, hashes. By the end of this lesson, you should be familiar with:

* The difference between single level and nested hashes
* How to add data to a nested hash

## Nested Hashes

We are used to seeing single level hashes that looks like this:

```ruby
jon_snow = {
  name: "Jon",
  email: "jon_snow@thewall.we"
}
```
However, what if we want to have a more complicated system that can catalog several people. A nested hash will be particularly useful in this case. 

Let's say we have the following nested hash: 

```ruby
contacts = {
  "Jon Snow" => {
    name: "Jon",
    email: "jon_snow@thewall.we", 
    favorite_icecream_flavors: ["chocolate", "vanilla"]  },
  "Freddy Mercury" => {
    name: "Freddy",
    email: "freddy@mercury.com",
    favorite_icecream_flavors: ["strawberry", "cookie dough", "mint chip"]
  }
}
```
### Adding Information to Nested Hashes

#### Example 1:

Your good buddy Jon Snow has just tried mint chip ice cream for the first time. He loved it a lot and now you need to add "mint chip" to his list of favorite ice creams. We already know how to access the array of ice cream flavors that constitute the value of the `:favorite_icecream_flavors` key: 


```ruby
contacts["Jon Snow"][:favorite_icecream_flavors]
#  => ["chocolate", "vanilla"]
```

How can we add a flavor to the list? Well, `:favorite_icecream_flavors` is an array, so we can use the same syntax as above to access that array along with our old friend `<<` (the shovel method) to add an item to the array. There are two ways we can do this. Let's take a look. 

####Option 1:

```ruby
contacts["Jon Snow"][:favorite_icecream_flavors] << "mint chip"
```
####Option 2: More verbose

If the above option isn't clear, we can break it down step by step.

* First, grab the value (which itself is another hash) of the "Jon Snow" key, and store it in a variable called `jon_snow`: `jon_snow = contacts["Jon Snow"]`
* Second, grab the value of Jon Snow's favorite ice cream, and store that array in a variable: `jons_fav_ice_cream = jon_snow[:favorite_icecream_flavors]`
* Third, add the new ice cream to `jons_fav_ice_cream` using the shovel (`<<`) operator: `jons_fav_ice_cream << "mint chip"`

```ruby
jon_snow = contacts["Jon Snow"]
jons_fav_ice_cream = jon_snow[:favorite_icecream_flavors]
jons_fav_ice_cream << "mint chip"
```

puts contacts 
#  => {
  "Jon Snow" => {
    name: "Jon",
    email: "jon_snow@thewall.we", 
    favorite_icecream_flavors: ["chocolate", "vanilla", "mint chip"]
  },
  "Freddy Mercury" => {
    name: "Freddy",
    email: "freddy@mercury.com",
    favorite_icecream_flavors: ["strawberry", "cookie dough", "mint chip"]
  }
}
```

#### Example 2: 

Now let's say that you want to add a whole new key/value pair to your Jon Snow contact—his address. In a simpler hash with just one level of key value pairs, we've already learned how to add new key/value pairs. Here's a reminder: 

```ruby
hash = {first: "first value!", second: "second value!"}
hash[:third] = "third value!"

puts hash
#  => {first: "first value!", second: "second value!", third: "third value!"}
```

In a nested hash, we can add new key/value pairs in a similar way. We need to first access the level of the hash to which we want to add a key value pair, and then we can create a new key value on the second level using the same notation. Since we want the `"Jon Snow"` key to include a new key/value pair of his address, the implementation should look like this: 

```ruby
contacts["Jon Snow"][:address] = "The Lord Commander's Rooms, The Wall, Westeros"

puts contacts
  #  => 
  {
    "Jon Snow" => {
       :name=>"Jon", :email=>"jon_snow@thewall.we", 
     :favorite_icecream_flavors=>["chocolate", "vanilla", "mint chip"], 
     :address=>"The Lord Commander's Rooms, The Wall, Westeros"
    }, 
    "Freddy Mercury"=> { 
     :name=>"Freddy", 
     :email=>"freddy@mercury.com", 
     :favorite_icecream_flavors=> ["cookie dough", "mint chip"]
    }
  }

```