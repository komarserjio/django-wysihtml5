Django-wysihtml5
================

|TravisCI|_

.. |TravisCI| image:: https://secure.travis-ci.org/danirus/django-wysihtml5.png?branch=master
.. _TravisCI: https://travis-ci.org/danirus/django-wysihtml5


By Daniel Rus Morales <http://danir.us/>

* http://pypi.python.org/pypi/django-wysihtml5/
* http://github.com/danirus/django-wysihtml5/

Simple Django app that provides a Wysihtml5 rich text editor textarea widget.

Includes a **demo project** and a **test suite**. If you commit code, please consider adding proper coverage (especially if it has a chance for a regression) in the test suite.

Run the tests with:  ``python setup.py test``


Quick start
===========

1. Add ``wysihtml5`` to ``INSTALLED_APPS`` in your settings module.
2. Create a model with a field of type ``Wysihtml5TextField``.
3. Create an admin class for that model by inheriting from both ``wysihtml5.admin.AdminWysihtml5TextFieldMixin`` and Django's ``admin.ModelAdmin``.
4. Hit your app's admin URL and see the `wysihtml5 <https://github.com/xing/wysihtml5>`_ editor in action.


Demo site
=========

1. Cd into the demo directory: ``cd django-wysihtml5/example/demo``
2. Run syncdb with --no-input: ``python manage.py syncdb --noinput`` (user: admin, pwd: admin)
3. Run the dev web server: ``python manage.py runserver``
4. Hit the demo URL: `http://localhost:8000 <http://localhost:8000>`_ to see the example article fully formatted with Wysihtml5.
5. Hit the demo admin URL: `http://localhost:8000/admin/ <http://localhost:8000/admin/>`_ to see the widget in action.


Customization
=============

Two settings allow you to customize the editor:

 * WYSIHTML5_EDITOR -> editor's parameters customization
 * WYSIHTML5_TOOLBAR -> editor's commands and toolbar customization


WYSIHTML5_EDITOR setting
------------------------

Customize the Wysihtml5 Editor parameters, as in `here <https://github.com/xing/wysihtml5/wiki/Configuration>`_, by defining ``WYSIHTML5_EDITOR`` in your settings file. ``WYSIHTML5_EDITOR`` is a dictionary that defaults to::

    EDITOR_CONF = {
        # Give the editor a name, the name will also be set as class 
        # name on the iframe and on the iframe's body
        'name': 'null',
        # Whether the editor should look like the textarea (by adopting styles)
        'style': 'true',
        # Id of the toolbar element, pass falsey value if you don't want 
        # any toolbar logic
        'toolbar': 'null',
    	# Whether urls, entered by the user should automatically become 
        # clickable-links
        'autoLink': 'true',
        # Object which includes parser rules (set this to 
        # examples/rules/spec.json or your own spec, otherwise only span 
        # tags are allowed!)
        'parserRules': 'wysihtml5ParserRules',
        # Parser method to use when the user inserts content via copy & paste
        'parser': 'wysihtml5.dom.parse || Prototype.K',
        # Class name which should be set on the contentEditable element in 
        # the created sandbox iframe, can be styled via the 'stylesheets' option
        'composerClassName': '"wysihtml5-editor"',
        # Class name to add to the body when the wysihtml5 editor is supported
        'bodyClassName': '"wysihtml5-supported"',
        # By default wysihtml5 will insert <br> for line breaks, set this to
        # false to use <p>
        'useLineBreaks': 'true',
        # Array (or single string) of stylesheet urls to be loaded in the 
        # editor's iframe
        'stylesheets': '["%s"]' % (settings.STATIC_URL + 
                                   "wysihtml5/css/stylesheet.css"),
        # Placeholder text to use, defaults to the placeholder attribute 
        # on the textarea element
        'placeholderText': 'null',
        # Whether the composer should allow the user to manually resize 
        # images, tables etc.
        'allowObjectResizing': 'true',
        # Whether the rich text editor should be rendered on touch devices 
        # (wysihtml5 >= 0.3.0 comes with basic support for iOS 5)
        'supportTouchDevices': 'true'
    }


WYSIHTML5_TOOLBAR setting
-------------------------

