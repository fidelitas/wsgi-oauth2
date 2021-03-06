.. wsgi-oauth2 documentation master file, created by
   sphinx-quickstart on Fri Nov  4 07:40:13 2011.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

wsgi-oauth2
===========

.. image:: _static/oauth2.png

This module provides a simple WSGI middleware that requires the user to
authenticate via the specific `OAuth 2.0`_ service e.g. Facebook_, Google_,
GitHub_.

.. _OAuth 2.0: http://oauth.net/2/
.. _Facebook: http://www.facebook.com/
.. _Google: http://www.google.com/
.. _GitHub: https://github.com/


Prerequisites
-------------

It requires Python 2.6, 2.7, 3.2 or higher.
It has no dependencies for non standard libraries, but if there is an installed
:mod:`simplejson` library, it will be used instead of the standard :mod:`json`
package.


Installation
------------

You can install the package via downloading from PyPI_:

.. sourcecode:: console

   $ pip install wsgi-oauth2

If you want to use the bleeding edge, install it from the :ref:`Git repository
<sourcecode>`:

.. sourcecode:: console

   $ pip install git+git://github.com/dahlia/wsgi-oauth2.git

.. _PyPI: http://pypi.python.org/pypi/wsgi-oauth2


Predefined services
-------------------

There are some predefined services.

.. autodata:: wsgioauth2.google

.. autodata:: wsgioauth2.facebook

.. autodata:: wsgioauth2.github


Basic usage
-----------

::

    from myapp import app
    from wsgioauth2 import github

    client = github.make_client(client_id='...', client_secret='...')
    app = client.wsgi_middleware(app, secret='hmac*secret')


.. module:: wsgioauth2

:mod:`wsgioauth2` --- API references
------------------------------------

.. autoclass:: wsgioauth2.Service
   :members:

.. autoclass:: wsgioauth2.Client
   :members:

.. autoclass:: wsgioauth2.AccessToken
   :members:

.. autoclass:: wsgioauth2.WSGIMiddleware
   :members:

.. autoclass:: wsgioauth2.GitHubService
   :members:


.. _sourcecode:

Source code
-----------

The source code is available under MIT license. Check out from the GitHub__:

.. sourcecode:: console

   $ git clone git://github.com/dahlia/wsgi-oauth2.git

We welcome pull requests as well!

__ https://github.com/dahlia/wsgi-oauth2


Bugs
----

If you found bugs or want to propose some improvement ideas, use the
`issue tracker`_.

.. _issue tracker: https://github.com/dahlia/wsgi-oauth2/issues


Author
------

The package is written by `Hong Minhee`_.

.. _Hong Minhee: http://hongminhee.org/


Changelog
---------

Version 0.2.1
'''''''''''''

To be released

- Fixed a bug that :class:`~wsgioauth2.GitHubService` raises :exc:`KeyError`
  when users who didn't declare their name on GitHub tries to login.
  [:pull:`9` by Aymeric Augustin]


Version 0.2.0
'''''''''''''

Released on August 10, 2014.

- Now it bocomes compatible with Python 3.2 or later.


Version 0.1.4
'''''''''''''

Released on August 8, 2014.

- :attr:`~wsgioauth2.WSGIMiddleware.login_path` can now be configured to
  protect only a subsection of an application.
  [:pull:`8` by Aymeric Augustin]


Version 0.1.3
'''''''''''''

Released on June 19, 2013.

- :attr:`~wsgioauth2.WSGIMiddleware.forbidden_path` can now be configured.
  Default forbidden page is ugly so also allow forbidden path to be passed
  through to the protected application so it can be styled properly.
  [:pull:`4` by Mike Milner]
- :class:`~wsgioauth2.GitHubService` now takes an optional parameter
  ``allowed_orgs`` to limit access based on GitHub organizations.
  [:pull:`4` by Mike Milner]
- Fix :meth:`Client.request_access_token()` to understand
  :mimetype:`Content-Type` with ``charset``.
  [:pull:`5` by Jacob Kaplan-Moss]


Version 0.1.2
'''''''''''''

Released on March 22, 2013.

- Add predefined GitHub service (:data:`wsgioauth2.github`).
  [:pull:`3` by Mike Milner]
- Add option to set :envvar:`REMOTE_USER`.  [:pull:`3` by Mike Milner]


Version 0.1.1
'''''''''''''

Released on May 2, 2012.

- Set cookie with ``expires`` option if the response contains ``expires_in``
  parameter.  [:pull:`2` by mete0r]


Version 0.1.0
'''''''''''''

Released on November 4, 2011.  First version.
