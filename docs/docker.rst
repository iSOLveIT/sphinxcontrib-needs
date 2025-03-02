:orphan:

.. _docker:

Sphinx-Needs Docker Image
=========================

Status
------

=======================================  ====================
Image                                    Build Status   
=======================================  ====================
``danwos/sphinxneeds:latest``            |sphinxneeds-status|
``danwos/sphinxneeds-latexpdf:latest``   |sphinxneeds-status|
=======================================  ==================== 

.. |sphinxneeds-status| image:: https://github.com/useblocks/sphinxcontrib-needs/actions/workflows/docker.yaml/badge.svg
   :target: https://github.com/useblocks/sphinxcontrib-needs/actions/workflows/docker.yaml



Image Variants
--------------

The Sphinx-Needs docker images come in two flavors, each designed for a specific
use case. 

``sphinxneeds:<tag>``
~~~~~~~~~~~~~~~~~~~~~

This is the defacto image (size ~ 350MB). If you are unsure about what
your requirements are, you probably want to use this one. It is designed to be
used both as a throw away container (mount your documentation and start
the container), as well as the base to build your own images.

.. note::
   The image does not include latex packages and therefore does 
   not support PDF generation. Please use the latex-pdf version below for 
   such use cases.

Included Tools
^^^^^^^^^^^^^^

The image is based on the `sphinx
image <https://hub.docker.com/r/sphinxdoc/sphinx>`__ and includes the
following tools.

+------------------------+
| Tools                  |
+========================+
| python-slim            |
+------------------------+
| sphinx                 |
+------------------------+
| sphinxcontrib-needs    |
+------------------------+
| sphinxcontrib-plantuml |
+------------------------+
| graphviz               |
+------------------------+
| jre                    |
+------------------------+

``sphinxneeds-latexpdf:<tag>``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This image includes all the tools in the ``sphinxneeds:latest`` image
and additionally pdf generation tools. The image is ~ 1.5GB large.


Included Tools
^^^^^^^^^^^^^^

The image is based on the `sphinx latexpdf
image <https://hub.docker.com/r/sphinxdoc/sphinx-latexpdf>`__ and
includes the following tools.

+------------------------+
| Tools                  |
+========================+
| python-slim            |
+------------------------+
| sphinx                 |
+------------------------+
| sphinxcontrib-needs    |
+------------------------+
| sphinxcontrib-plantuml |
+------------------------+
| graphviz               |
+------------------------+
| jre                    |
+------------------------+
| latexmk                |
+------------------------+
| texlive                |
+------------------------+

Getting Started
---------------

Prerequisites
~~~~~~~~~~~~~

To use the images, install and configure `Docker <https://www.docker.com/>`__.


Pulling the Image from Docker Hub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The image can be pulled by

.. code:: bash

   docker pull danwos/sphinxneeds:latest

or

.. code:: bash

   docker pull danwos/sphinxneeds-latexpdf:latest

A specific version can be pulled with a version tag.

For example,

.. code:: bash

   docker pull danwos/sphinxneeds:0.7.8


Build The Image Locally
~~~~~~~~~~~~~~~~~~~~~~~

| To build the image locally, execute the following.

.. code:: bash

   cd docker && ./build_docker.sh
   
.. note::
   The script allows to choose between html and pdf version and
   the Sphinx-Needs version to be installed.

Usage
-----

Linux
~~~~~

.. code:: bash

   docker run --rm -it -v $(pwd):/sphinxneeds danwos/sphinxneeds:latest <build-command>

Windows (cmd)
~~~~~~~~~~~~~

.. code:: bash

   docker run --rm -it -v %cd%:/sphinxneeds danwos/sphinxneeds:latest <build-command>

Windows (Powershell)
~~~~~~~~~~~~~~~~~~~~

.. code:: bash

   docker run --rm -it -v ${PWD}:/sphinxneeds danwos/sphinxneeds:latest <build-command>

``<build-command>``\ s to be used are:

Generate HTML
~~~~~~~~~~~~~

.. code:: bash

       make html

For example,

.. code:: bash

   docker run --rm -it -v $(pwd):/sphinxneeds danwos/sphinxneeds:latest make html

Generate PDF
~~~~~~~~~~~~

.. code:: bash

       make latexpdf

.. note:: Make sure ``danwos/sphinxneeds-latexpdf:latest`` is installed for PDF generation.

To enter a shell, execute:

Linux
~~~~~

.. code:: bash

   docker run --rm -it -v $(pwd):/sphinxneeds danwos/sphinxneeds:latest bash


Windows (cmd)
~~~~~~~~~~~~~

.. code:: bash

   docker run --rm -it -v %cd%:/sphinxneeds danwos/sphinxneeds:latest bash


Windows (Powershell)
~~~~~~~~~~~~~~~~~~~~

.. code:: bash

   docker run --rm -it -v ${PWD}:/sphinxneeds danwos/sphinxneeds:latest bash

Once inside the docker container shell, execute a ``<build-command>``