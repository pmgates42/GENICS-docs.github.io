Setting Up Environment
======================

Introduction
------------

This section provides step-by-step instructions on how to set up your environment for working with our project.
The GENICS project is a node.js, react, and next.js application. It uses MongoDB as a database.
The following sections will walk you through setting up your environment for working with the project.

Node Package Manager
----------------------

Our project uses [Node Package Manager](https://www.npmjs.com/) to manage dependencies.

The latest version should work, but make sure you use a version greater than 14.0.0

Verify that the installation was successful by running the following command in your terminal:

.. code-block:: bash

    npm -v


Run the command below to install the dependencies for the project.

.. code-block:: bash

    cd genics-app
    npm install

You may receive an error at this point:
    
.. code-block:: bash

    npm ERR! code ERESOLVE
    npm ERR! ERESOLVE could not resolve
    npm ERR! 
    npm ERR! While resolving: @next-auth/mongodb-adapter@1.1.1
    npm ERR! Found: mongodb@5.0.0
    npm ERR! node_modules/mongodb
    npm ERR!   mongodb@"^5.0.0" from the root project

At this point, try running through yarn instead:

.. code-block:: bash

    npm install -g yarn
    yarn install


If you do not have yarn installed, you can install it with the following command:

.. code-block:: bash

    npm install -g yarn




Setup Database Config
----------------------

Create a new file `genics-app/.env.local` This file contains the database configuration.

.. code-block:: bash

    NEXT_PUBLIC_MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.yj5ul.mongodb.net/GDB
    MONGODB_USER=<username>
    MONGODB_PASSWORD=<password>

*Get the username and password from the "database admin"*

Next, create the auth secret. NEXTAUTH_SECRET is an environment variable used in Next.js applications with NextAuth.js
for securing and encrypting session data and tokens. You will need openssl installed on your machine.

.. code-block:: bash

    openssl -v                  # Check if openssl is installed
    cd genics-app
    openssl rand -base64 32     # Generate the secret

Update the secret in genics-app/.env.local

.. code-block:: bash

    NEXT_PUBLIC_MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.yj5ul.mongodb.net/GDB
    MONGODB_USER=<username>
    MONGODB_PASSWORD=<password>
    NEXTAUTH_SECRET=<generated-secret>

Run The Server Locally
-------------------------

Run using yarn:

.. code-block:: bash

    cd genics-app
    yarn dev

Run using npm:

.. code-block:: bash

    cd genics-app
    npm run dev

If everything works correctly, you should see the following output:

.. code-block:: bash

    $ next dev
    - info Loaded env from /Users/paulgates/Documents/GitHub/Untitled/SER401-GENICS/genics-app/.env.local
    - ready started server on [::]:3000, url: http://localhost:3000
    - event compiled client and server successfully in 343 ms (18 modules)
    - wait compiling...
    - event compiled client and server successfully in 345 ms (18 modules)
    - info Loaded env from /Users/paulgates/Documents/GitHub/Untitled/SER401-GENICS/genics-app/.env.local
    - info Loaded env from /Users/paulgates/Documents/GitHub/Untitled/SER401-GENICS/genics-app/.env.local

open :ref: `localhost:3000<http://localhost:3000>` in your browser to view the app. Select an account for login.

Currently, the only account that is registered is:

john-doe@example.com
1234