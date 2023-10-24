> Name :- Jha Rajesh Parasnath & Suhaib Malam <br> Class :- MSc SEM 1

<br>

# <center>*-: Blog Management System :-*</center>

<br>
<br>

## <center>Explanation</center>

<br>

## Config

* `config.js` : Let's break down what each of these variables is for:

sessionSecret:

This variable is assigned the string "blogsessionuserssecret".
It seems to be intended for use as a session secret in a web application. Session secrets are typically used to encrypt and sign user sessions, enhancing security. It's important to keep session secrets secret, as they are a critical part of session management.
emailUser:

This variable is assigned an empty string "".
It appears to be meant for storing an email username or email account name. However, it's empty, so there's no actual email address or username specified here.
emailPassword:

This variable is also assigned an empty string "".
It seems to be intended for storing an email account password. Just like the emailUser variable, it's empty, which means there's no actual email account password provided in this code.
The module then exports these three variables (sessionSecret, emailUser, and emailPassword) so that they can be used in other parts of the application. The values for emailUser and emailPassword should be filled in with valid credentials for your specific email service if this code is part of a larger project that sends emails. Additionally, the sessionSecret should be kept secret and unique for the security of your application.

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
## Middlewares

* `adminLoginAuth.js` :  code defines two middleware functions, isLogin and isLogout, typically used in the context of user authentication and routing in a web application. Here's an explanation of each of these functions:

isLogin(req, res, next):
This middleware function checks if a user is logged in and has administrative privileges (is an admin).
It's intended to protect routes that should only be accessible to logged-in administrators.
If the user is logged in and is an admin (as indicated by the session variables req.session.user_id and req.session.is_admin), it allows the request to proceed by calling the next function, which passes control to the next middleware or route handler.
If the user is not logged in or is not an admin, it redirects them to the login page (/login) to authenticate themselves.
isLogout(req, res, next):
This middleware function checks if a user is logged in as an admin and redirects them to the dashboard if they are already logged in.
It's typically used to protect routes that are meant for users who are not logged in, such as registration or login pages.
If the user is logged in as an admin (as indicated by the session variables req.session.user_id and req.session.is_admin), it redirects them to the dashboard page (/dashboard) to prevent them from accessing the login or registration pages.
If the user is not logged in or is not an admin, it allows the request to proceed by calling the next function, enabling them to access the requested route.
<br>

* `isBlog.js` :  Here's an explanation of the isBlog middleware:

isBlog(req, res, next):
This middleware function checks if the blog application has been set up. It does so by querying the BlogSetting model in the database to see if any settings exist.
If no blog settings are found in the database (i.e., blogSetting.length == 0), and the user is not attempting to access the /blog-setup route (as indicated by req.originalUrl), the middleware redirects the user to the blog setup page (/blog-setup). This ensures that users are redirected to set up the blog when it has not been configured.
If blog settings are found in the database or if the user is already on the /blog-setup route, the middleware allows the request to proceed by calling the next function. This allows the user to access the requested route.
The isBlog middleware is used to enforce that the blog setup must be completed before users can access other parts of the blog application. If the blog has not been set up, the middleware automatically redirects users to the blog setup page, ensuring that the blog's configuration is in place before users can access and interact with the blog.







* `userAuth.js` : The provided code defines two middleware functions, isLogin and isLogout, which are typically used in the context of user authentication and routing in a web application. However, there are some differences compared to the previously explained isLogin and isLogout functions. Here's an explanation of each of these functions:

isLogin(req, res, next):

This middleware function checks if a user is logged in and is not an administrator.
It's intended to protect routes that should only be accessible to logged-in non-administrative users.
If the user is logged in and is not an admin (as indicated by the session variables req.session.user_id and req.session.is_admin), it allows the request to proceed by calling the next function, which passes control to the next middleware or route handler.
If the user is not logged in or is an admin, it redirects them to the login page (/login) to authenticate themselves.
isLogout(req, res, next):

This middleware function checks if a user is not logged in as an admin and redirects them to the home page if they are already logged out.
It's typically used to protect routes that are meant for logged-out users or non-administrative users.
If the user is not logged in as an admin (as indicated by the session variables req.session.user_id and req.session.is_admin), it redirects them to the home page (/) to prevent them from accessing certain routes.
If the user is logged in as an admin, it allows the request to proceed by calling the next function, enabling them to access the requested route.
These middleware functions help ensure that users are appropriately authenticated and authorized to access certain routes based on whether they are administrators or regular users. isLogin is used to protect routes that non-admin users should access, and isLogout is used to protect routes intended for non-logged-in users. These functions help control the flow of user requests and enhance security in your web application.
<br>

