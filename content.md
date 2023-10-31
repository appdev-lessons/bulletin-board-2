# Bulletin Board 2

In this project, we're going to practice building sign in and sign out using a gem called Devise.

<div class="bg-red-100 py-1 px-5" markdown="1">
[Here is a walkthrough video for this lesson](https://share.descript.com/view/qpQZz1iDN8a). **Please note** the video does not include the conditional Delete link button. The `rake grade` spec for this is not worth any points, but if you do want to implement it, then give it a try!

You are also welcome to visit the [git commits I made throughout the video](https://github.com/raghubetina/bulletin-board-2/commits/main) to view the code on GitHub.
</div>

## Data model

[Our aim is to build an app like this.](https://bulletin-board-2.matchthetarget.com/)

Click around and notice what the differences are between our new target and the old one for `bulletin-board-1` ([bulletin-board-1.matchthetarget.com](https://bulletin-board-1.matchthetarget.com/)):

- A non-signed in user can still browse boards and posts.
- A user has to sign in before they can create a board or a post.
- Boards know who their creator is and display it on the `boards#index` and `boards#show` pages.
- Posts know who their creator is and display it on the `boards#show` page.
- On the `boards#show` page, below the title of a post, there is a link to delete a post that appears for the creator (and only the creator) of a post.

## Setup 

Here is your target: 

[bulletin-board-2.matchthetarget.com](https://bulletin-board-2.matchthetarget.com/)

This project includes automated tests, so click on this button to get started:

LTI{Load Bulletin Board 2 assignment}(https://grades.firstdraft.com/launch)[S9ymPy6WCsn18gLbByVbZQ7k]{vfdtzJb5bLYqYwuqgeRKpc5d}(10)[Bulletin Board 2 Project]

Then, fork the repository and create your codespace.

The starter code is the solution to the `bulletin-board-1` project. Study it and compare it to your own solution.

Once you feel comfortable, watch the [walkthrough video](https://share.descript.com/view/qpQZz1iDN8a), pause it frequently, and type along to complete the assignment at get the `rake grade` specs to pass. The notes below are all contained in the video.

## Setting up Devise

### Install

```
rails generate devise:install
```

### Set sign out to GET

Since we haven't learned how to implement DELETE routes in Rails yet, we need to change part of the configuration in the `config/initializers/devise.rb` file from `:delete` to `:get`:

```ruby
# config/initializers/devise.rb, Line 269

config.sign_out_via = :get
```

### Set a root route

Devise also want use to define our root route with a specific syntax, so do that:

```ruby
# config/routes.rb

root "boards#index"
```

### Generate user account

Once we've set everything up, we can use our new generator supplied by the gem to create the `User` model and routes. Run this at the bash prompt:

```
rails generate devise user
```

And, as usual, `rake db:migrate` afterwards.

## Explore Devise-provided RCAVs

Once you restart your application server, you should find four new routes defined:

- `GET /users/sign_up`
- `GET /users/sign_in`
- `GET /users/sign_out`
- `GET /users/edit`

You can add those routes as links in your `app/views/layouts/application.html.erb` file for easy access. However:

## Add conditional navigation: `current_user`

You should add these navigation links with a conditional so not all four links are always shown. You can do that with the Devise-provided helper method: `current_user`. 

See the walkthrough video for that step.

## Add foreign key columns

Now that we have our users setup, we need to associate boards and posts with owners. That means we'll need to modify our database tables to add a new foreign key column. 

We can do that by running these two **migrations**, checking the content of the migration files, and then running `rake db:migrate`:

```
rails generate migration AddUserIdToBoards user_id:integer
```

and

```
rails generate migration AddUserIdToPosts user_id:integer
```

See the walkthrough video for those steps.

## Add foreign keys in controller actions

Now that you have foreign key columns in the database tables, you need to visit any controller actions and make sure that the `current_user.id` is passed to any actions that need it (e.g. `boards#create`).

See the walkthrough video for that step.

## Update sample data task

Now that we are requiring a `user_id` in our boards and posts, we need to open the `lib/tasks/dev.rake` file where our `sample_data` task lives and update it to include the foreign key when creating our sample data.

See the walkthrough video for that step.

## Customize the UI

Now that we have everything setup with user sign in and foreign keys in our models, it is time to customize the user interface to match the target!

See the walkthrough video for those steps.

## Conditionally allow delete

In the target, you will notice a "Delete post" link to the delete action for a Post, _if and only if_ the signed in user is the owner of that post.

Can you implement this on your own?

You have all the tools you need:

- `current_user` if the user is signed in
- `post.user_id` with the user ID associated with a post
- the `posts#destroy` RCAV, written for you by the `draft:resource` generator in the previous `bulletin-board-1` project

So all you need to do is conditionally show a "Delete post" link! Revisit e.g. Must See Movies for a look at one of your previous delete links if you need.

Give it a shot!

## Our Devise guide

We prepared a manual with the steps to setup Devise in your project. It includes the steps in this project, and some additional things that you can do, such as editing Devise view templates. That is very important if your `User` model has attributes that you want to edit besides the email and password. [Here is that manual, which should serve as your go-to guide on user accounts with Devise.](https://learn.firstdraft.com/lessons/238-authentication-with-devise-basics). You may want to skip right to the [section on customizing views and forms.](https://learn.firstdraft.com/lessons/238-authentication-with-devise-basics#customizing-devise-views)

---

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }
	
---
