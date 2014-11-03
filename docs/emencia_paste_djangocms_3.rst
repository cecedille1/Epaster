.. _intro_emencia_paste_djangocms_3:
.. _buildout: http://www.buildout.org/
.. _virtualenv: http://www.virtualenv.org/
.. _pip: http://www.pip-installer.org
.. _Foundation 3: http://foundation.zurb.com/old-docs/f3/
.. _Foundation: http://foundation.zurb.com/
.. _Foundation Orbit: http://foundation.zurb.com/orbit.php
.. _modular-scale: https://github.com/scottkellum/modular-scale
.. _Compass: http://compass-style.org/
.. _SCSS: http://sass-lang.com/
.. _rvm: http://rvm.io/
.. _Django: https://www.djangoproject.com/
.. _django-admin-tools: https://bitbucket.org/izi/django-admin-tools/
.. _Django CMS: https://www.django-cms.org/
.. _django-assets: https://github.com/miracle2k/django-assets/
.. _django-debug-toolbar: https://github.com/django-debug-toolbar/django-debug-toolbar/
.. _Django Blog Zinnia: https://github.com/Fantomas42/django-blog-zinnia
.. _Django CKEditor: https://github.com/divio/djangocms-text-ckeditor/
.. _Django Filebrowser: https://github.com/wardi/django-filebrowser-no-grappelli
.. _django-google-tools: https://pypi.python.org/pypi/django-google-tools
.. _Django Porticus: https://github.com/emencia/porticus
.. _Django PDB: https://github.com/tomchristie/django-pdb
.. _Django flatpages app: https://docs.djangoproject.com/en/1.5/ref/contrib/flatpages/
.. _Django sites app: https://docs.djangoproject.com/en/1.5/ref/contrib/sites/
.. _Django reCaptcha: https://github.com/praekelt/django-recaptcha
.. _Django registration: https://github.com/macropin/django-registration
.. _CKEditor: http://ckeditor.com/
.. _emencia-cms-snippet: https://github.com/emencia/emencia-cms-snippet
.. _Service reCaptcha: http://www.google.com/recaptcha
.. _Django Codemirror: https://github.com/sveetch/djangocodemirror
.. _django-crispy-forms: https://github.com/maraujop/django-crispy-forms
.. _crispy-forms-foundation: https://github.com/sveetch/crispy-forms-foundation
.. _emencia-django-slideshows: https://github.com/emencia/emencia-django-slideshows
.. _emencia-django-staticpages: https://github.com/emencia/emencia-django-staticpages
.. _emencia-django-socialaggregator: https://github.com/emencia/emencia-django-socialaggregator
.. _django-urls-map: https://github.com/sveetch/django-urls-map
.. _Sitemap framework: https://docs.djangoproject.com/en/1.5/ref/contrib/sitemaps/
.. _djangocms-admin-style: https://github.com/divio/djangocms-admin-style
.. _django-admin-shortcuts: https://github.com/alesdotio/django-admin-shortcuts/

*******************
DjangoCMS 3.x paste
*******************

DjangoCMS projects are created with the many components that are available for use. These components are called **mods** and these mods are already installed and ready to use, but they are not all enabled. You can enable or disable them, as needed.

It is always preferable to use the mods system to install new apps. You should never install a new app with `pip`_. If you plan to integrate it into the project, always use the `buildout`_ system. Just open and edit the ``buildout.cfg`` file to add the new egg to be installed. For more details, read the `buildout`_ documentation.

Links
=====

* Download his `PyPi package <https://pypi.python.org/pypi/emencia_paste_djangocms_3>`_;
* Clone it on his `Github repository <https://github.com/emencia/emencia_paste_djangocms_3>`_;

Paste
=====

This paste will appear with the name ``djangocms-3`` in the paster templates list (with the ``paster create --list-templates`` command).

To use this paste to create a new project you will do something like : ::

    paster create -t djangocms-3 myproject

Django
======

django-instance
---------------

This is the command installed to replace the ``manage.py`` script in Django. ``django-instance`` is aware of the installed eggs.

Paste template version
----------------------

In your projects, you can find from which Paste template they have been builded in the 'project/__init__.py' file where you should find the used package name and its version.

