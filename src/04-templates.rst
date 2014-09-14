.. _templates:

Templates
=========

`Templates` are a cool way to customize your quicktexts by using template variables. 
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

    Hello {{to.0.firstname}},

When using the `quicktext` above it will generate the following result::

    Hello Jane,


Now, let's break down the template above:

 1. '{{' means that the template started
 2. 'to' - is actually the "To" field in the e-mail. So if you have say: 
     Jane Doe <jane@doe.org> in the 'to' variable correspond with Jane's address.
 3. '.0' means that we only refer to the first address. So if we have multiple
     addresses in the 'To' field then we refer only to the first one and not the
     rest of them.
 4. '.firstname' meas that given the first to address insert only the 
     'firstname' in the template. We could have said 'name' - would've include the full name.
 2.  '}}' end of template.

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


What is behind all this?
--------------------------

The power of the templates is given by the `Handlebars <http://handlebarsjs.com/>`_
template library.


