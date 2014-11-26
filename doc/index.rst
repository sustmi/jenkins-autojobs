Jenkins-autojobs
================

.. image:: img/explanation-figure.png
   :align: center
   :width: 680

Introduction
------------

*Jenkins-autojobs* is a set of scripts for automatically creating
Jenkins jobs from template jobs and the branches in an SCM repository.
*Jenkins-autojobs* supports git_, mercurial_ and subversion_.

A routine run performs the following actions:

- Reads settings from a :ref:`yaml configuration <gityamlconfig>` file.
- Lists branches/refs from SCM.
- Creates or updates jobs as dictated by the configuration file.

In its most basic form, the configuration file specifies:

- How to access Jenkins and the SCM repository.
- Which branches to process and which to ignore.
- Which template job to use for which branches.
- How new jobs should be named.


Features
--------

- If a template job is updated, all "derived" jobs will also be
  updated the next time *jenkins-autojobs* runs.

- Set the enabled/disabled state of new jobs. A new job can inherit
  the state of its template job, but an updated job can keep its most
  recent state.

- Perform text substitutions throughout all text elements of a job's
  ``config.xml``. This is useful for plugins that cannot introspect
  the name of the current branch or job (e.g. `Sidebar-Link`_).

- Add new jobs to a Jenkins view.

- Remove jobs that were created with *jenkins-autojobs* for which a
  branch no longer exist in the repository.


Installation
------------

The latest stable version of *jenkins-autojobs* can be installed from
pypi_.

.. code-block:: bash

    $ pip install jenkins-autojobs

*Jenkins-autojobs* depends on a version of lxml with support for XML
canonicalization (c14n). Setup will attempt to install one if it is
not present on your system - in this case you also have to install the
``libxml`` and ``libxslt`` development headers:

.. code-block:: bash

    $ apt-get install libxml2-dev libxslt1-dev # on a Debian compatible OS
    $ yum install libxml2-devel libxslt-devel  # on a Redhat compatible OS
    $ pacman -S libxslt libxml2                # on Arch Linux and derivatives



Usage
-----

All scripts accept the same command-line options and arguments::

    Usage: jenkins-makejobs-* [-rvdtjnyoupUYOP] <config.yaml>

    General Options:
      -n dry run
      -v show version and exit
      -d debug config inheritance
      -t debug http requests

    Repository Options:
      -r <arg> repository url
      -y <arg> scm username
      -o <arg> scm password
      -Y scm username (read from stdin)
      -O scm password (read from stdin)

    Jenkins Options:
      -j <arg> jenkins url
      -u <arg> jenkins username
      -p <arg> jenkins password
      -U jenkins username (read from stdin)
      -P jenkins password (read from stdin)

===============  =============================
 SCM             Script Name
===============  =============================
 git_            ``jenkins-makejobs-git``
 subversion_     ``jenkins-makejobs-svn``
 mercurial_      ``jenkins-makejobs-hg``
===============  =============================

Work in progress.


Configuration
-------------

.. toctree::
   :maxdepth: 2

   git
   subversion
   mercurial


Changes
-------

.. toctree::

   :maxdepth: 2
   changelog


Similar Projects
----------------

* jenkins-build-per-branch_
* jenkins-job-builder_


License
-------

*Jenkins-autojobs* is released under the terms of the `Revised BSD
License`_. The *jenkins-autojobs* logo is released under the `CC BY-SA
3.0`_ license.


.. _github:            https://github.com/gvalkov/jenkins-autojobs
.. _`Revised BSD License`: https://raw.github.com/gvalkov/jenkins-autojobs/master/LICENSE
.. _lxml:              http://lxml.de/
.. _`Sidebar-Link`:    https://wiki.jenkins-ci.org/display/JENKINS/Sidebar-Link+Plugin
.. _python-jenkins:    http://pypi.python.org/pypi/python-jenkins
.. _jenkins-build-per-branch: http://entagen.github.com/jenkins-build-per-branch/
.. _jenkins-job-builder: https://pypi.python.org/pypi/jenkins-job-builder/
.. _git:               https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin
.. _subversion:        https://wiki.jenkins-ci.org/display/JENKINS/Subversion+Plugin
.. _mercurial:         https://wiki.jenkins-ci.org/display/JENKINS/Mercurial+Plugin
.. _pypi:              http://pypi.python.org/pypi/jenkins-autojobs
.. _`CC BY-SA 3.0`:    http://creativecommons.org/licenses/by-sa/3.0/