* `BinModel.js` :  Let's break down the code step by step:

Importing Mongoose:

You import the Mongoose library at the beginning of the code. Mongoose is an ODM (Object-Document Mapping) library for MongoDB, which allows you to define data models and interact with MongoDB databases using JavaScript.
Defining a Schema:

The binSchema variable is created as a Mongoose schema using mongoose.Schema({}). A schema defines the structure of documents within a collection. In this case, you have defined a schema with two fields:
model_name: A field of type String.
data: A field of type String.
Exporting the Model:

You export a Mongoose model using mongoose.model('Bin', binSchema). This line defines a model named 'Bin' based on the 'binSchema' schema.
'Bin': The first argument is the name of the model. This name will be used to interact with the 'Bin' collection in the database.
'binSchema': The second argument is the schema that defines the structure of the documents in the 'Bin' collection.
With this code, you have created a Mongoose model for a 'Bin' collection with the specified schema. This model can now be used to perform CRUD (Create, Read, Update, Delete) operations on documents in the 'Bin' collection in your MongoDB database.

<br>

* `blogSettingModel.js` : 'BlogSetting' in a MongoDB database. Here's an explanation of the code:

Importing Mongoose:

The code begins by importing the Mongoose library using require("mongoose"). Mongoose is an ODM (Object-Document Mapping) library for MongoDB, allowing you to define data models and interact with MongoDB databases using JavaScript.
Defining a Schema:

The blogSettingSchema variable is created as a Mongoose schema using mongoose.Schema({}). A schema defines the structure of documents within a collection. In this case, you have defined a schema with three fields:
blog_title: A field of type String, which is marked as required (the document must have this field).
blog_logo: A field of type String, also marked as required.
description: A field of type String, and it's required as well.
Exporting the Model:

The Mongoose model is exported using mongoose.model('BlogSetting', blogSettingSchema). This line defines a model named 'BlogSetting' based on the 'blogSettingSchema' schema.
'BlogSetting': The first argument is the name of the model. This name will be used to interact with the 'BlogSetting' collection in the database.
'blogSettingSchema': The second argument is the schema that defines the structure of the documents in the 'BlogSetting' collection.

<br>

* `likeModel.js` : Importing Mongoose:

The code begins by importing the Mongoose library using require("mongoose"). Mongoose is an ODM (Object-Document Mapping) library for MongoDB, allowing you to define data models and interact with MongoDB databases using JavaScript.
Defining a Schema:

The likeSchema variable is created as a Mongoose schema using mongoose.Schema({}). A schema defines the structure of documents within a collection. In this case, you have defined a schema with three fields:
post_id: A field of type mongoose.Schema.Types.ObjectId. This field is set to reference the 'Post' model, which means that it stores the ID of a related post document. It represents the post that the user has liked or disliked.
user_id: A field of type mongoose.Schema.Types.ObjectId. This field is set to reference the 'User' model, which means that it stores the ID of a related user document. It represents the user who has performed the like or dislike action.
type: A field of type Number, marked as required. This field represents the type of the like action. It is often used to distinguish between likes and dislikes, typically using values like 1 for a like and 0 for a dislike.
Exporting the Model:

The Mongoose model is exported using mongoose.model('Like', likeSchema). This line defines a model named 'Like' based on the 'likeSchema' schema.
'Like': The first argument is the name of the model. This name will be used to interact with the 'Like' collection in the database.
'likeSchema': The second argument is the schema that defines the structure of the documents in the 'Like' collection.
</br>

* `postModel.js` :
Here's an explanation of the code:

Importing Mongoose:

The code begins by importing the Mongoose library using require('mongoose'). Mongoose is an ODM (Object-Document Mapping) library for MongoDB, allowing you to define data models and interact with MongoDB databases using JavaScript.
Defining a Schema:

The postSchema variable is created as a Mongoose schema using mongoose.Schema({}). A schema defines the structure of documents within a collection. In this case, you have defined a schema with several fields:
title: A field of type String, marked as required. This field represents the title of the post and must be present in each document.
content: A field of type String, also marked as required. This field represents the content of the post and is required in each document.
image: A field of type String, with a default value of an empty string (''). This field represents an optional image associated with the post.
views: A field of type Number, with a default value of 0. This field represents the number of views the post has received.
comments: A field of type Object, with a default value of an empty object. This field is intended to store comments related to the post.
Exporting the Model:

