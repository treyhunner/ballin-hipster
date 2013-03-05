Undocumented Forms
==================

Changing forms dynamically
--------------------------

After calling ``__init__`` on the ``super`` form object, ``self.fields`` will
contain a dictionary of the form's fields.  Below are some ways these fields
might be modified.

Delete a field
~~~~~~~~~~~~~~

Deleting a field from ``self.fields`` will remove the field from the form.

Example of overridding ``UserChangeForm`` to use emails instead of usernames:

.. code-block:: pycon

    from django.contrib.auth.forms import UserChangeForm


    class EmailUserChangeForm(UserChangeForm):
        email = forms.EmailField(max_length=80)

        def __init__(self, *args, **kwargs):
            super(EmailUserChangeForm, self).__init__(*args, **kwargs)
            del self.fields['username']

        class Meta:
            model = User
