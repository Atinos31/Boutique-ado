The first thing that we need to do is to set up a new gitpod workspace.
To do that I'm going to use the gitpod full template from the code institute github by clicking use this template.
I'll call my repository boutique_ado which is going to be the name of our e-commerce store.
Now that the repository has been created I can click the green gitpod button to create the workspace in gitpod.
Once the workspace is ready the first thing to do is install Django and create a new Django project.
To install it we can use " pip3 install django".
And then we'll use "django-admin startproject boutique_ado ."
To create the project in the current directory.
And you'll see now that we have our Django project folder
along with its settings.py, urls.py, and a couple of other files here in the file explorer.
Before we go any further I'm gonna create a basic gitignore file by typing touch .gitignore
And inside this file I'll add the basics.
We want star dot sqlite3 to ignore our development database file.
And star dot pyc and __pycache__
To ignore compiled python code which we don't need in version control.
With that finished let's run the project and make sure all is well by typing "python3 manage.py runserver"
And exposing port 8000.
Looks like all as well.
So let's stop the server now.
And run the initial migrations by typing "python3 manage.py migrate".
And finally, I'll create a superuser so that we can log into the admin.
Using pytUon3 manage.py createsuperuser
Give myself a username
And an email address.
And a password.
Since you've done this a few times now
you're probably starting to see why django is called the web framework for perfectionist with deadlines.
In under 5 minutes, we've got a brand new project up and running and we're ready to start building
So the last thing I'll do is the initial commit to github.
Since we created this project from the code institute gitpod template
there's no need to initialize a git repository.
If you type git status you'll see that we've already got one and it's actually already tracking our changes.
And if you look at git remote -v you'll see that everything is already linked up to our repo on github.
To push the changes we've made to github all we need to do is git add . to add all the files.
git commit - m 'initial commit'
To give it a commit message.
And then git push, to push them to the repo.
In the next video, we'll use a popular Django package called django-allauth
to quickly set up an entire authentication system. And user account system.


With the project set up, I'm gonna head back to our user stories
which you'll recall we're using to guide our development.
Let's start in the registration and user accounts category.
Since this is something that's pretty fundamental to any website.
The ability to log in and out register for an account and so on.
We can complete almost all the user stories in this category at once.
By using a popular pre-built package called django-allauth.
And the reason we're using allauth as opposed to building our own authentication system.
Is that allauth already has all the features we'll need for the site
and it's completely customizable and will allow us to add even more functionality later on.
Additionally, it's open-source so it's backed by millions of developers who
keep it secure and up-to-date.
And it's unlikely we'd be able to create something better without a ton of extra development time.
In general with software development there's no need to reinvent the wheel.
So we're going to use allauth knowing that it's well supported
secure and we'll do everything we need right out of the box.
As you probably guessed the first thing we need to do is
install it with "pip3 install django-allauth==0.41.0"
From here let's head to the allauth documentation and grab a few settings to add to our settings.py file.
I'm gonna simply copy and paste these from the documentation
which will guarantee we're using the most up-to-date settings.
And when we're done we'll go over what each thing does.
First we need the request context processor which should already be there by default.
So I'm just gonna add a comment that it's required by allauth so that I remember not to remove it.
If it's not in your settings, just paste it in from the allauth documentation.
We also need a couple of authentication backends.
So I'll put those here.
And let's just get rid of these.
And we need to add a few apps to our installed apps.
So let's grab those.
And put them in.
And you'll see I've skipped the ones that were there by default, auth and messages.
Lastly I'm going to add something right underneath the authentication backends.
site_id = 1
With that finished let's talk about what each one of these settings does.
The request context processor here allows allauth and django itself for
that matter to access the HTTP request object in our templates.
So for example, if we wanted to access request.user or request.user.email in our django templates.
We'll be able to do it with this context processor.
It's required because the allauth templates which we'll see and customize later on
use the request object frequently.
So we need that so the allauth templates will work right.
The authentication backends we added give us a really nice feature.
Allowing users to log into our store via their email address which at the time of
recording this isn't supported by default in django.
The other back-end handles superusers logging into the admin which allauth doesn't handle.
So we defer to the default django Code for that.
Finally the apps we added to our installed apps are allauth itself and these two.
account which is the allauth app that allows all the basic user account stuff like logging in and out.
User registration and password resets.
And the other one's, social account which specifically handles logging in via
social media providers like Facebook and Google.
The contrib.sites app and the site _id setting we added.
Are used by the social account app to create the proper callback URLs
when connecting via social media accounts.
As an aside we won't actually use the social media stuff in
our site but I definitely encourage you to give it a shot in your own projects.
Because it's a really nice feature to have. Not only because it makes it a lot
more likely that users will create an account and use your site if they can do
it with a single click.
But also because when users connect with their social media accounts.
It allows you to track your user's activity a lot more effectively.
Which is great for things like email marketing and advertising, if you're trying to build a business.
Additionally, it allows users to connect payment accounts like Google pay and Apple pay
and a whole host of other things that just make their experience a lot smoother.
Getting back to the code here let's add the allauth urls to our project level urls.py file.
i'll create a path called accounts.
And use it to include all the allauth.urls
I'm doing this manually because at the time of recording this
the allauth doc's are still using the old url function from before django2
And I want to keep everything consistent with the version of django we're using.
We also need to import include here at the top. Since it's not imported by default.
So this gives us all the urls we need for login logout password resets and so on.
Next we need to run migrations to update the database since we added some new apps.
So let's do that with Python3 manage.py migrate.
Looks like we're all good there so now I'm going to run the server with Python3 manage.py run server.
And expose the port.
And then open our project
Navigate to the admin.
And log in.
And update the domain of the default site to boutiqueado.example.com
And we can change the display name to Boutique Ado
This isn't a critical setting but it would be if we were using social media authentication.
So we might as well do it now in case we want to use it in the future.
In the next video we'll finish adding the required settings for allauth.
And test our authentication system

