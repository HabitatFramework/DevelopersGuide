****************
Database Updater
****************

.. index::
	single: Database Updater

In order to apply structural and data changes to the HLU tool database you will need to use the HLU Tool Database Updater **HLUDbUpdater.exe**. The HLU Tool Database Updater provides an automated mechanism of applying changes to a target HLU Tool relational database. It will process one or more script files and execute all the SQL commands in the files.


Components
==========

Within the Visual Studio solution for the HLU Database Updater there is a single project containing a single .NET assembly.


.. index::
	single: Assemblies; HLUDbUpdater

.. _assembly_hlugistool:

HLUDbUpdater
------------

This is the main assembly that contains all of the user interfaces, the 'business logic' and also handles the data connection with the chosen relational database. There are a few ad-hoc classes in the parent folder but the majority of the source code is structured in the same sub-folders as the main HLUGISTool project (see :ref:`assembly_hlugistool` for more details).

The majority of the user interfaces and supporting classes relate to connecting the updater to the required relational database. Most of these are exact copies of the same components used in the main tool assembly but a few have been adapted to provide additional functionality specific to the database updater. There is no interaction with GIS or the spatial data so the components relating to the ArcGIS and MapInfo applications used by the main tool assembly are not included.


.. _database_updater_source_code:

Source Control
==============

.. index::
	single: Source Control; Database Updater
	single: Database Updater; Source Control

GitHub
------

Like the main tool the source code for the database updater is open source and hosted by GitHub. It can be downloaded from `HLUDbUpdater repository <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater>`_.

Branches
	There are two main `branches <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/branches>`_ in the repository:

		* **master** : contains the source code for the database updater
		* **scripts** : contains all of the SQL scripts to be applied by the database updater

Tags
	The source code for every version of the database updater source code from v1.0.0 to v1.0.1 is **Tagged** on GitHub. The `HLUDbUpdater Tags <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/tags>`_ point to a specific 'commit' in a branch to indicate that the commit relates to a released version of the tool.

.. _database_updater_releases:

Releases
	In addition to the source code **tags** each release of the database updater is also listed under `HLUDbUpdater Releases <https://github.com/HabitatFramework/DatabaseUpdater/releases>`_. Each release relates to one of the above tags but in addition contains a set of **Release Notes** together with a download link to a Zip copy of the source code and the executable **HLUDbUpdater.exe** for that version.

.. _database_updater_scripts:

Scripts
	All of the latest scripts for the database updater can be downloaded from <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/archive/scripts.zip>.


.. raw:: latex

	\newpage

.. _database_updater_new_releases:

Building New Releases
=====================

Building the database updater for a new version/release is more straightforward than building the main tool. The database updater does not need to be installed in order to be executed and hence it does not require an installer. There are just a few steps to consider.


.. index::
	single: New Releases; Database Updater
	single: Database Updater; New Releases

Version Numbers
---------------

Assembly version
	The HLUDbUpdater assembly version, using the format *Major.Minor.Patch.Build*, should be incremented following `semantic versioning <http://semver.org/>`_ rules. So whether the increment relates to a major change, minor update or just a patch will depend on what is contained in the new release.

	* Major version numbers change whenever there is significant change to the look or functionality or for large or potentially backward-incompatible changes.
	* Minor version numbers change when a new minor feature is introduced, or when a set of smaller features are rolled out together.
	* Patch numbers change when a new build of the software is released containing small bug fixes.
	* Build numbers typically don't change as a new version is not usually released just for a new build.

	.. note::
		The database updater version number appears in the user interface title bar.

ReadMe file
-----------

The **ReadMe.txt** file must be amended to reflect the version number and copyright details of the new release, as well as any new features or changes to system requirements. The ReadMe file is a simple text (.txt) file which is distributed with the database updater executable **HLUDbUpdater.exe**.


Distribution
============

Like the main tool, the database updater is currently distributed via GitHub. There are a number of stages involved in distributing a new release.

GitHub Tags
-----------

Once the final commit has been applied for a new version then a new tag should be created in the local Git repository for the **master** branch. It is common practice to use tag names by prefixing the version number with the letter `v`. The tag descriptions also follow a set pattern by explicitly stating if it is a major, minor or patch release.

	Name: version number prefixed by 'v' (e.g. 'v1.0.1')
	Description: Major/Minor/Patch release version number (e.g. `Minor release v1.0.1`)

		.. note::
			To create the above tag example enter the following in a Git shell whilst the master branch is active::

				git tag -a v1.0.1 -m ‘Minor release v1.0.1’

Once the tags have been created in the local repository they should be pushed to the remote GitHub repository.

	.. note::
		To push new tags to GitHub enter the following in a Git shell window::

			git push --tags

