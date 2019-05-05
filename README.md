# New_Django_App_Instructions

1. create project directory

2. pipenv shell

3. pipenv install Django==2.1

4. django-admin startproject [projectname] .

5. python manage.py runserver

6. open browser and check for validation

7. python manage.py startapp [appname]

8. in settings.py add [appname] to installed apps

9. in [appname] directory, create templates directory called 'templates'

10. create [appname].html as a template within the new 'templates' directory

11. in new template file add placeholder text: 
    
        <h1>Hello world</h1>

12. in [appname]'s views.py file create a view

        def [appname](request):
            return render(request, '[appname].html', {})


13. in [projectname] urls.py file, add urls for [appname]

        from django.urls import path, include

        urlpatterns = [
            path('admin/', admin.site.urls),
            path('', include('[appname].urls')),
        [

14. create urls.py file within app and add the following

        from django.urls import path
        from . import views

        urlpatterns = [
            path('', views.[appname], name='[appname]'),
        ]

15. python manage.py runserver

16. validate that placeholder text is there

17. pipenv lock

18. at root directory for project, create Procfile file 

19. add to Procfile

        web: gunicorn [projectname].wsgi --log-file - 

20. pipenv install gunicorn==19.9.0

21. add to settings.py

        ALLOWED_HOSTS = ['*']

22. pipenv install whitenoise==3.3.1

23. in settings.py, in INSTALLED_APPS, above 'django.contrib.staticfiles', add

        'whitenoise.runserver_nostatic',
    
    in MIDDLEWARE, after SessionMiddleware, add
    
        'whitenoise.middleware.WhiteNoiseMiddleware',
        
    at the bottom of the settings file, add
    
        STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
        STATIC_URL = '/static/'
        STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
        STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'

24. initiate git in project directory

25. git add -A

26. git commit -m "configured for heroku"

27. create github repository named [projectname]

28. git remote add origin https://github.com/Rob-Valdez/[reponame].git

29. git push -u origin master

30. heroku create [projectname]

31. heroku git:remote -a [projectname]

32. git push heroku master

## TODO

create env variable from django secret key
