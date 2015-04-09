# Ontic
Satellite 6 entities mapping and random data generation

An entity is a class that maps fields and is capable of generate random data
for each field.

For example an entity which maps an user should look like the following:

    class User(Entity):
        name = StringField()
        supervisor = OneToOneField('User')
        subordinate = OneToManyField('User')

The methods available are:

* `get_fields`: returns all fiels defined on the entity class
* `get_values`: returns the value of each field on the current entity object

Any logic needed to process the data and create on server should be added by a
higher layer, for example, a CLI client can grab the data (entity) and use it
to create a new user:

    user = User(name='Foo')
    cli_client.create(user)  # this will store the created id on the entity

In the previous example just the name field was provided, the others will be
random generated. The generation will be just the data and not the entity on
the server as this is just the data layer.
