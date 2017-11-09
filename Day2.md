# Reddit | Day 2

## Part 1: Individual Posts
Now that we can finally make & view all of our posts, the next step is to view a single post, comment on it, and view the comment thread. Let's get started!

## Part 6: Post Routes
We will need to also implement the following routes for Reddit posts (create/delete/get all/etc).

- `/post`
    - `POST /new`: Create a new post
        - all posts should have a title, but the body and link are optional
   	    - each post should be attached to a single user
   	    - posts should have a parent attribute, and posts with a parent are called comments (this will allow users to reply to comments)
    - `POST /delete`: Delete an existing post (given a `post_id`)
    - `GET /all`: Respond with all posts
    - `GET /[post_id]`: Respond with the thread of all posts associated with the entered `post_id`
        - response should include all parent & children posts of the given `post_id`
    - `GET /[user_id]`: Respond with all posts associated with a certain user

## Part 7: Vote Routes
Now let's create some `vote` routes. For these you will have to modify some routes from the last few parts. Each vote entry is either an upvote or a downvote, and **must** be attached to a user and a post.

- `/post`
    - `GET /[post_id]/upvote`: Create an upvote entry in the `votes` table for the given `post_id` by the currently logged in user
        - **IF** upvote by current user already exists, then delete the vote entry
    - `GET /[post_id]/downvote`: Create an downvote entry in the `votes` table for the given `post_id` by the currently logged in user
        - **IF** downvote by current user already exists, then delete the vote entry
- modify the following routes:
    - `GET /post/[post_id]`: Include all votes associated with every post within the comment thread in the response
    - `GET /post/[user_id]`: Include all votes associated with all posts returned for this user

## Part 8: Connect FrontPage
Now that we have have a frontend and a backend, all that's left is to connect the two!

1. Run `npm install --save axios`
1. In your `Modal` component write the following two functions
    - `onLogin()`: This function is called upon clicking the login button
        - use `refs` to retrieve information from the login form input boxes
        - use `axios` perform a `POST` request to `/api/user/login`
        - upon successful login reroute the user to the `/` route (back to the FrontPage)
    - `onRegister()`: This function is called upon clicking the register button
        - use `refs` to retrieve information from the register form input boxes
        - use `axios` perform a `POST` request to `/api/user/register`
        - upon successful login reroute the user to the `/` route (back to the FrontPage)
1. Modify your `SideBar` component to perform a `GET /api/user` request on `componentDidMount` (this will tell you whether or not the user is logged in)
    - If the user is logged in you should hide the `Login` and `Register` buttons, and replace them with the `username`
    - If the user isn't logged in you should display the `Login` and `Register` buttons
1. Implement an `onclick` function for the `SubmitPost` button. The function should first check if the user is logged in by performing a `GET /api/user` request.
    - If the user is logged in you should redirect them to `/post/new`
    - If the user is not logged in you should fire a `TOGGLE_LOGIN_MODAL` action (to prompt the user to log in/register)

## Part 9: New Post
In this section you will set up functionality to create new posts

1. Create a `NewPost` component, and add it to your Router on path `/post/new`
1. This component should contain:
    - `<input type="text">`: For the title of the post **[REQUIRED]**
    - `<textarea>`: For the content of the post
    - `<input type="text">`: For the link
    - `<input type="submit">`: For the submit button
1. On clicking the submit button you should retrieve the inputted information (via `refs`) and carry out a `POST` request to `/api/post/new`
1. Once posted you should redirect users back to the `/` route (FrontPage)

## Subreddits
You've successfully made *most* of reddit. Now come the subreddits!

## C'est Fini!
Congratulations! You've learned & understood SQL (hopefully), and made an awesome clone of Reddit.
