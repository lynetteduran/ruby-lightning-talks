# Acts-as-taggable-on

Handles generic tagging in the view by displaying select model attributes, behaviors, and connections to other models!


## Whats So Great About Acts-as-taggable-on

<li> Adds tag and tag clouds/calculations!
<li> Can add more than one tag per model (upgrade from acts-ass-taggable-on-steroids)!


## Why use Acts-as-taggable-on

From the af83DEV website, article: "Playing with acts as taggable on" -- *"There are several Ruby on Rails plugins for tagging. The first one was acts_as_taggable by DHH. It was simple and limited in functionality, so it was forked several times. The most popular version of these forks is acts_as_taggable_on_steroids, which is pretty performant, has tag cloud calculations and offers extras such as tests.

However, it's not possible to have several sets of tags on the same object. For example, it can be useful to separate skills and interests for users. acts_as_taggable_on implements this lacking functionality."*


## Examples

Wanna add a tag to your Users?

Once you have properly installed this gem (please read below for Setup instructions), you are ready to declare a model as taggable. In this example, we will add a tag to our User model:

```
class User <  ActiveRecord::Base
  		acts_as_taggable_on :tags
end
```

Then, add a line in user_helper.rb

```
include ActsAsTaggableOn::TagsHelper
```

Next, add a way for the user to add their own tag in the "add a user" form, in this case users/_new.html.erb

```
<%= f.label :tags %>
<%= f.text_field :tag_list %>
```


Now, let's add a way to see the tags in the user show file:


```
<% @user.tags.any? %>
   <% @user.tags.each do |tag| %>
   <%= link_to tag.name, tagged_url(:tag, tag.name) %>
<% end %>
```

Next, we need to add a "tagged" method to the users controller


```
def tagged
  if params[:tag].present? 
    @users = User.tagged_with(params[:tag])
  else 
    @users = User.all
  end  
end
```

Finally, we'll add a route for our Tagged action

```get 'tagged', to: 'posts#tagged', as: 'tagged'
```


## Setup?

Open your Gemfile in your Rails app and add the following (consult the gem github page for latest versions):

```gem 'acts-as-taggable-on', '~> 4.0'```


In your terminal, while in your Rails app, run:


```bundle```


Then


```rake acts_as_taggable_on_engine:install:migrations```


Don't forget to migrate!


```rake db:migrate```

Now you are ready to tag away!



## Resources

<li> [Github and Docs](https://github.com/mbleigh/acts-as-taggable-on)
<li> [ACTS AS TAGGABLE ON – A SHORT TUTORIAL, by Alex Muraro](https://alexmuraro.me/posts/acts-as-taggable-on-a-short-tutorial/)
<li> [Playing with acts as taggable on, by Bruno Michel](http://dev.af83.com/2008/02/25/playing-with-acts-as-taggable-on.html)