We last left our project after beginning the initial setup of django-allauth
let's finish that and test it in this video.
I'll begin by logging out of the admin and stopping the development server.
Before anything we need to make a small correction to the urls.py file
By adding a slash at the end of the accounts path, to make sure it's included
in the allauth urls. and they're generated properly.
For this video, we're going to start again in settings.py.
Since by default allauth will send confirmation emails to any new accounts.
We need to temporarily log those emails to the console so we can get the confirmation links.
To do that we can set the EMAIL_BACKEND setting
to django.core.mail.backends.console.EmailBackend"
I'm also going to paste in some additional settings from the completed project and explain what each one does.
The account authentication method is what tells allauth that we want to allow
authentication using either usernames or emails.
These three email settings here
make it so that an email is required to register for the site.
Verifying your email is mandatory so we know users are using a real email.
And they're gonna be required to enter their email twice on the registration page
to make sure that they haven't made any typos.
Finally we're setting a minimum username length of four characters.
And specifying a login url and a url to redirect back to after logging in.
I'm gonna change the login redirect url to /success
Only temporarily, even though this url doesn't exist and you'll see why in a moment.
With all these settings complete the only thing left to do is test it.
In order to test whether allauth is working properly.
I'm gonna run the server with python3 manage.py runserver
And open the project.
And then navigate to /accounts/login
I'll attempt to login using the superuser we created earlier.
And you'll see that this directs us back to a page telling us we need to confirm our email.
So we know allauth is working because email confirmations are now required in order to log in.
The only problem here is that we created this user before installing allauth.
So we need to create and confirm an email manually.
To do that I'm gonna login to the admin.
And open the email address model that was set up when we ran the migrations that came with allauth.
Notice that this model is under the accounts app.
Which specifically is the allauth accounts app that we added to installed apps.
You'll see there's also a social accounts app here.
And you can see the site's framework
that comes from adding django.contrib.sites to our installed apps.
So opening the email address model.
I'll click Add email address.
Select my username.
Enter an email.
And select both verified and primary. To convince allauth that we verified the email.
Saving that. Let's logout and head back to the login page to see the difference.
Now when we log in with the superuser.
we get a 404 page not found, but that's actually a good thing if you look closely.
Because we're actually at the /success url.
That means that our login system redirected us back to the login redirect url in settings.py.
Which confirms that authentication is working properly.
At this point, I'm going to go back to settings.py.
And change the login redirect url to just /
Which means upon logging in will just be redirected to the home page of our store.
It looks like everything is working correctly so far
so let's freeze the requirements of our project with pip3 freeze > requirements.txt
With all that finished, there's one more thing I want to do before we commit our changes.
And that is to get our templates directory set up.
So we have a place to start writing some front-end code.
Let's type mkdir templates
And mkdir templates/allauth
Which will hold our customized allauth templates.
Finally I'm going to commit my changes with git add .
git commit -m "setup allauth"
and git push
In the next video we'll get our home page setup and begin customizing the login functionality
