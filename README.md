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

Here are some questions to answer. Give it a shot in `rails console`:

For the user `"Trina"`,

  - How many photos has the user posted?
  - How many photos has the user liked?
  - How many comments has the user made?
     - How many photos has the user commented on? Is this the same as the number of comments the user has made? Hint: there's a method called `.distinct` that you can call on a collection to remove duplicates.
  - How many follow requests has the user sent?
     - How many of those were accepted? (I.e. how many people is the user following?)
  - How many follow requests has the user received?
     - How many of those were accepted? (I.e. how many followers does the user have?)
  - What are the usernames of all of the people the user is following?
  - How many photos are in the user's feed (photos posted by the people the user is following)?
  - How many photos have the people the user is following liked?

Once you've answered the questions for `"Trina"` in `rails console`, try defining instance methods in `app/models/user.rb` that will make it easy to answer these question for any user.

require "rails_helper"

describe Photo, "#poster" do
  it "returns the user who posted the photo" do

  end
end


describe Photo, "#comments" do
  it "returns the comments made on the photo" do

  end
end

describe Comment, "#commenter" do
  it "returns the user who authored the comment" do

  end
end

describe Photo, "#likes" do
  it "returns the likes made on the photo" do

  end
end

describe Photo, "#fans" do
  it "returns the users that have liked the photo" do

  end
end

describe Photo, "#fan_list" do
  it "returns the usernames of the users that have liked the photo as a sentence" do

  end
end

describe User, "#comments" do
  it "returns the comments the user has made" do

  end
end

describe User, "#own_photos" do
  it "returns the photos posted by the user", points: 2 do

  end
end

describe User, "#liked_photos" do
  it "returns the photos the user has liked" do

  end
end

describe User, "#commented_photos" do
  context "when the user made only one comment per photo" do
    it "returns the photos the user has commented on" do

    end
  end
end

describe User, "#commented_photos" do
  context "when the user made more than one comment per photo" do
    it "returns the photos the user has commented on" do

    end
  end
end

describe User, "#sent_follow_requests" do
  it "returns all of the follow requests that were sent by the user" do

  end
end

describe User, "#received_follow_requests" do
  it "returns all of the follow requests that were received by the user" do

  end
end

describe User, "#accepted_sent_follow_requests" do
  it "returns the follow requests that were sent by the user and accepted" do

  end
end

describe User, "#accepted_received_follow_requests" do
  it "returns the follow requests that were received by the user and accepted" do

  end
end

describe User, "#followers" do
  it "returns the people whose follow requests the user has accepted" do

  end
end

describe User, "#following" do
  it "returns the people that have accepted the user's follow requests" do

  end
end

describe User, "#feed" do
  it "returns the photos posted by the people the user is following" do

  end
end

describe User, "#discover" do
  it "returns the photos that are liked by the people the user is following" do

  end
end
