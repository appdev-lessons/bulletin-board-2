# Bulletin Board 2

In this project, we're going to practice building sign in and sign out using a gem called Devise.

<div class="bg-red-100 py-1 px-5" markdown="1">
[Here is a walkthrough video for this lesson](https://share.descript.com/view/qpQZz1iDN8a). **Please note** the video does not include the conditional Delete link button. The `rake grade` spec for this is not worth any points, but if you do want to implement it, then read the notes below. Those notes are still a work in progress, so if you don't see the instructions yet, check back in the lesson in a few hours.
</div>

## Data model

[Our aim is to build an app like this.](https://bulletin-board-2.matchthetarget.com/)

Click around and notice what the differences are between our new target and the old one for bulletin-board-1:

- A non-signed in user can still browse boards and posts.
- A user has to sign in before they can create a board or a post.
- Boards know who their creator is and display it on the boards#index and boards#show pages.
- Posts know who their creator is and display it on the boards#show page.
- On the boards#show page, below the title of a post, there is a link to delete a post that appears for the creator (and only the creator) of a post.

## Setup 

Here is your target: [bulletin-board-2.matchthetarget.com](https://bulletin-board-2.matchthetarget.com/)

This project includes automated tests, so click on this button to get started:

LTI{Load Bulletin Board 2 assignment}(https://grades.firstdraft.com/launch)[S9ymPy6WCsn18gLbByVbZQ7k]{vfdtzJb5bLYqYwuqgeRKpc5d}(10)[Bulletin Board 2 Project]

Then, fork the repository and create your codespace.

The starter code is the solution to the bulletin-board-1 project. Study it and compare it to your own solution.

## Install Devise

```
rails generate devise:install
```

## Set sign out to GET

```
# config/initializers/devise.rb, Line 269

config.sign_out_via = :get
```

## Set a root route

```ruby
# config/routes.rb

root "boards#index"
```

## Generate user account

```
rails generate devise user
```

## Add foreign key columns

```
rails generate migration AddUserIdToBoards user_id:integer
```

```
rails generate migration AddUserIdToPosts user_id:integer
```

## Update sample data task

## Explore Devise-provided RCAVs

- `GET /users/sign_up`
- `GET /users/sign_in`
- `GET /users/sign_out`
- `GET /users/edit`

## Add conditional navigation

## Add hidden foreign key fields

## Conditionally allow deletes

---

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }
	
---
