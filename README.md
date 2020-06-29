# Cheatsheet for Django QuerySets
Current Django Version: [3.0](https://docs.djangoproject.com/en/3.0/ref/models/querysets/)

## Methods that return new [QuerySets](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#methods-that-return-new-querysets)


Dajngo uses MVC system : Model - View - Controllers

# Creatin a Django Project:


`python -m venv  venv` create a virtual encironment

`source venv/bin/activate` activate virtual environment venv

`pip install -r requirements.txt` install all the required tools

# 0. Create Database:

`createdb db_name `

# 1. Start a Project:


`django-admin startproject <name> .`  This makes sure that the project is not nested


    mysite/            --> A container for your project/ can be renamed.   

    manage.py       --> A command-line utility that lets you interact with this Django project. 
    
    mysite/.        --> Actual Python package for your project     
    
        __init__.py --> An empty file that tells Python that this directory should be considered a Python package.   
        
        settings.py --> Settings/configuration for this Django project.       
        
        urls.py.    --> The URL declarations for this Django project; a “table of contents” of your Django-powered site.  
        
        asgi.py     --> An entry-point for ASGI-compatible web servers to serve your project.   
        
        wsgi.py     --> An entry-point for WSGI-compatible web servers to serve your project.`  
        
  
        
        
# 2. Verify Django project works. Change into the outer mysite directory

`python manage.py runserver`

Starting development server at http://127.0.0.1:8000/

Quit the server with CONTROL-C.


# Changing the port from the default development server on the internal IP at port 8000.

`python manage.py runserver 8080`

# Changing the server’s IP, pass it along with the port. 

`python manage.py runserver 0:8000`

# 3. Create your app, make sure you’re in the same directory as manage.py , use:

`python manage.py startapp name`


# 4. Make. migration

The migrate command looks at the INSTALLED_APPS setting and creates any necessary database tables according to the database settings in your project/settings.py file and the database migrations shipped with the app (Next migrations will completed after the models are ceated, look at #7). 
 
 `python manage.py migrate`


`python manage.py createsuperuser`


# 13. In our app, create models:

Models are Python objects that define the structure of an application's data, and provide mechanisms to manage (add, modify, delete) and query records in the database.
Here, each model is represented by a class that subclasses django.db.models.Model. Each model has a number of class variables, each of which represents a database field in the model.
  # App/models.py
  
    from django.db import models

    class Question(models.Model):
  
        question_text = models.CharField(max_length=200)
      
        pub_date = models.DateTimeField('date published')
      
# 14 Activate models

The model code gives Django a lot of information. With it, Django is able to:
 a. Create a database schema (CREATE TABLE statements) for this app.
 b. Create a Python database-access API for accessing Question and Choice objects.
   after telling the project that the app is installed in the project INSTALLED_APPS section in settings.
   
   `python manage.py makemigrations <app_name>`, then run
   
   `python manage.py migrate <app_name>`

# 6. Views:

A view is a request handler function, which receives HTTP requests and returns HTTP responses. 
Views access the data needed to satisfy requests via models, and delegate the formatting of the response to templates.
`from django.http import HttpResponse`

  `def index(request):`
  
    `return HttpResponse()`
    
# 7. URLs for App: 

While it is possible to process requests from every single URL via a single function, it is much more maintainable to write a separate view function to handle each resource. A URL mapper is used to redirect HTTP requests to the appropriate view based on the request URL. 
The URL mapper can also match particular patterns of strings or digits that appear in a URL and pass these to a view function as data.

    from django.urls import path

     from . import views
 
        urlpatterns = [
 
        path('', views.index, name='index'),
 
        ]

# 8. URLs for project.  

When Django encounters include(), it chops off whatever part of the URL matched up to that point and 
sends the remaining string to the included URLconf for further processing.
URLconf is like a table of contents for your Django-powered Web site.

     from django.contrib import admin

     from django.urls import include, path

     urlpatterns = [

      path('polls/', include('polls.urls')),

      path('admin/', admin.site.urls),

     ]

# 9. A index view is now wiredinto the URLconf. Verify it’s working with:

`python manage.py runserver`

# 10. Completing Setup In project/settings.py

 # Add Installed_apps 

    Add'APP_name', 'django_extensions' under INSTALLED_APPS 

 # Add Database:

    If you are not using SQLite as your database, additional settings such as USER, PASSWORD, and HOST

    `DATABASES = {

        'default': {

            'ENGINE': 'django.db.backends.postgresql',

            'NAME': 'mydatabase'
        }
    }`




   
# 15 Playing with the API/Python shell

Now, let’s hop into the interactive Python shell and play around with the free API Django gives you. To invoke the Python shell, use this command:

`python manage.py shell_plus`

# 16 __str__() AND  Model.__str__()

It’s important to add __str__() methods to your models, not only for your own convenience when dealing with the interactive prompt, but also because objects’ representations are used throughout Django’s automatically-generated admin.

    class Choice(models.Model):

        # ...
    
    def __str__(self):
    
        return self.choice_text



# settings.py

    STATICFILES_DIRS = [
        os.path.join(BASE_DIR, "static"),
    ]


# Templates: 

A template is a text file defining the structure or layout of a file (such as an HTML page), with placeholders used to represent actual content. A view can dynamically create an HTML page using an HTML template, populating it with data from a model. A template can be used to define the structure of any type of file; it doesn't have to be HTML!


Other commands:

1. Create Database
2. Set up your models
3. Run makemigrations `
4. Run python manage.py migrate
5. If you make alterations to models, rerun the migrations commands to update db.
6. Tests to pass: python manage.py test --failfest

`python manage.py shell_plus` to complete commands in the py shell

`python -m venv  venv` create a virtual encironment

`source venv/bin/activate` activate virtual environment venv

`pip install -r requirements.txt` install all the

`django-admin.py startproject <project_name>` start a new Django project

`git init` Initialize new Git repo

`git add -A` add your changes to staging and then to the local repo.

`git commit -am` initial commit

`git remote add origin` PUSH your files to central repo.

`git remote add origin github.com/Carole-Ouedraogo/new_repo`

`git push -u origin master`

`createdb <db_name>`

`python3 manage.py test`

`python3 manage.py migrate`

`python3 manage.py makemigrations <app_name>`

`python manage.py test --failfest` test file is run 

 `new_var = _` assigns, and gives you access to previous output in python shell
 
 `ON DELETE CASCADE` delete child when parent is deleted
 
 `ON DELETE SET NULL` set null when parent is deleted

****************************************************************************************************
# Django APIs

**Can be chained:**

```python
Entry.objects.filter(**kwargs).exclude(**kwargs).order_by(**kwargs)
```

 * [filter](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#filter)
 * [exclude](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#exclude)
 * [annotate](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#annotate)
 * [order_by](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#order-by)
 * [reverse](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#reverse)
 * [distinct](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#distinct)
 * [values](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#values)
 * [values_list](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#values-list)
 * [dates](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#dates)
 * [datetimes](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#datetimes)
 * [none](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#none)
 * [all](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#all)
 * [union](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#union)
 * [intersection](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#intersection)
 * [difference](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#difference)
 * [select_related](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#select-related)
 * [prefetch_related](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#prefetch-related)
 * [extra](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#extra)
 * [defer](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#defer)
 * [only](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#only)
 * [using](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#using)
 * [select_for_update](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#select-for-update)
 * [raw](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#raw)

## Operators that return new [QuerySets](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#operators-that-return-new-querysets)

 * [AND (&)](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#and)
 * [OR (|)](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#or)

## Methods that do not return [QuerySets](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#methods-that-do-not-return-querysets)

 * [get](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#get)
 * [create](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#create)
 * [get_or_create](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#get-or-create)
 * [update_or_create](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#update-or-create)
 * [bulk_create](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#bulk-create)
 * [bulk_update](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#bulk-update)
 * [count](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#count)
 * [in_bulk](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#in-bulk)
 * [iterator](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#iterator)
 * [latest](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#latest)
 * [earliest](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#earliest)
 * [first](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#first)
 * [last](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#last)
 * [aggregate](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#aggregate)
 * [exists](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#exists)
 * [update](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#update)
 * [delete](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#delete)
 * [as_manager](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#as-manager)
 * [explain](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#explain)

## Field lookups

**Field lookups are how you specify the meat of an SQL WHERE clause. They’re specified as keyword arguments to the QuerySet methods *filter()*, *exclude()* and *get()*.**

```python
Example: Entry.objects.get(id__exact=14)  # note double underscore.
```

 * [exact](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#exact)
 * [iexact](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#iexact)
 * [contains](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#contains)
 * [icontains](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#icontains)
 * [in](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#in)
 * [gt](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#gt)
 * [gte](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#gte)
 * [lt](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#lt)
 * [lte](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#lte)
 * [startswith](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#startswith)
 * [istartswith](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#istartswith)
 * [endswith](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#endswith)
 * [iendswith](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#iendswith)
 * [range](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#range)
 * [date](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#date)
 * [year](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#year)
 * [iso_year](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#iso-year)
 * [month](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#month)
 * [day](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#day)
 * [week](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#week)
 * [week_day](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#week-day)
 * [quarter](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#quarter)
 * [time](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#time)
 * [hour](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#hour)
 * [minute](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#minute)
 * [second](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#second)
 * [isnull](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#isnull)
 * [regex](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#regex)
 * [iregex](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#iregex)

**Protip: Use [in](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#in) to avoid chaining [filter()](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#filter) and [exclude()](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#exclude)**

```python
Entry.objects.filter(status__in=['Hung over', 'Sober', 'Drunk'])
```

## Aggregation functions ([link](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#aggregation-functions))

 * [expression](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#expression)
 * [output_field](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#output-field)
 * [filter](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#aggregate-filter)
 * [\*\*extra](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#id7)
 * [Avg](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#avg)
 * [Count](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#id8)
 * [Max](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#max)
 * [Min](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#min)
 * [StdDev](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#stddev)
 * [Sum](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#sum)
 * [Variance](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#variance)

## Query-related tools ([link](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#query-related-tools))

 * [Q() objects](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#q-objects)
 * [Prefetch() objects](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#prefetch-objects)
 * [prefetch_related_objects()](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#prefetch-related-objects)
 * [FilteredRelation() objects](https://docs.djangoproject.com/en/3.0/ref/models/querysets/#filteredrelation-objects)

- - -

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Django-QuerySet-Cheatsheet</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">@chrisdl and @briandant</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.<br />

The [contributors](https://github.com/chrisdl/Django-QuerySet-Cheatsheet/graphs/contributors) are as gods among ants and shall forever be remembered as such.

The Django web framework referenced in the Django-QuerySet-Cheatsheet is ​© 2005-2018 Django Software Foundation.
Django is a registered trademark of the Django Software Foundation.
