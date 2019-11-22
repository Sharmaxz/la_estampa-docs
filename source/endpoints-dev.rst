Authenticating Requests
-----------------------

The `Print` endpoints requires authentication.

PLEASE WRITE ME


------------------------

Category
------------------------

The category is a way to filter and sort the `Tag`_.

.. list-table:: **Attributes**
   :widths: 15 15 15
   :header-rows: 1

   * - field
     - type
     - required
   * - id
     - integer
     - false
   * - name
     - string
     - true



GET
===

If you want to get all category, use:

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/category/

**Response:**

.. code-block:: bash

    [
        {
            "id": 1,
            "name": "category 1"
        },
        {
            "id": 2,
            "name": "category 2"
        }
        ...
    ]

But if you prefer to take one category. Replace the <id> for the value that you want.

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/category/<id>

**Response:**

.. code-block:: bash

    {
        "id": 1,
        "name": "category"
    }


POST
====

You need to do post request with the category name in the body to create a new category.

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/category/

body:

.. code-block:: bash

    {
        "name" : "category"
    }


**Response:**

.. code-block:: bash

    {
        "id": 1,
        "name": "category"
    }

PUT
===

Choose the category that you want to update and replace the <id> to category ID and add all the attributes in the body.

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/category/<id>

body:

.. code-block:: bash

    {
        "name" : "category"
    }


**Response:**

.. code-block:: bash

    {
        "id": 1,
        "name": "category"
    }

P.S: The response will contains the new values.

PATCH
=====

Choose the category that you want to partial update and replace the <id> to category ID and add all the attributes in the body.

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/category/<id>

body:

.. code-block:: bash

    {
        "name" : "category"
    }

**Response:**

.. code-block:: bash

    [
        {
            "id": 1,
            "name": "category"
        }
    ]

P.S: The response will contains the new values.

------------------------

Collection
------------------------

The collection is a `Print`_ group, with the name suggests is a `Print`_ collection.



.. list-table:: **Attributes**
   :widths: 15 15 15
   :header-rows: 1

   * - field
     - type
     - required

   * - id
     - integer
     - false

   * - date_creation
     - datetime
     - true

   * - date_update
     - datetime
     - false

   * - briefing
     - string
     - false


   * - ps
     - string
     - false

GET
===

If you want to get all collection, use:

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/collection/

POST
====

You need to do post request with the collection attributes in the body to create a new collection.

.. code-block:: bash

    https://la-estampa.herokuapp.com/api/collection/

body:

.. code-block:: bash

    {
    }


**Response:**

.. code-block:: bash

    {
        "id": 1,
    }



------------------------

Print
------------------------


GET
===



.. code-block:: bash

    https://la-estampa.herokuapp.com/api/mywork/






POST
====


.. code-block:: bash

    https://la-estampa.herokuapp.com/api/mywork/

.. list-table:: **POST**
   :widths: 20 15 15
   :header-rows: 1

   * - field
     - type
     - required
   * - id
     - integer
     - false
   * - code
     - string
     - true
   * - exclusivity
     - string
     - true
   * - status
     - string
     - false
   * - type
     - string
     - false
   * - date_creation
     - datetime
     - true
   * - date_update
     - datetime
     - false
   * - image
     -
     - true
   * - psd_original
     -
     - true
   * - psd_final
     -
     - false
   * - psd_flirted
     -
     - false
   * - briefing
     - Briefing
     - false

Filter user posts by category

.. code-block:: bash

    'https://viunge.herokuapp.com/v1/post/(?category=[0-9]+)'



Tag
------------------------


------------------------

Report
------------------------

Report a video post as Inappropriate Content or Offensive Material for staff review

.. code-block:: bash

    'https://viunge.herokuapp.com/v1/report/'


.. list-table:: **POST**
   :widths: 20 15 15
   :header-rows: 1

   * - field
     - type
     - required
   * - id
     - integer
     - false
   * - reviewed
     - INC (Inappropriate Content or Offensive Material) or SAF (Considered Safe)
     - false
   * - video_id
     - integer
     - true


Generate Presigned Post for AWS S3 Bucket
-----------------------------------------

.. code-block:: bash

    'https://viunge.herokuapp.com/v1/generate_presigned_url/(?file_name=[a-z0-9]+)'

Response:

.. code-block:: bash

    {
        "post": {
            "url": "https://s3-eu-west-1.amazonaws.com/viunge-be-videos-in",
            "fields": {
                "key": "file_name.mov",
                "x-amz-algorithm": "AWS4-HMAC-SHA256",
                "x-amz-credential": "",
                "x-amz-date": "",
                "policy": "",
                "x-amz-signature": ""
            }
        }
    }

Social Login Endpoints
----------------------


These endpoints provides account creation, and access token creation.

Convert Token
=============

Use this endpoint to convert a token from Facebook or Instagram
to an access token for a ViUnge user.
This access token is then used to authenticate the user on the other
endpoints.

If the user is not registered on ViUnge, an account is created for him.


.. code-block:: bash

    POST 'https://viunge.herokuapp.com/v1/auth/convert-token/'

    {
      client_id: <client_id>,
      client_secret: <client_secret>,
      grant_type: convert_token,
      backend: <provider>,
      token: <social_token>
    }

`cliend_id` and `client_secret` are the credentials of the client application.
This is provided by the backend.

`provider` can be 'facebook' or 'instagram'.

`token` is the access token returned by the facebook or instagram social login sdk.



Response:

.. code-block:: bash

    {
        access_token: <hash_string>,
        expires_in: 36000,
        token_type: "Bearer",
        score: "read write",
        refresh_token: <hash_string>,
    }

Invalidate Sessions
===================

Use this endpoint to invalidate all sessions of an user.

.. code-block:: bash

    POST 'https://viunge.herokuapp.com/v1/auth/invalidate-sessions/'
    Authorization: Bearer <token>

    {
      client_id: <client_id>
    }

The response is an empty json object, with HTTP status code 204.