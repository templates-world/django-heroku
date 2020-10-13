# django-heroku

A simple template of Django's tutorial with Heroku deploy.

## Setup

### Setup Heroku Locally

Before start, we need to login to Heroku. You must download the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install) for that. After that, simply run:

```
heroku login
```

If you didn't create a project, you can create one using

```
heroku create <your project name>
```

***To note:** The name is optional. A random name will be generated automatically if you don't precise it.*

### Local Installation and Run

**Mac/Linux:**

```
python3 -m pip install --user virtualenv
python3 -m venv env
source env/bin/activate
pip install django
cd mysite
pip install gunicorn dj-database-url whitenoise psycopg2
python3 manage.py migrate
python3 manage.py runserver
```

**Windows:**

```
py -m pip install --user virtualenv
py -m venv env
.\env\Scripts\activate
pip install django
cd mysite
python manage.py migrate
python manage.py runserver
```

### Deploy to heroku

Before deploy, replace ``<your project name>`` in ``mysite/mysite/settings.py`` by the name of your project that you created before. Then setup the remote (link to send the website) using:

```
heroku git:remote -a <your project name>
```

Due to some possible errors, we will disable the ``collect`` dependency using

```
heroku config:set DISABLE_COLLECTSTATIC=1 
```

Finally, push the project:

```
git push heroku master
```

You simply need to migrate the database and create a super user now:

```
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```