Note that previously (before the Epaster version 1.8), this file was containing the Epaster version, not the Paste template one, since the package didn't exists yet.

How the Mods work
-----------------

The advantage of centralizing app configurations in their mods is the project's ``settings.py`` and ``urls.py`` are gathered together in its configuration (cache, smtp, paths, BDD access, etc.). Furthermore, it is easier to enable or disable the apps.

To create a new mods, create a directory in ``$PROJECT/mods_avalaible/`` that contains at least one empty ``__init__.py`` and a ``settings.py`` to build the app in the project and potentially its settings. The `settings.py`` and ``urls.py`` files in this directory will be executed automatically by the project (the system loads them after the project ones so that a mods can overwrite the project's initial settings and urls). N.B. With Django's ``runserver`` command, a change to these files does not reload the project instance; you need to relaunch it yourself manually.

To enable a new mods, you need to create its symbolic link (**a relative path**) in ``$PROJECT/mods_enabled``. To disable it, simply delete the symbolic link.

Compass
=======

`Compass`_ is a **Ruby** tool used to compile `SCSS`_ sources in **CSS**.

By default, a Django project has its `SCSS`_ sources in the ``compass/scss/`` directory. The CSS `Foundation`_ framework is used as the database.

A recent install of Ruby and Compass is required first for this purpose (see `RVM`_ if your system installation is not up to date).

Once installed, you can then compile the sources on demand. Simply go to the ``compass/`` directory and launch this command: ::

    compass compile

When you are working uninterruptedly on the sources, you can simply launch the following command: ::

    compass watch

`Compass`_ will monitor the directory of sources and recompile the modified sources automatically.

By default the ``compass/config.rb`` configuration file (the equivalent of `settings.py`` in Django) is used. If needed, you can create another one and specify it to `Compass`_ in its command (for more details, see the documentation).

Foundation
----------

This project embeds `Foundation`_ 5 sources installed from the `Foundation`_ app so you can update it from the sources if needed (and if you have installed the Foundation cli, see its documentation for more details). If you update it, you need to synchronize the updated sources in the project's static files using a command in the Makefile: ::

    make syncf5
    
**You only have to do this when you want to synchronize the project's Foundation sources from the latest Foundation release. Commonly this is reserved for Epaster developers.**

This will update the Javascript sources in the static files, but make sure that it cleans the directory first. Never put your files in the ``project/webapp_statics/js/foundation5`` directory or they will be deleted. Be aware that the sources update will give you some file prefixed with a dot like ``.gitignore``, you must rename all of them like this ``+dot+gitignore``, yep the dot character have to be renamed to ``+dot+``, else it will cause troubles with GIT and Epaster. There is a python script named ``fix_dotted_filename.py`` in the source directory, use it to automatically apply this renaming.

For the `Foundation`_ SCSS sources, no action is required; they are imported directly into the compass config.

The project also embeds `Foundation 3`_ sources (they are used for some components in Django administration) but you don't have to worry about them.

RVM
---

`rvm`_ is somewhat like what `virtualenv`_ is to Python: a virtual environment. The difference is that it is intended for the parallel installation of a number of different versions of **Ruby** without mixing the gems (the **Ruby** application packages). In our scenario, it allows you to install a recent version of **Ruby** without affecting your system installation.

This is not required, just an usefull cheat to know when developing on a server with an old distribution.

Installation and initial use
============================

Once your project has been created with this epaster template, you need to install it to use it. The process is simple. Do it in your project directory: ::

    make install

When it's finished, active the virtual environment: ::

    source bin/active

You can then use the project on the development server: ::

    django-instance runserver 0.0.0.0:8001

.. note::
        ``0.0.0.0`` is some sort of alias that mean "bind this server on my ip", so if your local ip is "192.168.0.42", the server will be reachable in your browser with the url ``http://192.168.0.42:8001/``.

.. note::
        Note the ``:8001`` that mean "bind the server on this port", this is a required part when you specify an IP. Commonly you can't bind on the port 80 so allways prefer to use a port starting from *8001*.

.. note::
        If you don't know your local IP, you can use ``127.0.0.1`` that is an internal alias to mean "my own network card", but this IP cannot be reached from other computers (because they have also this alias linked to their own network card).

The first required action is the creation of a CMS page for the home page and also you should fill-in the site's name and its domain under ``Administration > Sites > Sites > Add site``.

