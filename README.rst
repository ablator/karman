Ablator Python Client
=====================

This is *karman* -- a Python Client for the `ablator project`_.

.. _ablator project: https://github.com/ablator/ablator/

Using karman, you can connect to a hosted or self-hosted instance of ablator,
and check which functionalities to present to your user.

Installation
~~~~~~~~~~~~

To install karman, use pip::

    pip install karman

Usage
~~~~~

You can include karman.py in your code and use its `which` and `caniuse` methods. 

To do so, you'll need a username -- basically any string that uniquely identifies 
one of your users -- and the functionality id, which you can copy and paste from
the ablator web interface::

    import karman
    username = "(your user name string)"
    functionality_id = "f8077bfe-bb42-404c-a0d0-3fa107b01860"
    ablator_client = karman.Karman(base_url='http://ablator.space/')
    availability = ablator_client.which(username, functionality_id)

    # this will return one of the following:
    # availability == "breakthesystem.test-app.test-func.on"
    # availability == None

Both the `which` and the `caniuse` methods are blocking and will only return once
they get an answer from the ablator server. There is no caching implemented at the
moment.

The `which` method will return either a string that corresponds to the flavor slug
of the flavor that was selected for your user, or None, if the functionality is 
disabled for your user.

The `caniuse` method will return `True` if any flavor is activated for your user, 
and `False` otherwise. Use this method if you only want to use ablator to roll
out a functionality, as opposed to a/b testing.

Command Line
~~~~~~~~~~~~

If you install karman via pip, you also get the karman command line tool. To use it
run it like this::

    karman --base_url http://ablator.space/ <username> <functionality_id>

Add the -c parameter to continuously query the ablator server. If that's too fast
add slow parameter as well like this: -c -s