You can customize Wysihtml5 commands configuration by defining ``WYSIHTML5_TOOLBAR`` in your settings file. ``WYSIHTML5_TOOLBAR`` is a dictionary that defaults to::

    WYSIHTML5_TOOLBAR = {
        "formatBlockHeader": { 
            "active": True,
            "command_name": "formatBlock",
            "render_icon": "wysihtml5.widgets.render_formatBlockHeader_icon"
        },
        "formatBlockParagraph": { 
            "active": True,
            "command_name": "formatBlock",
            "render_icon": "wysihtml5.widgets.render_formatBlockParagraph_icon"
        },
        "bold": { 
            "active": True,
            "command_name": "bold",
            "render_icon": "wysihtml5.widgets.render_bold_icon"
       },
        "italic": { 
            "active": True,
            "command_name": "italic",
            "render_icon": "wysihtml5.widgets.render_italic_icon"
        },
        "underline": { 
            "active": True,
            "command_name": "underline",
            "render_icon": "wysihtml5.widgets.render_underline_icon"
        },
        "justifyLeft": { 
            "active": True,
            "command_name": "justifyLeft",
            "render_icon": "wysihtml5.widgets.render_justifyLeft_icon"
        },
        "justifyCenter": { 
            "active": True,
            "command_name": "justifyCenter",
            "render_icon": "wysihtml5.widgets.render_justifyCenter_icon"
        },
        "justifyRight": { 
            "active": True,
            "command_name": "justifyRight",
            "render_icon": "wysihtml5.widgets.render_justifyRight_icon"
        },
        "insertOrderedList": { 
            "active": True,
            "command_name": "insertOrderedList",
            "render_icon": "wysihtml5.widgets.render_insertOrderedList_icon"
        },
        "insertUnorderedList": { 
            "active": True,
            "command_name": "insertUnorderedList",
            "render_icon": "wysihtml5.widgets.render_insertUnorderedList_icon"
        },
        "insertImage": { 
            "active": True,
            "command_name": "insertImage",
            "render_icon": "wysihtml5.widgets.render_insertImage_icon",
            "render_dialog": "wysihtml5.widgets.render_insertImage_dialog"
        },
        "createLink": { 
            "active": True,
            "command_name": "createLink",
            "render_icon": "wysihtml5.widgets.render_createLink_icon",
            "render_dialog": "wysihtml5.widgets.render_createLink_dialog"
        },
        "insertHTML": { 
            "active": True,
            "command_name": "insertHTML",
            "command_value": "<blockquote>quote</blockquote>",
            "render_icon": "wysihtml5.widgets.render_insertHTML_icon"
        },
        "foreColor": { 
            "active": True,
            "command_name": "foreColor",
            "render_icon": "wysihtml5.widgets.render_foreColor_icon"
        },
        "changeView": { 
            "active": True,
            "command_name": "change_view",
            "render_icon": "wysihtml5.widgets.render_changeView_icon"
        },
    }

Two of the commands allow dialog customization too:

* `Create Link <https://github.com/xing/wysihtml5/wiki/Supported-Commands#wiki-createLink>`_
* `Insert Image <https://github.com/xing/wysihtml5/wiki/Supported-Commands#wiki-insertImage>`_

Customize commands by declaring them in the ``WYSIHTML5_TOOLBAR`` dictionary. You can:

* Disable commands by setting ``"active": False``.
* Redefine a command name to provide your own Wysihtml5 command implementation. Change the setting ``"command_name": "yourNewCommand"``, and write your function command in JavaScript. See link to an example below.
* Render your own command icons by writing a ``render_icon`` function. 
* Render your own widget dialogs for ``createLink`` and ``insertImage``.

Only declare your customized commands and attributes, django-wysihtml5 will use the default settings for the rest.

Look at the specific `demo_wysihtml5 <https://github.com/danirus/django-inline-media/tree/master/example/demo_wysihtml5>`_ site in `django-inline-media <https://github.com/danirus/django-inline-media>`_. It provides a customize ``insertImage`` command.  

Have questions?
---------------

* On Wysihtml5: `go here <https://github.com/xing/wysihtml5>`_
* On this app: `post a comment <http://danir.us/projects/django-wysihtml5-10>`_

Go and make happy your users!
