.. _templates:

Templates
=========

`Templates` are the primary block of the Gorgias Google Chrome extension.

One distinction compared to the :ref:`alternatives` is that it supports custom variables
that are replaced on template execution.

The simplest example can be summarized as follows:

When you write an e-mail to someone it's usually a good idea to address that
person by name, this removes ambiguity if the e-mail has multiple recipients
and is also a good sign that you took the time to address somebody with a
greeting. It's good etiquette!

So imagine that you want to address Jane Doe by typing::

    Hello Jane,

    And then the rest of the e-mail follows...


Now make it easier to write the 'Hello Jane' part you can simply create a
template and use the template variables.
The following goes into the body of the quicktext::

    Hello {{to.0.first_name}},

When using the `template` above it will generate the following result::

    Hello Jane,


Now, let's break down the template above:

 1. '{{' marks the start of the template variable.
 2. 'to' - refers to the "To" field in the e-mail. So if you have say:
     Jane Doe <jane@doe.org> in the 'to' variable correspond with Jane's address.
 3. '.0' means that we only refer to the first address. So if we have multiple
     addresses in the 'To' field then we refer only to the first one and not the
     rest of them.
 4. '.first_name' referst to the first to address insert only the
     'first_name' in the template. We could have said 'name' - would've include the full name.
 2.  '}}' marks end of template variable.

So once again, if we have 'Jane Doe <jane@doe.org>' in the `To` field then the
resulting template will look like this::

    Hello Jane,


Other examples
----------------

::

    'Hello {{ to[0].name }}' => 'Hello Jane Doe'
    'The subject: {{ subject }}' => 'The subject: e-mails subject'
    'You can e-mail me at: {{ from.email }}' => 'You can e-mail me at: email@example.org'


You can also do more complicated stuff like for loop iteration::

    Hello {{#each to}}
        - Name {{name}}
        - First name {{first_name}}
        - Last name {{last_name}}
        - Email {{email}}
    {{/each}}


Which given multiple addresses in the `To` field will result in this rendering::


    Hello
        - Name Jane Doe
        - First name Jane
        - Last name Doe,
        - Email jane@doe.org

.. note:: If the variable value is missing (Ex: no First Name for the contact) the variable is replace with an empty string.

Complete list of available variables
------------------------------------

As you know by now the `To` and `From` fields are a list and `0` is the index of the first item in that list.

* `To` field
    * {{to.0.email}}
    * {{to.0.name}}
    * {{to.0.last_name}}
    * {{to.0.first_name}}

* `From` field
    * {{from.0.email}}
    * {{from.0.name}}
    * {{from.0.last_name}}
    * {{from.0.first_name}}

* `CC` field
    * {{cc.0.email}}
    * {{cc.0.name}}
    * {{cc.0.last_name}}
    * {{cc.0.first_name}}
* `BCC` field
    * {{bcc.0.email}}
    * {{bcc.0.name}}
    * {{bcc.0.last_name}}
    * {{bcc.0.first_name}}

* {{subject}} - subject content of the message


What is behind all this?
------------------------

The power of the templates is given by the `Handlebars <http://handlebarsjs.com/>`_
template library.


