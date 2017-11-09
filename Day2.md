# Reddit | Day 2

## Part 1: Individual Posts
Now that we can finally make & view all of our posts, the next step is to view a single post, comment on it, and view the comment thread. Let's get started! Here are the post routes that you need to implement:

- `/post`
    - `POST /delete`: Delete an existing post (given a `post_id`)
        - This should delete all comments that belong to post being deleted
    - `GET /[post_id]`: Respond with the thread of all posts associated with the entered `post_id`
        - response should include all parent & children posts of the given `post_id`
    - `GET /[user_id]`: Respond with all posts associated with a certain user (not including threads)

## Part 2: Vote Routes
Now let's create some `vote` routes. For these you will have to modify some routes from the last few parts. Each vote entry is either an upvote or a downvote, and **must** belong to to a user. A post has many votes.

- `/post`
    - `GET /[post_id]/upvote`: Create an upvote entry in the `votes` table for the given `post_id` by the currently logged in user
        - **IF** upvote by current user already exists, then delete the vote entry
    - `GET /[post_id]/downvote`: Create an downvote entry in the `votes` table for the given `post_id` by the currently logged in user
        - **IF** downvote by current user already exists, then delete the vote entry
- modify the following routes to:
    - `GET /post/[post_id]`: Include all votes associated with every post within the comment thread in the response
    - `GET /post/[user_id]`: Include all votes associated with all posts returned for this user

## Part 3: Subreddits
You've successfully made *most* of reddit. Now come the subreddits!

## C'est Fini!
Congratulations! You've learned & understood SQL (hopefully), and made an awesome clone of Reddit.
