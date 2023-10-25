> Name :- Jha Rajesh Parasnath & Suhaib Malam <br> Class :- MSc SEM 1

<br>

# <center>*-: Blog Management System :-*</center>

<br>
<br>

## <center>Explanation</center>

<br>


## Controller

* `adminController.js` :Here's an explanation of each function:

securePassword(password):

This function is an asynchronous function that takes a password as an argument.
It uses the bcrypt library to hash the password with a salt factor of 10 for security.
The hashed password is then returned.

blogSetup(req, res):

This function is responsible for handling the initial setup of the blog.
It attempts to find any existing blog settings. If there are existing settings, it redirects the user to the login page. Otherwise, it renders a page for setting up the blog.

blogSetupSave(req, res):

This function is used to save the settings for the blog.
It retrieves data from the request, including the blog title, image, description, email, name, and password.
It securely hashes the password using the securePassword function.
It creates a new BlogSetting object with the blog's title, image, and description and saves it to the database.
It also creates a new User with the provided name, email, hashed password, and sets the user as an admin.
If both the blog settings and user data are saved successfully, it redirects the user to the login page; otherwise, it renders the blog setup page with an error message.

dashboard(req, res):

This function retrieves all posts from the database and renders a dashboard view, passing the posts to be displayed.
loadPostDashboard(req, res):

This function is responsible for rendering a view for managing posts.

addPost(req, res):

This function handles the addition of a new blog post.
It extracts post data from the request, such as title, content, and an optional image.
It creates a new Post object with the provided data and saves it to the database.
It sends a response indicating the success or failure of the operation.

uploadPostImage(req, res):

This function is used for uploading post images.
It constructs a path for the uploaded image and sends a response with a success message and the image path.

deletePost(req, res):

This function deletes a post based on the provided post ID.
It sends a response indicating whether the post was deleted successfully or not.

loadEditPost(req, res):

This function loads a view for editing a specific blog post.
It retrieves the post data based on the post ID and renders an edit view.

updatePost(req, res):

This function handles the updating of a blog post.
It takes the updated post data, including the title, content, and image.
It finds and updates the post in the database based on the provided post ID.
It sends a response indicating the success or failure of the update.

loadSettings(req, res):

This function loads the blog settings view.
It retrieves the current post limit setting, if available, and renders a view for modifying the setting.

saveSettings(req, res):

This function is responsible for saving the blog settings.
It updates the post limit setting in the database and sends a response indicating the success or failure of the update.
<br>

* `blogController.js` :
Certainly, here's an explanation of the JavaScript functions in the code you provided:

sendCommentMail(name, email, post_id):

This function is used to send an email notification to a user when someone replies to their comment.
It uses the Nodemailer library to set up an email transport configuration for Gmail (SMTP).
It constructs an email message with a link to the post where the user can read their replies.
Finally, it sends the email using the configured transporter.

loadBlog(req, res):

This function is responsible for loading the main blog page.
It retrieves the blog post limit setting from the database.
It fetches a limited number of blog posts from the database based on the post limit setting.
It renders the 'blog' view, passing the retrieved posts and post limit to be displayed.

loadPost(req, res):

This function loads an individual blog post.
It calculates and retrieves the counts of likes and dislikes for the post.
It fetches the content of the post based on the provided post ID.
It renders the 'post' view, passing the post content, likes, and dislikes to be displayed.

addComment(req, res):

This function is used to add a new comment to a blog post.
It extracts data from the request, including the post ID, username, email, and comment content.
It generates a new ObjectID for the comment.
It updates the corresponding blog post by pushing the new comment object to the "comments" array.
It sends a response indicating the success of the comment addition.

doReply(req, res):

This function is responsible for adding a reply to a comment on a blog post.
It generates a new ObjectID for the reply.
It updates the corresponding blog post's comment with the new reply, using the post ID and comment ID.
It also calls the sendCommentMail function to notify the original commenter about the reply via email.
It sends a response indicating the success of the reply addition.

getPosts(req, res):

This function is used to fetch a set of blog posts based on the start and limit parameters.
It queries the database to retrieve a range of posts, allowing for pagination.
It sends the retrieved posts as a response to the client.
<br>

* `userController.js` :

sendResetPasswordMail(name, email, token):

This function is used to send a password reset email to a user when they request a password reset.
It configures a nodemailer transport for sending email using Gmail's SMTP server.
It constructs an email message with a link to reset the password, using a token as a unique identifier.
It sends the email to the user's email address.

loadLogin(req, res):

This function is responsible for rendering the login page.
verifyLogin(req, res):

This function handles user login verification.
It retrieves the user's email and password from the request.
It checks if a user with the provided email exists.
If the user exists, it compares the provided password with the stored password using bcrypt.
If the password matches, it sets up a session and a user cookie and redirects the user to the appropriate page based on whether they are an admin or not. If the login fails, it renders the login page with an error message.

logout(req, res):

This function logs the user out.
It destroys the user's session and clears the user cookie.
It redirects the user to the login page.

forgetLoad(req, res):

This function renders the "forget password" page where users can request a password reset.

forgetPasswordVerify(req, res):

This function handles the password reset process.
It checks if the user's email exists in the database.
If the email exists, it generates a random token and associates it with the user in the database.
It then sends an email to the user with a link to reset the password.

resetPasswordLoad(req, res):

This function renders the "reset password" page, allowing users to reset their password after clicking a link from their email.
It checks if the provided token exists in the database.

resetPassword(req, res):

This function updates the user's password after a successful password reset.
It securely hashes the new password and updates the user's password in the database.
It clears the token associated with the user in the database.

loadRegister(req, res):

This function renders the user registration page.

register(req, res):

This function handles the user registration process.
It securely hashes the provided password using bcrypt.
It creates a new user object with the name, email, and hashed password.
It saves the user in the database and renders the registration completion message.