The Mongoose model is exported using mongoose.model('Post', postSchema). This line defines a model named 'Post' based on the 'postSchema' schema.
'Post': The first argument is the name of the model. This name will be used to interact with the 'Post' collection in the database.
'postSchema': The second argument is the schema that defines the structure of the documents in the 'Post' collection.
With this code, you have created a Mongoose model for a 'Post' collection with the specified schema. This model can be used to perform CRUD (Create, Read, Update, Delete) operations on documents in the 'Post' collection in your MongoDB database. It represents the data structure of a blog post, including its title, content, optional image, view count, and associated comments.
</br>

* `settingModel.js` :
Here's an explanation of the code:

Importing Mongoose:

The code begins by importing the Mongoose library using require('mongoose'). Mongoose is an ODM (Object-Document Mapping) library for MongoDB, allowing you to define data models and interact with MongoDB databases using JavaScript.
Defining a Schema:

The settingSchema variable is created as a Mongoose schema using mongoose.Schema({}). A schema defines the structure of documents within a collection. In this case, you have defined a schema with one field:
post_limit: A field of type Number, marked as required. This field represents the post limit setting, which typically controls the number of posts that can be displayed or retrieved.
Exporting the Model:

The Mongoose model is exported using mongoose.model('Setting', settingSchema). This line defines a model named 'Setting' based on the 'settingSchema' schema.
'Setting': The first argument is the name of the model. This name will be used to interact with the 'Setting' collection in the database.
'settingSchema': The second argument is the schema that defines the structure of the documents in the 'Setting' collection.
</br>

* `userModel.js` :
Here's an explanation of the code:

Importing Mongoose:

The code begins by importing the Mongoose library using require('mongoose'). Mongoose is an ODM (Object-Document Mapping) library for MongoDB, allowing you to define data models and interact with MongoDB databases using JavaScript.
Defining a Schema:

The userSchema variable is created as a Mongoose schema using mongoose.Schema({}). A schema defines the structure of documents within a collection. In this case, you have defined a schema with several fields:
name: A field of type String, marked as required. This field represents the user's name and must be present in each document.
email: A field of type String, marked as required. This field represents the user's email address and is required in each document.
password: A field of type String, marked as required. This field represents the user's password and must be present in each document.
is_admin: A field of type String, not required (marked as required: false). This field is intended to indicate whether the user has administrator privileges. It has a default value of 0, indicating a non-admin user.
token: A field of type String, with a default value of an empty string (''). This field is typically used for user authentication and authorization, and it starts empty by default.
Exporting the Model:

The Mongoose model is exported using mongoose.model('User', userSchema). This line defines a model named 'User' based on the 'userSchema' schema.
'User': The first argument is the name of the model. This name will be used to interact with the 'User' collection in the database.
'userSchema': The second argument is the schema that defines the structure of the documents in the 'User' collection.
</br>


## Routes

* `adminRoute.js` : Here's an explanation of the code:

Importing Dependencies:

The code begins by importing various dependencies and middleware using require. Notable dependencies include:
express: The core Express.js framework for building web applications.
body-parser: Middleware for parsing incoming request data.
express-session: Middleware for managing user sessions.
multer: Middleware for handling file uploads.
path: A built-in Node.js module for working with file and directory paths.
Configuring Middleware:

Several middleware configurations are set up for the admin_route Express application.
body-parser is used to parse JSON and URL-encoded data from incoming requests.
express-session is used to manage user sessions and is configured with a secret key and session options.
The view engine is set to 'ejs', indicating that the application will use the EJS templating engine for rendering views.
The views directory is set to './views', specifying the location of view templates.
The application serves static files from the 'public' directory using express.static('public').
Multer Configuration:

A configuration for handling file uploads is set up using Multer. It defines the storage destination and file naming.
Uploaded files will be stored in the 'public/images' directory.
The filenames are generated with a timestamp and the original filename to ensure uniqueness.
Importing Controllers and Middlewares:

The code imports controller functions and custom middlewares from the respective files. These functions and middlewares will be used to handle specific routes and actions.
Defining Routes:

The code defines several routes with corresponding HTTP methods and middleware functions.
/blog-setup: GET and POST routes for setting up the blog.
/dashboard: GET route for the admin dashboard.
/create-post: GET and POST routes for creating a new post.
/upload-post-image: POST route for uploading post images.
/delete-post: POST route for deleting a post.
/edit-post/:id: GET route for editing a specific post.
/update-post: POST route for updating a post.
/settings: GET and POST routes for managing application settings.
Exporting the Admin Route:

The admin_route Express application is exported to be used in other parts of the application.

<br>

* `blogRoute.js` :Here's an explanation of the code:

Importing Express and Dependencies:

The code begins by importing the Express.js framework and other dependencies.
View Engine and Static File Configuration:

