.. _preparing_repositories:

Preparing a repository for Binder
=================================

You can do this by making sure your repo contains:

* A collection of Jupyter Notebooks. These notebooks will be made available to
  users of your Binder.
* One (or many) text files that specify the requirements of your code. For
  example, a ``requirements.txt`` or ``environment.yml`` file. See the
  below examples for a list of supported files and environments.

Verify, and add if needed, the files specified above to the repository.
Once that's done, navigate to ``mybinder.org`` and insert the URL for
your git repository. Press ``Launch`` to automatically create your Binder.
The Binder service will be automatically send you to a live Jupyter session
connected to this repository.

.. note::

   If a previous version of the repository has already been built, Binder will
   only build a new one if the git hashes don't match. If Binder When Binder
   *doesn't* need to build a repository, the process of connecting to the live
   computational environment is much faster.


Simple Python dependencies
--------------------------

Many repositories already contain a ``requirements.txt`` specifying the
dependencies of that repository. For 'simple to install' dependencies, a
``requirements.txt`` should meet your needs. To generate a ``requirements.txt`` from
the environment you have locally use ``pip freeze > requirements.txt``. This
will list all packages you have installed, and can be a starting point for
constructing your ``requirements.txt``. We recommend you only list those
packages you really need to successfully build the repository.

Take a look at the `binder-examples/requirements <https://github.com/binder-examples/requirements>`_
repository to see an example.


Using conda packages
--------------------

For 'complex to install' packages, like ``numpy`` or ``scikit-learn``, we
recommend using the `conda package manager <https://conda.io/docs/index.html>`_.
To specify your dependencies create an ``environment.yml`` listing the packages
and versions required. For syntax help read `create an environment file manually <https://conda.io/docs/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually>`_
from the conda documentation.

Take a look at the `binder-examples/conda <https://github.com/binder-examples/conda>`_
repository to see an example.

.. note::

   Packages that require ``pip`` for installation can be specified in
   the ``environment.yml`` file.  We recommend this approach instead of having
   a ``requirements.txt`` and an ``environment.yml`` in the same repository.
   See `binder-examples/python-conda_pip <https://github.com/binder-examples/python-conda_pip>`_.


Using Python2
-------------

To use python 2.7 for your repository create a ``runtime.txt`` with
``python-2.7`` as only content. This will install a python2 environment in
addition to the default python environment. The contents of ``requirements.txt``
are installed into the python2 environment.

Take a look at the `binder-examples/python2_runtime <https://github.com/binder-examples/python2_runtime>`_
repository to see an example.

.. note::

   Make sure that you save your notebooks with a python2 kernel activated,
   as this defines which kernel Binder will use when a notebook is opened.
   The active kernel is displayed in the upper right corner of the notebook.

.. note::

   If you also wish to install dependencies into the python3 environment,
   include a file called ``requirements3.txt``. The packages inside it will be
   installed into the python3 environment.


Executing post-build commands
-----------------------------

You might need to run arbitrary commands at the end of the build process. Place
these in the ``postBuild`` file and make it executable. One use case is having
a repository that contains a Python package and examples that use the package.
In this case you can run ``python setup.py install`` from the ``postBuild``
file to avoid having to place your package in the ``requirements.txt``. It is
also useful for activating notebook extensions you installed via a
``requirements.txt`` directive earlier.

Take a look at the `binder-examples/jupyter-extension <https://github.com/binder-examples/jupyter-extension>`_
repository to see an example.