Available mods
==============

accounts
--------

Enable `Django registration`_ and everything you need to allow users to request registration and to connect/disconnect. The views and forms are added so this part can be used. 

It includes:

* A view for the login and one for the logout;
* All the views for the registration request (request, confirmation, etc.);
* A view to ask for the reinitialization of a password.

In the ``skeleton.html`` template, a partial HTML code is commented. Uncomment it to display the *logout* button when the user is connected.

The registration process consists in sending an email (to be configured in the settings) with the registration request to an administrator responsible for accepting them (or not). Once validated, an email is sent to the user to confirm his registration by way of a link. Once this step has been completed, the user can connect.

Also, note that this app use a dummy profile model linked to User object. This profile is dummy because it implement fields for sample but you may not need all of them or you can even may not need about a Profile model, the User object could be enough for your needs. So before to use the syncdb, be sure to watch for the model to change it, then apply your changes to ``forms.RegistrationFormAccounts``, ``views.RegistrationView`` and eventually templates.

admin_style
-----------

Enable `djangocms-admin-style`_ to enhance the administration interface. Also enable `django-admin-shortcuts`_.

*admin-style* better fit with DjangoCMS than `admin_tools`_. 

.. warning::
        This mod cannot live with `admin_tools`_, you have to choose only one of them.

admin_tools
-----------

Enable `django-admin-tools`_ to enhance the administration interface. This enables three widgets to customize certain elements. `filebrowser`_ is used, so if your project has not enabled it, you need to remove the occurrences of these widgets.

.. warning::
        This mod cannot live with `admin_style`_, you have to choose only one of them.

assets
------

Enable `django-assets`_ to combine and minify your *assets* (CSS, JS). The minification library used, *yuicompressor*, requires the installation of Java (the OpenJDK installed by default on most Linux systems is sufficient).

In general, this component is required. If you do not intend to use it, you will need to modify the project's default templates to remove all of its occurrences.

ckeditor
--------

Enable and define customization for the `CKEditor`_ editor. It is enabled by default and used by `Django CKEditor`_ in the `cms`_ mod, and also in `zinnia`_.

Note that DjangoCMS use it's own app named "djangocms_text_ckeditor", a djangocms plugin to use CKEditor (4.x).

But Zinnia use "django_ckeditor" that ship the same ckeditor but without cms addons.

This mod contains configuration for all of them.

And some contained patches/fixes :

* the codemirror plugin that is not included in any of the apps;
* A system to use the "template" plugin (see views.EditorTemplatesListView for more usage details);
* Some overriding to have content preview and editor more near to Foundation;

cms
---

`Django CMS`_ allows for the creation and management of the content pages that constitute your site's tree structure. By default, this component enables the use of `filebrowser`_, `Django CKEditor`_ and `emencia-cms-snippet`_ (a clone of the snippets' plugin with a few improvements).

By default it is configured to use only one language. See its ``urls.py`` to find out how to enable the management of multiple languages.

codemirror
----------

Enable `Django Codemirror`_ to apply the editor with syntax highlighting in your forms (or other content).

It is used by the snippet's CMS plugin.

contact_form
------------

A simple contact form that is more of a standard template than a full-blown application. You can modify it according to your requirements in its ``apps/contact_form/`` directory. Its HTML rendering is managed by `crispy_forms`_ based on a customized layout.

By default, it uses the `recaptcha`_ mods.

crispy_forms
------------

Enable the use of `django-crispy-forms`_ and `crispy-forms-foundation`_. **crispy_forms** is used to manage the HTML rendering of the forms in a finer and easier fashion than with the simple Django form API. **crispy-forms-foundation** is a supplement to implement the rendering with the structure (tags, styles, etc.) used in `Foundation`_.

debug_toolbar
-------------

Add `django-debug-toolbar`_ to your project to insert a tab on all of your project's HTML pages, which will allow you to track the information on each page, such as the template generation path, the  query arguments received, the number of SQL queries submitted, etc.

This component can only be used in a development or integration environment and is always disabled during production.

Note that its use extends the response time of your pages and can provokes some bugs (see the warning at end) so for the time being, this mods is disabled. Enable it locally for your needs but never commit its enabled mod and remember trying to disable it when you have a strange bug.

