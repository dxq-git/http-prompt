HTTP Prompt
===========

|PyPI| |Travis| |Appveyor| |Coverage|

HTTP Prompt is an interactive command-line HTTP client featuring autocomplete
and syntax highlighting, built on HTTPie_ and prompt_toolkit_.

.. image:: https://raw.githubusercontent.com/eliangcs/http-prompt/master/http-prompt.gif


Installation
------------

Just install it like a regular Python package::

    $ pip install http-prompt

You'll probably see some permission errors if you're trying to install it on
the system-wide Python. It isn't recommended. But if that's what you want to
do, you need to ``sudo``::

    $ sudo pip install http-prompt

Another alternative is to use ``--user`` option to install the package into
your user directory::

    $ pip install --user http-prompt

To upgrade HTTP Prompt, do::

    $ pip install -U http-prompt


Quickstart
----------

To start a session, you use the ``http-prompt`` executable:

.. code-block:: bash

    # Start with the given URL
    $ http-prompt http://httpbin.org

    # Or start with some initial options
    $ http-prompt localhost:8000/api --auth user:pass username=somebody

Once you're in a session, you can use the following commands.

To change URL address, use ``cd``:

.. code-block:: bash

    # Relative URL path
    > cd api/v1

    # Absolute URL
    > cd http://localhost/api

To add headers, querystring, or body parameters, use the syntax as in HTTPie_.
The following are all valid:

.. code-block:: bash

    > Content-Type:application/json username=john
    > 'name=John Doe' apikey==abc
    > Authorization:"Bearer auth_token"

You can also add HTTPie_ options like this:

.. code-block:: bash

    > --form --auth user:pass
    > --verify=no username=jane

To preview how HTTP Prompt is going to call HTTPie_, do:

.. code-block:: bash

    > httpie post
    http --auth user:pass --form POST http://localhost/api apikey==abc username=john

You can temporarily override the request parameters by supplying options and
parameters in ``httpie`` command. The overrides won't affact the later
requests.

.. code-block:: bash

    # No parameters initially
    > httpie
    http http://localhost

    # Override parameters temporarily
    > httpie /api/something page==2 --json
    http --json http://localhost/api/something page==2

    # Current state is not affected by the above overrides
    > httpie
    http http://localhost

To actually send a request, enter one of the HTTP methods:

.. code-block:: bash

    > get
    > post
    > put
    > patch
    > delete
    > head

The above HTTP methods also support temporary overriding:

.. code-block:: bash

    # No parameters initially
    > httpie
    http http://localhost

    # Send a request with some overrided parameters
    > post /api/v1 --form name=jane

    # Current state remains intact
    > httpie
    http http://localhost

To remove an existing header, a querystring parameter, a body parameter, or an
HTTPie_ option:

.. code-block:: bash

    > rm -h Content-Type
    > rm -q apikey
    > rm -b username
    > rm -o --auth

To reset the session, i.e., clear all parameters and options:

.. code-block:: bash

    > rm *

To exit a session, simply enter:

.. code-block:: bash

    > exit

Note that all the options are gone once you exit.


Roadmap
-------

* User configuration file, i.e., an RC file
* More HTTP headers for autocomplete
* More tests, e.g., integration test and testing on Windows
* More documentation
* Support for advanced HTTPie syntax, e.g, ``field:=json`` and ``field=@file.json``
* Support for cURL command preview
* Shell command evaluation
* Python syntax evaluation
* HTTP/2 support


.. |PyPI| image:: https://img.shields.io/pypi/v/http-prompt.svg
    :target: https://pypi.python.org/pypi/http-prompt

.. |Travis| image:: https://api.travis-ci.org/eliangcs/http-prompt.svg?branch=master
    :target: https://travis-ci.org/eliangcs/http-prompt

.. |Appveyor| image:: https://ci.appveyor.com/api/projects/status/9tyrtce5omcq1yyk/branch/master?svg=true
    :target: https://ci.appveyor.com/project/eliangcs/http-prompt/branch/master

.. |Coverage| image:: https://coveralls.io/repos/github/eliangcs/http-prompt/badge.svg?branch=master
    :target: https://coveralls.io/github/eliangcs/http-prompt?branch=master

.. _HTTPie: https://github.com/jkbrzt/httpie
.. _prompt_toolkit: https://github.com/jonathanslenders/python-prompt-toolkit
