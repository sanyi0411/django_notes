# Django notes

## Hello world of django
1. Install python
    ```shell
    sudo apt update
    sudo apt upgrade
    sudo apt install python3
    sudo apt install python3-pip
    ```

2. Install virtualenv
    ```shell
    sudo apt install python3-virtualenv
    ```

3. Create folder for the project
    ```shell
    mkdir django-tutorial
    cd django-tutorial
    ```

4. Create virtual environment
    ```shell
    python3 -m virtualenv django-venv
    ```

    Directory structure will look like this:
    ```
    ├── django_tutorial 
    │   └── django-venv 
    │       ├── bin 
    │       ├── lib 
    │       └── pyvenv.cfg 
    ```
5. Take note of the contents of the ```django-venv/bin``` folder

6. Activate the virtual environment
    ```shell
    source django-venv/bin/activate
    ```
    This will drop you in a new shell. See the ```(django-venv)``` at the beginning of the propt

7. Install django in the venv
    ```shell
    pip3 install django
    ```

8. Take note of the files in the ```django-venv/bin``` folder again. ```django-admin``` has appeared

9. Start a new project
    ```shell
    django-admin startproject myproject
    ```

    The directory structure will look like this:
    ```
    django_tutorial 
    │   ├── django-venv 
    │   │   ├── bin 
    │   │   │   ├── activate 
    │   │   │   ├── django-admin 
    │   │   │   ├── pip 
    │   │   ├── lib 
    │   │   └── pyvenv.cfg 
    │   └── myproject 
    │       ├── manage.py 
    │       └── myproject 
    │           ├── asgi.py 
    │           ├── __init__.py 
    │           ├── settings.py 
    │           ├── urls.py 
    │           └── wsgi.py 
    ```

10. Move into the new project folder
    ```shell
    cd myproject
    ```

11. Create a new app in the project
    ```shell
    python3 manage.py startapp myapp
    ```

    The directory structure will look like this:
    ```
    django_tutorial 
    │   ├── django-venv 
    │   └── myproject 
    │       ├── manage.py 
    │       ├── myapp 
    │       │   ├── admin.py 
    │       │   ├── apps.py 
    │       │   ├── __init__.py 
    │       │   ├── migrations 
    │       │   ├── models.py 
    │       │   ├── tests.py 
    │       │   └── views.py 
    │       └── myproject 
    │           ├── asgi.py 
    │           ├── __init__.py 
    │           ├── __pycache__ 
    │           ├── settings.py 
    │           ├── urls.py 
    │           └── wsgi.py 
    ```

12. Start the server
    ```shell
    python3 manage.py startserver
    ```
13. Open the given URL. You should see an ```The install worked successfully``` page

## Basic architecture

### MVC architecture
Model-View-Controller

Most web framework use this, but not django

- Controller: intercepts user requests.
- Model: data definitions, processing logic, interaction with database 
- View: presentation layer, placement and formatting, sends result to controller

```mermaid
flowchart LR;
    id1[(Database)];
    Client-- Request -->Controller;
    Controller-- Response -->Client;
    Controller-->View;
    Controller-->Model;
    View-->Model;
    Model-->View;
    Model-->id1;
    id1-->Model;
```

### MVT architecture
Model-View-Template

Slight variation on the MVC

- Model: data layer
- View: processing logic
- Template: presentation layer

```mermaid
graph LR;
    User((User))-->URL;
    URL-->User;
    URL-->View;
    View-->URL;
    View-->Model;
    Model-->View;
    View-->Template;
    Template-->View;
```

URL dispatcher:
- eqivalent to controller in MVC
- ```urls.py``` acts as dispathcer
    - defines URL patterns
    - a pattern is mapped with a view function

View:
- ```views.py```: created View definitions
- reads path, query, body parameters from requests
- interacts with model to perform CRUD operations
- uses the client's and model's data and renders its response using a template
- returns response to user

Model:
- ```models.py``` holds one or more model classes
- attributes of model class --> construct database table of matching structure
- view uses the client's and the model's data and renders its response using a template

Template:
- in the ```templates``` folder with the ```.html``` extension
- a template is a webpage
- mix of static HTML and Django Template Language blocks
- template preprocessor uses context data from View inserted in these blocks to formulate response
- View returns this response to the user

## Views and URLs

### View function

The function in the ```view.py``` (a.k.a view function):
 - fetches data from the client's request
    - takes a HttpRequest as parameter
 - applies a certain processing logic
 - sends the appropriate response back to the client
    - returns HttpResponse object


Function based view:
```python
# views.py (app)
from django.http import HttpResponse

def home(request):
    # some logic
    return HTTPResponse("Welcome to Little Lemon restaurant")

def myview(request):
    if request.method == 'GET':
        val = request.GET['key']
        # some logic
    
    if request.method == 'POST':
        val = request.POST['key']
        # some logic
```

Class based view:
```python
# views.py (app)
from django.http import HttpResponse
from django.views import View 

class MyView(View): 
    def get(self, request): 
        # logic to process GET request
        return HttpResponse('response to GET request') 
 
    def post(self, request): 
        # <logic to process POST request> 
        return HttpResponse('response to POST request')
```



### Routing

The ```urls.py``` file:
 - mapping a view function to a URL
 - it is good practice to create a ```urls.py``` in the app folder and include it in the project's ```urls.py```. This way the respective URLs for an app are clustered
    - in this case create a ```urls.py``` in the ```myapp``` folder
 - when a user makes a request, it is first handled by the ```urls.py``` at the project level
    - the project level ```urls.py``` will have to include the app level ```urls.py```


 ```python
# urls.py (project)
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls'))
]
 ```

```python
# urls.py (app)
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name="home"),
]
```