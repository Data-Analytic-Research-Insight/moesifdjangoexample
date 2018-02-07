# Moesif Django Example

Django is a web application framework that many developers to serve APIs.

[Moesif](https://www.moesif.com) is an API analyatics platform. [moesifdjango](https://github.com/Moesif/moesifdjango)
is a middleware that makes integration with Moesif easy for Django based applications.

This is an example of django application with Moesif integrated. This example is based
on the quick start [tutorials of Django](https://docs.djangoproject.com/en/1.11/intro/) and [Django rest framework](http://www.django-rest-framework.org/#quickstart).

## Key files

moesifdjango's [github readme](https://github.com/Moesif/moesifdjango) already documented
the steps for setup Moesif Django. But here is the key file where the Moesif integration is added:

- `mysite/settings.py` added Moesif middleware related settings.

## How to run this example.

1. Setup [virtual env](https://virtualenv.pypa.io/en/stable/) if needed `virtualenv ENV`. Start the virtual env by `source ENV/bin/activate`

2. Install django if you haven't done so. `pip install Django`

3. Install moesifdjango in the environment by `pip install moesifdjango`

4. Install Django Rest Framework by, `pip install djangorestframework`

5. Be sure to edit the `mysite/setting.py` to change the application id to your
application id obtained from Moesif.

  ```
  MOESIF_MIDDLEWARE = {
      'APPLICATION_ID': 'your application id from moesif',
  }
  ```

6. `python manage.py runserver`

7. See `urls.py` for some urls that you can hit the server with
(e.g. `http://localhost:8000/users`), and the data
should be captured in the corresponding Moesif account of the application id.

## Using Celery (Optional)

If you are already using Celery in your Django application to manage task queueing,
the `moesifdjango` SDK can also take advantage of the benefits. Do the following steps:

1. Install Redis by, `pip install -U "celery[redis]"`

2. If you plan to use celery as the backend of asynchronous delivered logged requests,
you also need to add `moesifdjango` to your `INSTALLED_APPS`

3. Install django-celery by, `pip install django-celery`

  To enable `django-celery` for your project you need to add `djcelery` to `INSTALLED_APPS`:

  ```
  INSTALLED_APPS += ('djcelery', )
  ```

  then add the following lines to your settings.py:

  ```
  import djcelery
  djcelery.setup_loader()
  ```

4. Be sure to set the `USE_CELERY` to `True`

  ```
  MOESIF_MIDDLEWARE = {
      'USE_CELERY': True
  }
  ```
