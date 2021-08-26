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