The view engine is set to 'ejs', indicating that the application will use the EJS templating engine for rendering views.
The views directory is set to './views', specifying the location of view templates.
The application serves static files from the 'public' directory using express.static('public'). This allows the application to serve static assets such as CSS, JavaScript, and images from the 'public' directory.
Importing the Blog Controller:

The code imports controller functions from the 'blogController' file. These functions handle the logic for rendering blog content and managing comments and replies.
Defining Routes:

The code defines several routes with corresponding HTTP methods and controller functions:
/: A GET route that renders the main blog page. It invokes the loadBlog function from the 'blogController' when accessed.
/post/:id: A GET route that displays a specific blog post. It invokes the loadPost function from the 'blogController' and expects a post ID as a URL parameter.
/add-comment: A POST route used to add comments to a blog post. It invokes the addComment function from the 'blogController'.
/do-reply: A POST route for adding replies to comments. It invokes the doReply function from the 'blogController'.
/get-posts/:start/:limit: A GET route used to retrieve a range of blog posts. It invokes the getPosts function from the 'blogController' and expects 'start' and 'limit' parameters in the URL to specify the range of posts to retrieve.
Exporting the Blog Route:

The blog_route Express application is exported to be used in other parts of the application.
<br>

* `userRoute.js` : Here's an explanation of the code:

Importing Express and Dependencies:

The code begins by importing the Express.js framework and various dependencies, including:
body-parser: Middleware for parsing JSON and URL-encoded data from incoming requests.
cookie-parser: Middleware for parsing cookies from the request.
express-session: Middleware for managing user sessions.
config: A custom configuration file (presumably containing secrets and settings).
Middleware Configuration:

Several middleware configurations are set up for the user_route Express application.
body-parser is used to parse JSON and URL-encoded data from incoming requests.
cookie-parser is used to parse cookies from the request.
express-session is used to manage user sessions and is configured with a secret key and session options.
The view engine is set to 'ejs', indicating that the application will use the EJS templating engine for rendering views.
The views directory is set to './views', specifying the location of view templates.
The application serves static files from the 'public' directory using express.static('public').
Importing Controllers and Middlewares:

The code imports controller functions (userController) and custom middlewares (adminLoginAuth and userAuth) from their respective files. These functions and middlewares handle user-related actions and authentication.
Defining Routes:

The code defines several routes with corresponding HTTP methods and middleware functions:
/login: GET and POST routes for user login. The loadLogin function displays the login form, and the verifyLogin function handles user authentication.
/register: GET and POST routes for user registration. The loadRegister function displays the registration form, and the register function handles user registration.
/logout: GET route for user logout. The logout function is used to log the user out.
/user-logout: GET route for user logout with different authentication middleware (userAuth).
/forget-password: GET route for initiating the password reset process. The forgetLoad function displays the "forgot password" page.
/forget-password: POST route for verifying the user's email address and initiating the password reset process. The forgetPasswordVerify function handles this action.
/reset-password: GET route for entering a new password. The resetPasswordLoad function displays the "reset password" page.
/reset-password: POST route for setting a new password. The resetPassword function handles this action.
Exporting the User Route:

The user_route Express application is exported to be used in other parts of the application.
<br>

* `index.js` : It uses the Express.js framework for creating routes, MongoDB as the database, and Socket.io for real-time communication. Here's an explanation of the code:

Database Connection:

The code uses Mongoose to connect to a MongoDB database hosted on MongoDB Atlas. The connection string specifies the database server, username, and password.
Server Setup:

An Express.js application is created using express().
An HTTP server is created using the http module, and the Express application is passed to it.
The Server class from the Socket.io library is used to set up a WebSocket server (io) on top of the HTTP server. This enables real-time communication between clients and the server.
Middleware:

The custom isBlog middleware is used as application-level middleware to check whether the application is in "blog" mode. If not, it redirects to the "/blog-setup" route. This middleware seems to be used to ensure that the blog is properly configured before allowing access to other routes.
Routing:

The code sets up routes for different parts of the application using Express routers:
adminRoute: Handles routes related to the admin section.
userRoute: Handles routes related to user actions like login, registration, and password reset.
blogRoute: Handles routes related to the blog content, including viewing posts and comments.
Socket.io Events:

The code sets up Socket.io event handlers to handle real-time communication between clients and the server. Events include:
"new_post": Broadcasts new post data to all connected clients.
"new_comment": Broadcasts new comment data to all connected clients.
"new_reply": Broadcasts new reply data to all connected clients.
"delete_post": Informs clients about the deletion of a post.
"increment_page_view": Increments the view count for a post and informs clients about the updated count.
"like" and "dislike": Handle like/dislike actions and update the counts.
Server Listening:

The server listens on port 3000 using the http.listen() method. When the server is running, it outputs "Server is running" to the console.
<br>
