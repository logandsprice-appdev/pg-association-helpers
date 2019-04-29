# Photogram Queries

In this project, we're going to practice querying our tables more; in particular, we want to practice leveraging the foreign key columns we added to build **associations** between tables.

## Standard Workflow

 1. From [your Cloud9 repositories list](https://c9.io/account/repos), set up a workspace [as usual](https://guides.firstdraft.com/starting-on-a-project-in-cloud9).
 1. Set up the project: `bin/setup`

## The domain model

Here's what our domain model looks like in this appliction:

![Domain Model](erd.png?raw=true "Domain Model")

I've already created these tables by running the following commands:


```bash
rails generate draft:model user username:string private:boolean likes_count:integer comments_count:integer
```

```bash
rails generate draft:model photo caption:text image:string owner_id:integer likes_count:integer comments_count:integer
```

```bash
rails generate draft:model follow_request sender_id:integer recipient_id:integer status:string
```

```bash
rails generate draft:model like fan_id:integer photo_id:integer
```

```bash
rails generate draft:model comment photo_id:integer body:text author_id:integer
```

The `bin/setup` script includes a line that `rails db:migrate`s, so the tables should be set up; if not, you can run `rails db:migrate` now to be sure.

## Play around in rails console

Pop open a `rails console` and verify that the models got set up correctly:

```ruby
User.count
Photo.count
FollowRequest.count
Like.count
Comment.count
```

As usual, we could create some data manually with `.new`, `.save`, etc; but, to save time, I've included a rake task for you that will add some dummy data to play around with. At a Terminal prompt, run:

```bash
rails dummy:reset
```

This will take a few minutes to create 40 users, some photos for each user, some followers, likes, comments, etc.


> Note that if for some reason later you want to reset the database again, you need to first destroy it:
>
> ```bash
> rails db:drop
> ```
>
> and then re-create and re-populate it:
>
> ```bash
> rails db:migrate
> rails dummy:reset
> ```

## Queries to write

Here are some questions to answer:

For the user `"Trina"`,

  - How many photos has the user posted?
  - How many photos has the user liked?
  - How many photos has the user commented on?
  - How many follow requests has the user sent?
     - How many of those were accepted?
  - How many follow requests has the user received?
     - How many of those were accepted?
  - How many photos are in the user's feed?
  - How many photos have the people the user is following liked?
