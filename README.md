# Allrecipes

A Ruby interface to the Allrecipes API.
Allrecipes doesn't have an API, the requests are done using mechanize.

## Installation

Add this line to your application's Gemfile:

    gem 'allrecipes'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install allrecipes

## Usage

**Initialize scraper**
```ruby
recipes = Allrecipes.new
```

**Get all recipes**
```ruby
recipes.all #default sorted by popularity, limit 20.
```

**Get recipes by course**
```ruby
recipes.course("breakfast") #default sorted by popularity, limit 20.
```
List of courses: 
```ruby
[ "appetizer", "bread", "breakfast", "dessert", "drink","fruit", "herbs", "main", "salad", "soup", "meat", "pasta", "seafood", "wholegrains"]
```

**Get recipes by region**
```ruby
recipes.region("european") #default sorted by popularity, limit 20.
```

Specific options available
```ruby
recipes.region("french") #default sorted by popularity, limit 20.
```

List of regions available: 
```ruby
[
  "asian"
    "chinese" 
    "thai" 
    "japanese" 
    "filipino" 
    "korean" 
    "vietnamese" 
    "malaysian" 
    "pakistani" 
    "indonesian" 
    "iranian" 
    "bangladeshi" 
    "indian" 

  "african"
    "african_main"
    "moroccan"
    "south_african"
    "egyptian"

  "australian"

  "canadian"
    "vancouver" 
    "toronto" 
    "quebec" 

  "european"
    "italian"
    "uk"
    "french"
    "greek"
    "eastern_european"
    "german"
    "scandinavian"
    "spanish"
    "portuguese"
    "dutch"
    "austrian"
    "swiss"
    "belgian"

  "latin_american"
    "mexican" 
    "caribbean" 
    "south_american" 

  "middle_eastern"
    "lebanese" 
    "turkish" 
    "israeli" 
]
```

**Get recipes by ingredient**
```ruby
recipes.ingredient("apples") #default sorted by relevance, limit 21.
```

**Passing options to search** 

```#all, #region, #course, #ingredient``` all accept an options hash with the following paramters: limit, page & sort_by. 

**Limit**

Default & max limit is 20 for ```#all, #region & #course```. 
Defaut & max limit is 21 for ```#ingredient```.

```ruby
recipes.all({ limit: 10 })
recipes.ingredient("apples", { limit: 10 })
```
**Page**

For pagination it's as simple as passing the page number. 
If there are no results specified for that page, a blank array will be returned.
```ruby
recipes.all({ limit: 5, page: 3 }) #first 5 results from the 3rd page.
recipes.course("dessert", { page: 2 }) #20 results from page 2.
```

**Sort_By**

```#all, #region, #course``` are default sorted by popularity. Options available are popularity, date(newest first) and title(ascending).
If mentioned outside of this scope, will resort to default(popularity). 
```ruby
recipes.all({ page: 5, sort_by: "date" })
recipes.region("german", { sort_by: "title", limit: 10 })
```

```#ingredient``` search is default sorted by relevance. Options available are relevance, popularity and rating.
If mentioned outside of this scope, will resort to default(relevance). 
```ruby
recipes.ingredient("apples", { sort_by: "rating", page: 3 })
```


**Sample response**
```ruby
[
    {
      :name => "Lasagna",
      :image => "http://images.media-allrecipes.com/userphotos/250x250/00/03/24/32427.jpg",
      :servings => 12,
      :ingredients =>
        [
          {
            "quantity" => 1.0,
            "unit" => "pound", 
            "name" => "ground beef"
          }
        ],
     :directions => 
       [
         {
           "Bring a large pot of lightly salted water to a boil"
         }
       ]
    }
]
```

## Todo

1. Complex search with queries such as multiple ingredients, course, time etc.
2. Add prep time & cook time to results
3. Add nutrional info to results.
4. Add rating to results
5. Add user photos for recipe to results
6. Able to get popular recipes of the day.
7. Able to insert recipe URL directly. 
8. Able to add page URL directly.
