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
Most web framework use this, but not django

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

```geojson
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": 1,
      "properties": {
        "ID": 0
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
              [-90,35],
              [-90,30],
              [-85,30],
              [-85,35],
              [-90,35]
          ]
        ]
      }
    }
  ]
}
```

```stl
solid cube_corner
  facet normal 0.0 -1.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 1.0 0.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
  facet normal 0.0 0.0 -1.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 1.0 0.0 0.0
    endloop
  endfacet
  facet normal -1.0 0.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 0.0 1.0
      vertex 0.0 1.0 0.0
    endloop
  endfacet
  facet normal 0.577 0.577 0.577
    outer loop
      vertex 1.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
endsolid
```