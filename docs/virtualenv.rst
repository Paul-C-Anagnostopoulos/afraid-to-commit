##################
Virtualenv and pip
##################


What is it?
===========

Virtualenv lets you create and manage virtual Python environments.

If you're running a Python project for deployment or development, the chances
are that you'll need more than one version of it, or the numerous other Python
applications it depends upon, to at any one time.

For example, when a new version of Django is released, you might want to check
your project is still compatible. You don't want to have to set up a whole new
server with a different version of Django to find out.

With virtualenv, you can quickly set up a a brand new Python environment, and
install your components into it - along with the new version of Django,
without touching or affecting what you already have running.

You can have literally dozens of virtualenvs on the same machine, all running
different versions of your Python software, all independently of each other,
and can safely make changes to one without affecting anything else.

pip goes hand-in-hand with virtualenv; in fact, it comes with virtualenv (as
well as separately). It's an installer, and is the easiest way to install
things into a virtualenv.


Install virtualenv
==================

Try:

	virtualenv --version
	
Do you have a version lower than 1.9? Upgrade it (some of these commands may
require `sudo`):

	pip install --upgrade virtualenv
	
If you got a "Command not found" when you tried to use virtualenv, try:

	pip install virtualenv
	
or:

	apt-get install python-virtualenv # for a Debian-based system
	
If that fails or you're using a different system, you might need more help:

	http://www.virtualenv.org/en/latest/#installation
	

Using virtualenv
================

Create and activate a virtual environment
-----------------------------------------

::

	virtualenv my-first-virtualenv
	cd my-first-virtualenv
	source bin/activate

Notice how your command prompt tells you that the virtualenv is active (and it remains active even while you're not in its directory):

	(my-first-virtualenv)daniele@v029:~/my-first-virtualenv$ python 

What's in the virtualenv?
-------------------------

::

	pip freeze # list installed items
	
Install a package
----------------- 

	pip install rsa
	
pip will visit PyPI, the Python Package Index, and will install Python-RSA (a
"Pure-Python RSA implementation"). It will also install its dependencies -
things it needs - if any have been listed at PyPI.

Now see what `pip freeze` reports. And try:

	(my-first-virtualenv)daniele@v029:~/my-first-virtualenv$ python 
	Python 2.7.2+ (default, Jul 20 2012, 22:15:08) 
	[GCC 4.6.1] on linux2
	Type "help", "copyright", "credits" or "license" for more information.
	>>> import rsa
	
Where packages get installed
----------------------------

Your virtualenv has a site-packages directory, in the same way your system does. So now rsa can be found in:

	~/my-first-virtualenv/lib/python2.7/site-packages/rsa 
	
Dependencies
------------

Python-RSA doesn't have any dependencies, but if it did, and if those
dependencies had dependencies, pip would install them all.

So if all the package authors have done a good job of informing PyPI about
their software's requirements, you can install a Django application, for
example, and pip will will install it and Django and possibly dozens of other
pieces of software, all into your virtualenv, and without your having to make
sure that everything required is in place.

Create a second virtualenv
--------------------------

::

	cd ~/ # it would be silly to create a virtualenv inside another
	virtualenv my-second-virtualenv
	source bin/activate # activate it, and deactivate the other one 

`pip freeze` will show you that you haven't installed Python-RSA in this one -
it's a completely different Python environment from the other, and both are
isolated from the system-wide Python setup.

Deactivate a virtualenv
-----------------------

	deactivate
	
Now you're no longer in any virtualenv.       

--install-site-packages
-----------------------

Sometimes you might want to have the Python packages already installed on your
system included in your new virtualenv. In that case:

	virtualenv --install-site-packages my-third-virtualenv 
	
remove a virtualenv
-------------------

virtualenvs are disposable. You can get rid of these:

    cd ~/
	rm -r  my-first-virtualenv my-second-virtualenv my-third-virtualenv
	
A virtualenv for the workshop
=============================

There's more to virtualenv, but that's all you need to get started
and to use it effectively. Now create a virtualenv for the workshop:

	virtualenv afraid-to-commit
	cd afraid-to-commit
	source bin/activate
	pip install django
	