.. note::
	The database updater **script** branch does not require tags as scripts do not necessarily relate to specific versions of the database updater or the main tool.

.. tip::
	Existing tags for the database updater can be viewed on GitHub under `HLUTool Tags <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/tags>`_.


Release Notes
-------------

Each new release of the database updater should be accompanied by its own set of release notes. Release notes are written using `GitHub Flavored Markdown <https://help.github.com/articles/github-flavored-markdown>`_ and should contain the following information as a minimum:

	* Version
	* Release date
	* System requirements
	* Execution Instructions
	* Additions
	* Removals
	* Changes
	* Fixes


Once the new tag for a release has been pushed to the GitHub repository then release notes can be added. To add release notes go to the list of `HLUDbUpdater Tags <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/tags>`_ and click **Add release notes** against the required tag.


.. tip::
	Existing release for the database updater can be viewed on GitHub under `HLUTool Releases <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/releases>`_.


Upload Executables
------------------

Finally, once a new release has been created on GitHub the **HLUDbUpdater.exe** executable and associated files (e.g. ReadMe.txt, Licence.txt and .dlls) can be uploaded. This provides an effective way of distributing the database updater and ensures that it is stored alongside the relevant release notes and source code for each release.

.. note::
	To attach the executable and associated files to a release combine them all into a single **.zip** file, edit the release on GitHub and then 'drag and drop' the .zip file on the *Attach binaries by dropping them here* area.


.. index::
	single: Database Updater; Scripts

Scripts
=======

The scripts processed by the database updater contain one or more SQL statements designed to update the structure and/or contents of an HLU Tool relational database. Each script file must adopt the following rules in order to be valid and be processed by the database updater program.

File Names
----------

Script files (e.g. '**0000B.sql**') must be named sequentially using **Base36** (e.g. 0 to 9 then A to Z, 10 to 19 then 1A to 1Z, etc.). If a script file is found that has already been processed then it will be skipped and moved to the **Archive** sub-folder. If a script file is **missing** from the Base36 sequence then an error will appear and processing will stop.

SQL Commands
------------

Each SQL command must meet the following rules:

	* Each SQL command must fit on a single line - multi-line commands will be split at line ends
	* Comments are delimited using the prefix/suffix **/\*** and **\/** (e.g. '/* Delete the existing exports_fields row. */')
	* String values are delimited by single quotes **''** (e.g. 'INSERT INTO [exports] (export_id, export_name) VALUES (1, \'All attribute fields\')')
	* Database table names are delimited by square brackets **[]** (e.g. 'DELETE * FROM [exports]')
	* **INSERT** commands must explicitly include the **INTO** keyword (e.g. 'INSERT INTO [lut_user] ...')

	.. note::
		* Single quotes within strings are not currently supported (e.g. 'White's House')
		* Double quotes within strings are not currently supported (e.g. 'White House "North"')


Specific Connection Type Directives
-----------------------------------

Specific connection types or databases can be targeted by specifying the required connection types/database in a comma-delimited list within square brackets **[]** on a separate line, e.g. **[Access,SqlServer,PostGreSql,Oracle]**. These directives are required when the structure or keywords of a SQL command are different between connection types or databases - for example *Access* uses the function 'UCASE' to convert strings to upper case whereas *SQLServer*, *Oracle* and *PostgreSQL* use the function *UPPER*.

Once a connection type directive has been specified in a script **all** subsequent SQL commands in the script will **only** be applied if the **actual** connection type or database established by the user is found in the comma-delimited list **until** either:

	* Another specific connection type directive is encountered
	* The connection type is reset using the **[All]** or **[Any]** directive


Special Commands
----------------

Scripts can contain a number of **special** commands unique to the database updater:

Set Ignore_Errors
	Set *On* to ignore any errors in subsequent SQL commands (i.e. '**Set Ignore_Errors On**')
	Set *Off* to immediately stop a script if any errors occur processing subsequent SQL commands (i.e. '**Set Ignore_Errors Off**')

Set Timeout
	To override the default timeout specify the number of seconds before a database timeout will occur when processing a single SQL command (e.g. '**Set timeout 120**')
	To reset the default timeout specify '**Set timeout default**' or '**Set timeout**'

Set Display_Results
	Set *On* to display the results of any subsequent SQL commands (i.e. '**Set display_results on**')
	Set *Off* to hide the results of all subsequent SQL commands (i.e. '**Set display_results off**')

Set Skip_Version_Update
	Set *On* to skip updating the database version in the **lut_version** table (i.e. '**Set skip_version_update on**')
	Set *Off* to ensure the database version in the lut_version table is updated (as default) (i.e. '**Set skip_version_update off**')

