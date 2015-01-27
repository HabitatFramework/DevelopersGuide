*******
Preface
*******

The most up to date version of this documentation can be found in **html** and **PDF** form on `ReadTheDocs <https://readthedocs.org/projects/hlutool-developersguide/>`_.

What this guide covers
======================

This guide explains a little about how the HLU Tool source code is structured, what you may need to develop and support it, how to build and distribute it, and how to maintain the associated online guides.

:doc:`../requirements/requirements` summarises the applications, websites, tools, skills & experience that a developer may need.

:doc:`../components/components` outlines the major components of the tool's source code.

:doc:`../source/source` introduces the basics of the GitHub version control repository where the source code is hosted.

:doc:`../coding/coding` proposes some general guidelines for coding standards, metadata and comments when making code changes.

:doc:`../installer/installer` summarises the features and configuration options that are used for creating an installer for the tool.

:doc:`../releases/releases` lists the steps to follow when building the tool and distributing a new release.

:doc:`../registration/registration` describes how and why the tool is registered as an ArcGIS extension.

:doc:`../documentation/documentation` gives an overview of the associated online guides and how to maintain them. 

:doc:`../issues/issues` introduces the online forum and issue log where problems and enhancements can be proposed and discussed.

:doc:`../appendix/appendix` contains a copy of the GNU Free Documentation License v1.3 covering this guide.


.. index::
	single: Licensing

Open Source Licensing
=====================

The code for the HLU Tool is 'open source' and is released under `GNU General Public License (GPL) v3 <http://www.gnu.org/licenses/gpl.html>`_. Users are free to install it on as many computers as they like, and to redistribute it according to the GPLv3 license.

This guide is released under `GNU Free Documentation License (FDL) v1.3 <http://www.gnu.org/licenses/fdl.html>`_. Permission is granted to copy, distribute and/or modify this document under the terms of the license.

These licenses are designed to guarantee the user's freedom to share and change the software and documentation under the terms of the licenses (but note that no additional restrictions may be applied to any new products resulting from changes to the HLU Tool or associated documentation).

Please remember, however, that the tool cost a lot of money to develop and still requires further development and ongoing support. Hence any contributions towards costs would be gratefully received. Enquiries can be made via the `ALERC forum <http://forum.lrcs.org.uk/viewforum.php?id=24>`_.


.. index::
	single: Quick Links

Quick links
===========

The following are links to some of the websites relevant to the use, support and development of the tool:

* `ALERC Forum <http://forum.lrcs.org.uk/viewforum.php?id=24>`_ - Announcements, bug reports, user Q&A and feature discussions.
* `Releases <https://github.com/HabitatFramework/HLUTool/releases>`_ - Release notes and installers for ArcGIS and MapInfo systems.
* `Source Code <https://github.com/HabitatFramework>`_ - Repositories for the source code of the tool and associated online guides.
* `Issue Log <https://github.com/HabitatFramework/HLUTool/issues>`_ - Known issues and existing change requests.
* `User Guide <https://readthedocs.org/projects/hlugistool-userguide/>`_ - Online guide for users of the tool.
* `Technical Guide <https://readthedocs.org/projects/hlutool-technicalguide/>`_ - Online guide for administrators and technical users.
* `Developer's Guide <https://readthedocs.org/projects/hlutool-developersguide/>`_ - Online guide for developers (this guide).


.. index::
	single: Acknowledgements

Acknowledgements
================

Many thanks are due to all the LRCs in the south-east of England and their staff who have, and continue to, fund and support the development of the HLU Tool. It takes a small army of developers, testers and users to build a truly useful tool (especially users who care enough to test new releases, report bugs and discuss feature requests).


Conventions used in this manual
===============================

The following typographical conventions are used in this manual:

:kbd:`Ctrl-A`
	Indicates a key, or combination of keys, to press.

:guilabel:`Commit`
	Indicates a label, button or anything that appears in user interfaces.

**Tools... --> About**
	Indicates a menu choice, or a combination of menu choices, tab selections or GUI buttons.

:file:`C:\\Program Files\\HLU Tool`
	Indicates a filename or directory name.

.. tip::
	Tips can help save time or provide shortcuts.

.. note::
	Notes explain things in more detail or highlight important points.

.. caution::
	Warnings where developers should pay attention.

