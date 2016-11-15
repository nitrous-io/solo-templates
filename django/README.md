## Django

### Sample application

A sample Django scaffold has been created for you in
`/home/nitrous/code/example`, with the database already set up.  It is the
equivalent to running the following:

```
cd ~/code
mkdir example
cd example
django-admin startproject example .
# configure example/settings.py to point database to example_development
python manage.py syncdb --noinput
# create User.objects.create_superuser with python manage.py shell
```

You can start the server by running `~/code/example/start-app` from the command
line.  Once it is running, you can use the preview menu to view the application
in a new tab.  Opening the `~/code/example/start-app` file is a good way of
finding out how to get your own Django application running.

Feel free to remove the `~/code/example` directory if you no longer need it.

### Create Django app

To install Django in a virtual environment and create a new Django project, run the following commands:

You can replace `django-env` with a name of your choice.

```
$ cd ~/code
$ virtualenv --no-site-packages django-env
$ source django-env/bin/activate
(django-env)$ pip install django
(django-env)$ django-admin.py startproject myproject
(django-env)$ cd myproject
```

The above is the [recommended way to install
Django](https://docs.djangoproject.com/en/1.8/topics/install/#installing-an-official-release-with-pip),
and uses the optional 2nd step of `virtualenv` to provide an isolated Python environment for your project.

You can configure your database settings in `~/code/django-env/myproject/myproject/settings.py`.

To install other Python packages you need, create a `requirements.txt` file:

```
$ cd ~/code/django-env
$ pip freeze > requirements.txt
```

After adding your dependencies to the `requirements.txt` file, you can then install them by running:

```
$ pip install -r requirements.txt
```

### Preview

You will need to listen to 0.0.0.0 when running the Django (gunicorn) server in order
to preview your app. You can do this by running:

`gunicorn appname.wsgi --bind 0.0.0.0:3000`

The above command assumes you are previewing your app on port 3000, which is
the default preview port set up for this project, and that your app is called `appname`.


## Postgres

A `postgres` superuser has been created with username `nitrous`, it has access to the
database `example_development`.
