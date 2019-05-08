# New_Django_App_Instructions

1. create project directory

2. pipenv shell

3. pipenv install Django==2.1

4. django-admin startproject [projectname] .

5. python manage.py runserver

6. open browser and check for validation

7. python manage.py startapp [appname] # presentations, for example

8. in settings.py add [appname] to installed apps

        '[appname].apps.[Appname]Config'
        
   and

        "DIRS": ["templates/"],

9. in [projectname] directory, create templates directory called 'templates'

10. in new 'templates' directory, create html file named 'base.html'

11. add the following to base.html:

        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

        {% block page_content %}{% endblock %}

        <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>

12. in [appname] directory, create templates directory called 'templates'

13. create home.html as a template within the new 'templates' directory

14. in home.html add placeholder text: 
    
        {% extends "base.html" %}

        {% block page_content %}
        <h1>Hello, World!</h1>
        {% endblock %}

15. in [appname]'s views.py file create a view

        def [appname](request):
            return render(request, '[appname].html', {})

16. create urls.py file within app and add the following

        from django.urls import path
        from . import views

        urlpatterns = [
            path('', views.[appname], name='[appname]'),
        ]

17. in [projectname] urls.py file, add urls for [appname]

        from django.urls import path, include

        urlpatterns = [
            path('admin/', admin.site.urls),
            path('', include('[appname].urls')),
        [


18. python manage.py runserver

19. validate that placeholder text is there

20. python manage.py createsuperuser

21. pipenv lock

22. at root directory for project, create Procfile file 

23. add to Procfile

        web: gunicorn [projectname].wsgi --log-file - 

24. pipenv install gunicorn==19.9.0

25. pipenv install whitenoise==3.3.1

26. in root project directory, add 'static' directory

27. in settings.py, 

    copy the secret key to a notepad

    change SECRET_KEY to 
    
        'django_secret_KEY'
    
    change allowed hosts as follows:

        ALLOWED_HOSTS = ['*']
    
    in INSTALLED_APPS, as the last app, add

        'whitenoise.runserver_nostatic',
            
    in MIDDLEWARE, after SessionMiddleware, add
    
        'whitenoise.middleware.WhiteNoiseMiddleware',
        
    at the bottom of the settings file, add
    
        STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
        STATIC_TMP = os.path.join(BASE_DIR, 'static')
        STATIC_URL = '/static/'

        os.makedirs(STATIC_TMP, exist_ok=True)

        STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
        STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'

28. initiate git in project directory

29. git add -A

30. git commit -m "configured for heroku"

31. create github repository named [projectname]

32. git remote add origin https://github.com/Rob-Valdez/[reponame].git

33. git push -u origin master

34. heroku create [projectname]

35. heroku git:remote -a [projectname]

36. log into heroku and under settings, create a new Config Vars value

    django_secret_KEY

    and add the string for the secret key

37. git push heroku master
