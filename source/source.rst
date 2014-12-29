**************
Source Control
**************

.. index::
	single: Source Control; GitHub

.. _source_control_github:

GitHub
======

The HLU Tool source code is hosted by GitHub in the `HLUTool repository <https://github.com/HabitatFramework/HLUTool>`_. GitHub is a well known web-based hosting service for software development projects. It uses the **Git** Version Control System (VCS) which, like all version control systems, records changes to a file or set of files over time so that specific versions can be recalled later.

If you are signed in to GitHub you can **Fork** the repository to create your own local copy, or alternatively you can download a Zip copy of all the source files.


Branches
--------

There are two main `branches <https://github.com/HabitatFramework/HLUTool/branches>`_ in the HLUTool repository:

	* **master** : contains the source code for the ArcGIS/MapInfo variant of the tool
	* **master-mapinfo** : contains the source code for the MapInfo only variant of the tool


Commits
-------

There are numerous commits to both of the above branches each of which incrementally contributes towards one of the releases for each variant of the tool. Each commit has a short summary and a longer text description of the changes that it contains and lists the files that were added/deleted/amended. Details of the actual lines added/deleted can also be viewed on GitHub.

New commits relating to changes to the tool in the future should similarly provide a summary and description of the changes, and ideally changes should be split/grouped where possible so that each relates to a single change or fix. This helps to determine what changes were made for each change/fix in the event that they need to be amended or reverted.


Tags
----

The source code for every version of the tool from v1.0.1 to v2.3.0 is **Tagged** on GitHub. The `HLUTool Tags <https://github.com/HabitatFramework/HLUTool/tags>`_ point to a specific 'commit' in a branch to indicate that the commit relates to a released version of the tool.

	* tags **'v1.0.1'** thru **'v2.3.0'** denote versions relating to the ArcGIS/MapInfo variant *master* branch
	* tags **'v1.0.1m'** thru **'v2.3.0m'** denote versions relating to the MapInfo only variant *master-mapinfo* branch.


Releases
--------

In addition to the source code **tags**, each variant/version of the tool is listed under `HLUTool Releases <https://github.com/HabitatFramework/HLUTool/releases>`_. Each release relates to one of the above tags, but in addition contains a set of **Release Notes** together with a download link to a Zip copy of the source code and the Windows Installer **setup.exe** program for that version. Links to the release for each new version can be sent to users of the tool for them to install.


Collaborating
-------------

Currently there are two owners of the HLUTool repository on GitHub, only one of whom is a developer. There has therefore been no need to fork the repository or raise **Pull** requests. If, in the future, a new developer is to take over development/maintenance of the tool then the simplest solution is for them to also become an *owner* of the repository so that they have control over source. However, if there is a need to have more than one developer then it may be necessary to agree on a collaborative source control process. According to GitHub there are two popular models of collaborative development:

Fork & Pull
+++++++++++

The fork & pull model lets anyone fork an existing repository and push changes to their personal fork without requiring access be granted to the source repository. The changes must then be pulled into the source repository by the project maintainer (owner). This model reduces the amount of friction for new contributors and is popular with open source projects because it allows people to work independently without upfront coordination.

Shared repository model
+++++++++++++++++++++++

The shared repository model is more prevalent with small teams collaborating on projects. Everyone is granted push access to the central, shared repository and topic branches are used to isolate changes.

Pull requests are especially useful in the fork & pull model because they provide a way to notify project maintainers about changes in your fork. However, they're also useful in the shared repository model where they're used to initiate code review and general discussion about a set of changes before being merged into a mainline branch.


.. raw:: latex

	\newpage

.. index::
	single: Source Control; Helpful Links

.. _source_control_links:

Helpful Links
=============

For those unfamiliar with Git and GitHub the following links will provide some useful reading material to help explain what Git is and how to use GitHub.

The Git Parable
	Tom Preston-Warner, a co-founder of GitHub, wrote a long but very informative post `The Git Parable <http://tom.preston-werner.com/2009/05/19/the-git-parable.html>`_ on his blog that is really worth reading as an introduction to the origins and concepts of Git.

Pro Git
	Written by Scott Chacon, the entire open source book on learning and using Git is available to `read online for free <http://book.git-scm.com>`_ or to purchase as a book.

Scott Chacon blog
	Scott Chacon, a software developer at GitHub and author of **Pro Git**, wrote a few posts on his `blog <http://scottchacon.com/>`_ that might be useful, especially the last post `GitHub Flow <http://scottchacon.com/2011/08/31/github-flow.html>`_.

Git Reference
	This handy site is great as a `glossary reference <http://gitref.org/>`_ if you know how to use Git but are always forgetting the commands.

GitHub Guides
	A series of guides and videos for understanding and using GitHub are available at `GitHub Guides <https://guides.github.com/>`_.

