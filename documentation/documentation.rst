.. index::
	single: Documentation

.. _documentation:

*************
Documentation
*************

There are three distinct guides that accompany the HLU Tool. All the guides are written using reStructuredText, their sources are stored on GitHub and they are available to view and download on ReadTheDocs.

**User Guide**

The user guide, available to view or download on ReadTheDocs at `HLUTool-UserGuide <https://readthedocs.org/projects/hlugistool-userguide>`_, is for those who will be regular users of the HLU Tool but are not concerned with how to install or configure the tool or how to perform database administration.

**Technical Guide**

The technical guide, available to view or download on ReadTheDocs at `HLUTool-TechnicalGuide <https://readthedocs.org/projects/hlutool-technicalguide>`_, is for those of a more ‘techie’ nature. It contains details of how to install, configure, maintain and upgrade the HLU Tool and use and maintain the associated relational database.

**Developer's Guide**

The developer's guide (this guide), available to view or download on ReadTheDocs at `HLUTool-DevelopersGuide <https://readthedocs.org/projects/hlutool-developersguide>`_, explains a little about how the HLU Tool source code is structured, what you may need to develop and support the tool and how to build and distribute it.


.. raw:: latex

	\newpage

.. index::
	single: Documentation; reStructuredText

.. _documentation_restructuredtext:

reStructuredText
================

What is it?
-----------

reStructuredText is is an easy-to-read, what-you-see-is-what-you-get plain text markup syntax. It is often used for in-line program documentation (such as Python docstrings), for quickly creating simple web pages, and for standalone documents (such as the HLU Tool guides).

reStructuredText can be written in any text editor, but some editors provide syntax highlighting and shortcuts to assist authors (see :ref:`requirements_tools` for some examples).

Further reading
---------------

For those unfamiliar with reStructuredText the following websites will provide some useful background reading material and references to help in authoring documents:

	* `Sphinx reStructuredText <http://sphinx-doc.org/rest.html>`_ - an introduction to reStructuredText concepts and syntax.
	* `Docutils <http://docutils.sourceforge.net/rst.html>`_ - a reference guide for reStructuredText markup syntax.


.. raw:: latex

	\newpage

.. index::
	single: Documentation; GitHub

.. _documentation_github:

GitHub
======

Source Control
--------------

The source code for the documentation is stored on GitHub with each guide in a separate repository. Source control for the guides works in the same way as for the tool itself using Git and GitHub for Windows (see :ref:`GitHub Source Control <source_control_github>`).

	.. tip::
		See `HabitatFramework <https://github.com/HabitatFramework>`_ for a list of *all* the repositories on GitHub relating to the tool.


One of the benefits of reStructuredText is that documents written using it are readable in their 'raw' markup format. So the source code files for the guides can be viewed and downloaded directly using GitHub. However, the intended purpose of the markup is the conversion of reStructuredText documents into more structured data formats; that's where ReadTheDocs comes in (see :ref:`documentation_rtd` below).

Webhooks
--------

The really clever trick is that once a change to a guide has been committed to GitHub, a **Webhook** notifies ReadTheDocs of the change. ReadTheDocs will then rebuild the documentation using the latest source of the documents.

.. note::
	Webhooks allow external services such as ReadTheDocs to be notified when certain events happen on GitHub. When the specified events happen, such as a commit, GitHub sends a `POST` request to each of the specified URLs. The target system can then pull in the latest source and perform an action, such as rebuilding the documentation.


.. raw:: latex

	\newpage

.. index::
	single: Documentation; ReadTheDocs

.. _documentation_rtd:

ReadTheDocs
===========

What is it?
-----------

`ReadTheDocs <https://readthedocs.org/>`_ is an online documentation repository for the open source community. It supports Sphinx docs written with reStructuredText. Sphinx is a documentation generator which converts reStructuredText files into HTML websites and other formats including PDF. ReadTheDocs automates the process of building and uploading Sphinx documentation. 

Building
--------

By using a GitHub *Webhook*, ReadTheDocs will be 'pinged' when the source has been updated. ReadTheDocs will then rebuild the documentation using the latest source documents.

When each ReadTheDocs project (each guide is a separate project) is built it automatically builds separate HTML and PDF formats of the documentation. This provides users with alternative methods of viewing the guides, each with its own strengths and weaknesses.

Versions
--------

ReadTheDocs supports multiple versions for each project, so for each release of the tool it can host a parallel release of each of the guides. To do this each guide would need to be updated (where appropriate) and then 'tagged' in GitHub (see :ref:`GitHub Source Control <source_control_github>`). ReadTheDocs will then build HTML and PDF formats of the guide for the new version and continue to host this latest version together with all previous versions.

	.. tip::
		Which versions are available to users on ReadTheDocs can be configured on the `Versions` page in the `Admin` section for each project (guide).

Further reading
---------------

The `ReadTheDocs documentation <https://docs.readthedocs.org/en/latest/index.html>`_ provides an introduction to those unfamiliar with ReadTheDocs features and explains the build process.

