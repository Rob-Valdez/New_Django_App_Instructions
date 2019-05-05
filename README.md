# New_Django_App_Instructions

1. create project directory

2. pipenv shell

3. pipenv install Django==2.1

4. django-admin startproject [projectname] .

5. python manage.py runserver

6. open browser and check for validation

7. python manage.py startapp [appname]

8. in settings.py add [appname] to installed apps

        '[appname].apps.[Appname]Config'

9. in [appname] directory, create templates directory called 'templates'

10. create [appname].html as a template within the new 'templates' directory

11. in new template file add placeholder text: 
    
        <h1>Hello world</h1>

12. in [appname]'s views.py file create a view

        def [appname](request):
            return render(request, '[appname].html', {})

13. create urls.py file within app and add the following

        from django.urls import path
        from . import views

        urlpatterns = [
            path('', views.[appname], name='[appname]'),
        ]

14. in [projectname] urls.py file, add urls for [appname]

        from django.urls import path, include

        urlpatterns = [
            path('admin/', admin.site.urls),
            path('', include('[appname].urls')),
        [


15. python manage.py runserver

16. validate that placeholder text is there

17. pipenv lock

18. at root directory for project, create Procfile file 

19. add to Procfile

        web: gunicorn [projectname].wsgi --log-file - 

20. pipenv install gunicorn==19.9.0


22. pipenv install whitenoise==3.3.1

23. in root project directory, add 'static' directory

24. in settings.py, 

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

25. initiate git in project directory

26. git add -A

27. git commit -m "configured for heroku"

28. create github repository named [projectname]

29. git remote add origin https://github.com/Rob-Valdez/[reponame].git

30. git push -u origin master

31. heroku create [projectname]

32. heroku git:remote -a [projectname]

33. log into heroku and under settings, create a new Config Vars value

    django_secret_KEY

    and add the string for the secret key

33. git push heroku master
