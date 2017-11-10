# Reddit | Day 2
This day will be less guided thus giving you more freedom in how you implement your queries.

## Part 1: Individual Posts
Now that we can finally make & view all of our posts, the next step is to view a single post, comment on it, and view the comment thread. Let's get started!

1. Navigate to `/backend/routes.js` and add a `GET /api/post/:id` route that responds with all post information corresponding to the given `postId`
1. Make sure that your list of posts on the Front Page are all links. They should link to `/post/:postId`.
1. Create a `PostPage` component that displays an overview of a single post
    - Given the `postId` param perform a `GET /api/post/:postId` request to retrieve information for the current post
1. On the `PostPage` component create a **comment** button that dispatches a `TOGGLE_COMMENT_MODAL` action along with the `postId`
    - Create a Modal with a textarea and a submit button
    - On submit you should perform a `POST /api/post/new` request (don't forget to include the `postId` for the post you are commenting on)
1. Modify your `GET /api/post/:id` route to respond with **ALL** children associated with the entered `postId`
    - **This is the one of the most challenging parts of the assignment, so be sure to think your strategy through thoroughly**
    - This request should recursively fetch all children of this post (this includes subchildren, subsubchildren, ...)
1. After the last step your `PostPage` component should receive the entire comment thread associated with the current post, so the next step is to iterate through this list and display the thread in a hierarchical manner
    - Each comment/post should have a **comment** button that dispatches that comment's `postId` (this allows us to comment on comments)
1. For each post/comment add a **delete** button that performs a `POST /api/post/delete/:id` request
1. Navigate to your `routes.js` file and create a `/post/delete/:id` route that deletes the comment with the given `postId` from your database **IF** the currently logged in user is the poster of that comment
    - Ensure that the `userId` foreign key on the post matches the user id of the currently logged in user
    - This route should also delete all subcomments associated with this comment

#### Goal
Make sure that the following set of steps are functional:

1. Navigate to the Front Page
1. Create a new post
1. View & click on the post on the Front Page
1. Comment on the post
1. Comment on the comment you just created
1. Comment on the comment you just created (you should now be three levels in)
1. View the comment hierarchy
1. Delete your first comment and watch all child comments disappear

## Part 2: Votes
Now let's create some `vote` routes. For these you will have to modify some routes from the last few parts. Each vote entry is either an upvote or a downvote, and **must** belong to to a user. A post has many votes.

1. Visit both the `PostPage` and the Front Page and create two buttons (upvote & downvote) beside **each** post/comment
    - On click they should each perform a `GET` request to either of the below routes (depending on which button was pressed)
        - `/api/post/:id/upvote`
        - `/api/post/:id/downvote`
1. Create a `/api/post/:id/upvote` route that inserts a new upvote into your votes table with foreign keys `postId` and `userId`
    - **IF** an upvote entry already exists in your table for that user & that post, then delete it
    - **IF** a downvote entry already exists in your table for that user & that post, then delete it and create an upvote entry
1. Create a `/api/post/:id/downvote` route that inserts a new downvote into your votes table with foreign keys `postId` and `userId`
    - **IF** a downvote entry already exists in your table for that user & that post, then delete it
    - **IF** an upvote entry already exists in your table for that user & that post, then delete it and create a downvote entry
1. Modify the `GET /post/:id` to include all votes associated with every post within the comment thread in the response
1. In the `AppContainer` (your Front Page) you should modify the query where you get all posts to account for the upvote and downvote data that you will now receive, as you need to:
    - Display the `# of upvotes - # of downvotes` as a number beside the upvote/downvote buttons
1. In the `PostPage` component you should modify the query where you get all posts to account for the upvote and downvote data that you will now receive, as you need to:
    - Display the `# of upvotes - # of downvotes` as a number beside the upvote/downvote buttons
1. **(Bonus)**: Make the `upvote` OR `downvote` buttons selected if a user has voted on a certain post

## Part 3: Subreddits [BONUS]
You've successfully made *most* of reddit. Now come the subreddits! Modify your application to add the following features:
- Add subreddits to your schema
- Allow users to create & own subreddits
- Allow users to delete subreddits (only the ones they own)
- Modify post creation functionality to ensure that each post belongs to a subreddit
- Allow users to subscribe to subreddits
- **ONLY** display posts from subscribed subreddits on frontpage

## C'est Fini!
Congratulations! You've learned & understood SQL (hopefully), and made an awesome clone of Reddit.
