Evernote
========

Service Description:
--------------------

This service allows to take notes, photos, schedules things and so on

modifications of settings.py
----------------------------

1) INSTALLED_APPS :

add or uncomment the following lines

.. code-block:: python

    INSTALLED_APPS = (
        # 'evernote',
        # 'th_evernote',
    )

to get

.. code-block:: python

    INSTALLED_APPS = (
        'evernote',
        'th_evernote',
    )


2) Cache :

After the default cache add :

.. code-block:: python

    CACHES = {
        'default':
        {
            'BACKEND': 'django.core.cache.backends.filebased.FileBasedCache',
            'LOCATION': BASE_DIR + '/cache/',
            'TIMEOUT': 600,
            'OPTIONS': {
                'MAX_ENTRIES': 1000
            }
        },
        # Evernote Cache
        'th_evernote':
        {
            'TIMEOUT': 500,
            "BACKEND": "django_redis.cache.RedisCache",
            "LOCATION": "redis://127.0.0.1:6379/1",
            "OPTIONS": {
                "CLIENT_CLASS": "django_redis.client.DefaultClient",
            }
        },

modifications of th_settings.py
-------------------------------

1) TH_SERVICES

add or uncomment the following line

.. code-block:: python

    TH_SERVICES = (
        # 'th_evernote.my_evernote.ServiceEvernote',
    )

to get

.. code-block:: python

    TH_SERVICES = (
        'th_evernote.my_evernote.ServiceEvernote',
    )


2) The service keys

It's strongly recommended that your put the following in a local_settings.py, to avoid to accidentally push this to a public repository


.. code-block:: python

    TH_EVERNOTE = {
        'sandbox': True,  # set it to False when in production
        'consumer_key': 'my key',
        'consumer_secret': 'my secret',
    }


creation of the table of the services
-------------------------------------

enter the following command

.. code-block:: bash

    python manage.py migrate


from the admin panel, activation of the service
-----------------------------------------------

from http://yourdomain.com/admin/django_th/servicesactivated/add/

* Select "Evernote",
* Set the Status to "Enabled"
* Check Auth Required: this will permit to redirect the user (or you) to the Evernote website to confirm the access of the Evernote account
* Provide a description

