************
New Releases
************

.. _new_releases:

Building the Tool
=================

When building the tool for a new version/release, rather than for just testing or debugging changes in progress, there are a number of steps to follow or dependencies to consider.


.. index::
	single: New Releases; Version Numbers

.. _building_version_numbers:

Version Numbers
---------------

Assembly version
++++++++++++++++

The HLUGISTool assembly version, using the format *Major.Minor.Patch.Build*, should be incremented following `semantic versioning <http://semver.org/>`_ rules. So whether the increment relates to a major change, minor update or just a patch will depend on what is contained in the new release.

	* Major version numbers change whenever there is significant change to the look or functionality or for large or potentially backward-incompatible changes.
	* Minor version numbers change when a new minor feature is introduced, or when a set of smaller features are rolled out together.
	* Patch numbers change when a new build of the software is released containing small bug fixes.
	* Build numbers typically don't change as a new version is not usually released just for a new build.

.. note::
	The assembly version number appears in the 'About' pop-up window on user interface.

Product version
+++++++++++++++

The product version in the installer project properties should also be changed to match the assembly version number.

.. note::
	The installer product version number is used when installing the tool to ensure an older version of the tool doesn't overwrite a later version. The version number also appears in the Control Panel *Programs and Features* list.


.. index::
	single: New Releases; Product Code

.. _building_product_code:

Product Code
------------

The installer **Product Code** should be changed to uniquely identify this version if the product. The Windows installer uses the product code at run time to determine whether the same version of the product has already been installed.

.. note::
	To create a new GUID that uniquely identifies a new version of the product or click the `Generate a new GUID button` ({...}) in the Product Code setting in the General Information tab of the InstallShield project.

A note of all previously used Product Codes is maintained in 'Releases and Product Codes.txt' in the source code repository on GitHub.


.. index::
	single: New Releases; Upgrading

.. _building_upgrade_from:

Upgrading
---------

The installer `Upgrade From` **Max Version** must reflect the version number of the most recent release so that the Windows installer will find and upgrade **all** previous of the tool.


.. index::
	single: New Releases; ReadMe Files

.. _building_readme_files:

ReadMe files
------------

The ReadMe file must be amended to reflect the version number and copyright details of the new release, as well as any new features or changes to system requirements. The ReadMe file is maintained in three different formats; simple text (.txt), rich text (.rtf) and markdown (.md). Each format is used in different circumstances:

	* **ReadMe.txt** - Installed with the tool on the target system.
	* **ReadMe.rtf** - Displayed during the installation process.
	* **ReadMe.md** - Displayed in the source code repository by GitHub.


.. raw:: latex

	\newpage

.. index::
	single: Releasing

.. _releasing:

Distributing the Release
========================

The tool is currently distributed via GitHub. There are a number of stages involved in distributing a new release of the tool.

.. index::
	single: New Releases; Tags

.. _releasing_tags:

GitHub Tags
-----------

Once the final commit has been applied for the new version then new tags should be created in the local Git repository for each branch/variant of the tool. It is common practice to use tag names by prefixing the version number with the letter `v`. For the tool tag descriptions also follow a set pattern by explicitly stating if it is a major, minor or patch release.

**ArcGIS/MapInfo variant**
Name: version number prefixed by 'v' (e.g. 'v1.0.8')
Description: Major/Minor/Patch release version number for ArcGIS/MapInfo (e.g. `Minor release v1.0.8 for ArcGIS/MapInfo`)

	.. note::
		To create the above tag example enter the following in a Git shell whilst the master branch is active::

			git tag -a v1.0.8 -m ‘Minor release v1.0.8 for ArcGIS/MapInfo’

**MapInfo variant**
Name: version number prefixed by 'v' and suffixed by 'm' (e.g. 'v1.0.8m')
Description: Major/Minor/Patch release version number for MapInfo only (e.g. `Minor release v1.0.8 for MapInfo only`)

	.. note::
		To create the above tag example enter the following in a Git shell window whilst the master-mapinfo branch is active::

			git tag -a v1.0.8m -m ‘Minor release v1.0.8 for Mapinfo only’


Once the tags have been created in the local repository they should be pushed to the remote GitHub repository.

	.. note::
		To push new tags to GitHub enter the following in a Git shell window::

			git push --tags


.. tip::
	Existing tags for the tool can be viewed on GitHub under `HLUTool Tags <https://github.com/HabitatFramework/HLUTool/tags>`_.


.. index::
	single: New Releases; Release Notes

.. _releasing_release_notes:

Release Notes
-------------

Each new version/variant of the tool should be accompanied by its own set of release notes. Release notes are written using `GitHub Flavored Markdown <https://help.github.com/articles/github-flavored-markdown>`_ and should contain the following information as a minimum:

	* Version
	* Release date
	* System requirements
	* Installation Instructions
	* Additions
	* Removals
	* Changes
	* Fixes


Once the new tags for each branch/variant have been pushed to the GitHub repository then release notes can be added. To add release notes go to the list of `HLUTool Tags <https://github.com/HabitatFramework/HLUTool/tags>`_ and click **Add release notes** against the required tag.


.. tip::
	Existing release for the tool can be viewed on GitHub under `HLUTool Releases <https://github.com/HabitatFramework/HLUTool/releases>`_.


.. index::
	single: New Releases; Executables

.. _releasing_executables:

Upload Executables
------------------

Finally, once each new release has been created on GitHub the associated installer setup.exe executable can be uploaded. This provides an effective way of distributing the tool and ensures that the installer is stored alongside the relevant release notes and source code for each version/variant.

.. note::
	To attach the **setup.exe** installer to a release, edit the release on GitHub and then 'drag and drop' the file on the *Attach binaries by dropping them here* area.

