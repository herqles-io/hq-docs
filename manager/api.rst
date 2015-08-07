Management APIs
===============

All Management APIs use token authentication and require :code:`X-Auth-Token` as a header parameter.
To get a token please reference the Users API.

Users
-----

Some APIs calls will be ignored depending on the identity and assignment driver that is in use.

.. http:put:: /user/token

   Request an API token.

   :json string username: the username to authenticate as
   :json string password: the password to use during authentication

   :>json string token: the authentication token
   :>json long expire_at: unix time in milliseconds when the token will expire

   :statuscode 200: successfully received an authentication token
   :statuscode 400: missing json parameters
   :statuscode 401: Invalid username or password
   :statuscode 404: User assignment does not exist

   **Example request**:

   .. sourcecode:: http

      PUT /user/token
      Content-Type: application/json

      {
        "username": "myuser",
        "password": "password123"
      }

   **Example response**:

   .. sourcecode:: http

     HTTP/1.1 OK

     {
       "token": "Ikd28lcjAj7qEC7rhFpX6ykhlf4gIElvVt5q0FS2WsQ",
       "expire_at": 14389774893
     }

.. http:post:: /user/add

   Add a new user.

   :json string username: the username for the user
   :json string password: the password for the user

   :reqheader X-Auth-Token: Authentication Token

   :>json boolean $username: will always be True
   :>json boolean identity: if the user identity was created
   :>json boolean assignment: if the user assignment was created

   :statuscode 200: successfully added a new user
   :statuscode 400: missing json parameters

   **Example request**:

   .. sourcecode:: http

      POST /usr/add
      Content-Type: application/json

      {
        "username": "myuser",
        "password": "password123"
      }

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK

      {
        "myuser": True,
        "identity": True,
        "assignment": True
      }

Workers
-------

Jobs
----

Tasks
-----