# New_Django_App_Instructions

create project directory

pipenv shell

pipenv install Django==2.1

django-admin startproject [projectname] .

python manage.py runserver

open browser and check for validation

python manage.py startapp [appname]

in settings.py add [appname] to installed apps

create view

    def [appname](request):
        return render(request, '[appname].html', {})

create templates directory in [appname] directory called 'templates'

create [appname].html as a template within the new 'templates' directory

in new template file add placeholder text: 
    
    <h1>Hello world</h1>

add app urls to project

    import include
add

    path('', include('[appname].urls')),

create urls.py file within app and add the following

    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.[appname], name='[appname]'),
    ]

python manage.py runserver
validate that placeholder text is there

pipenv lock

create Procfile for project at root directory for project
add to Procfile

    "web: gunicorn [projectname].wsgi --log-file -" 

pipenv install gunicorn==19.9.0

settings.py

    ALLOWED_HOSTS = ['*']

initiate git in project directory
git add -A
git commit -m "configured for heroku"

create github repository

git remote add origin https://github.com/Rob-Valdez/[reponame].git
git push -u origin master

heroku create [projectname]
heroku git:remote -a [projectname]
heroku config:set DISABLE_COLLECTSTATIC=1

git push heroku master

## pending steps
collect static files
create env variable from django secret key