.. warning::
        Never enable this mod before the first database install or a syncdb, else it will result in errors about some table that don't exist (like "django_site").

emencia_utils
-------------

Group together some common and various utilities from ``project.utils``.

filebrowser
-----------

Add `Django Filebrowser`_ to your project so you can use a centralized interface to manage the uploaded files to be used with other components (`cms`_, `zinnia`_, etc.).

The version used is a special version called *no grappelli* that can be used outside of the *django-grapelli* environment.

Filebrowser manage files with a nice interface to centralize them and also manage image resizing versions (original, small, medium, etc..), you can edit these versions or add new ones in the settings.

.. note::
        Don't try to use other resizing app like sorl-thumbnails or easy-thumbnails, they will not work with Image fields managed with Filebrowser.

flatpages
---------

Enable the use of `Django flatpages app`_ in your project. Once it has been enabled, go to the ``urls.py`` in this mod to configure the *map* of the urls to be used.

google_tools
------------

Add `django-google-tools`_ to your project to manage the tags for *Google Analytics* and *Google Site Verification* from the site administration location.

.. note::
        The project is filled with a custom template ``project/templates/googletools/analytics_code.html`` to use Google Universal Analytics, remove it to return to the old Google Analytics.

pdb
---

Add `Django PDB`_ to your project for more precise debugging with breakpoints. 

N.B. Neither ``django_pdb`` nor ``pdb`` are installed by the buildout. You must install 
them manually, for example with `pip`_, in your development environment so you do not 
disrupt the installation of projects being integrated or in production. You must also 
add the required breakpoints yourself.

See the the django-pdb Readme for more usage details.

.. note::
        django-pdb should be put at the end of settings.INSTALLED_APPS :
        
        "Make sure to put django_pdb after any conflicting apps in INSTALLED_APPS so 
        that they have priority."
        
        So with the automatic loading system for the mods, you should enable it with a 
        name like "zpdb", to assure that it is loaded at the end of the loading loop.

porticus
--------

Add `Django Porticus`_ to your project to manage file galleries.

recaptcha
---------

Enable the `Django reCaptcha`_ module to integrate a field of the *captcha* type via the `Service reCaptcha`_. This integration uses a special template and CSS to make it *responsive*.

If you do in fact use this module, go to its mods setting file (or that of your environment) to fill in the public key and the private key to be used to transmit the data required.

By default, these keys are filled in with a *fake* value and the captcha's form field therefore sends back a silent error (a message is inserted into the form without creating a Python *Exception*).

site_metas
----------

Enable a module in ``settings.TEMPLATE_CONTEXT_PROCESSORS`` to show a few variables linked to `Django sites app`_ in the context of the project views template.

Common context available variables are:

* ``SITE.name``: Current *Site* entry name;
* ``SITE.domain``: Current *Site* entry domain;
* ``SITE.web_url``: The Current *Site* entry domain prefixed with the http protocol like ``http://mydomain.com``. If HTTPS is enabled 'https' will be used instead of 'http';

Some projects can change this to add some other variables, you can see for them in ``project.utils.context_processors.get_site_metas``.

sitemap
-------

This mod use the Django's `Sitemap framework`_ to publish the ``sitemap.xml`` for various apps. The default config contains ressources for DjangoCMS, Zinnia, staticpages, contact form and Porticus but only ressource for DjangoCMS is enabled.

Uncomment ressources or add new app ressources for your needs (see the Django documentation for more details).

slideshows
----------

Enable the `emencia-django-slideshows`_ app to manage slide animations (slider, carousel, etc.). This was initially provided for `Foundation Orbit` and *Royal Slider*, but can be used with other libraries if needed.

socialaggregator
----------------

Enable the `emencia-django-socialaggregator`_ app to manage social contents.

.. note::
        This app require some API key settings to be filled to work correctly.

staticpages
-----------

This mod uses `emencia-django-staticpages`_ to use static pages with a direct to template process, it replace the deprecated mod *prototype*.

urlsmap
-------

`django-urls-map`_ is a tiny Django app to embed a simple management command that will display the url map of your project.

zinnia
------

`Django Blog Zinnia`_ allows for the management of a blog in your project. It is well integrated into the `cms`_ component but can also be used independently.
