*****************
Developer's Guide
*****************

Preface
=======

What this guide covers
----------------------

Introduction
============

Essential Concepts
------------------

Minimum System Requirements
---------------------------

Microsoft Visual Studio 2012
Microsoft .Net Framework 3.5
ArcGIS 10.1 or later
MapInfo 8 or later
SQL Server Express
Microsoft Access
GitHub for Windows
Git for Windows
InstallShield Limited Edition



Skills Needed
-------------

General application development processes, such as issue management, debugging, testing, 
Visual Studio
C#
SQL
LINQ
ArcGIS
ArcObjects
MapInfo
MapBasic
General understanding of XML
Understanding of source code control techniques, especially Git and GitHub
Familiarity of MarkDown syntax and online documentation repositories such as ReadTheDocs


General Guidelines
------------------




Source Code Components
======================
If you are looking for more detailed information on the tool this part of the documentation is for you.




Get the latest code

Navigating the source code



Database Design
===============
If you want to understand the structure of the database used by the tool this part of the documentation is for you.



Installer
=========

InstallShield Limited Edition




Version Control
===============

GitHub


Helpful links
-------------

Git Parable (Tom Preston-Warner blog)
Pro Git (book and git-scm.com/book)
GitHub Flow (Scott Chacon blog)




Bug tracking
============

ALERC forum
GitHub repository issue tracker



Build Instructions
==================

Building The Installer
----------------------

Version Numbers

Product Code

Upgrade Path



Making The Release
------------------

GitHub Tags

Release Notes

Upload Executables

ReadMe Files



Build
1. Amend the HLUGISTool assembly version (appears in 'About' popup in user interface).
2. Amend the installer version
3. Amend the installer product key (and note in 'HLU Releases.txt')
4. Amend the installer Upgrade Paths 'Max Version' to the previous version number
5. Amend readme.txt, readme.rtf and readme.md
6. Create release notes - update version, release date, additions, changes, fixes, etc.

GitHub
1. Create new tags for releases
2. Push tags to GitHub
3. Add release notes to new tags
4. Attach setup.exe installer to release and publish the release

Releases
1. Minor release v1.0.3.0
2. Minor release v1.0.3.0 for MapInfo only


Documentation updates
=====================

GitHub

ReadTheDocs



Typical Development Process
===========================

	Select issue/change request to address
	Checkout source code from online repository
	Create source code branch
	Change source code
	Add comments to the source code to describe each new/amended assembly, class, method, property and section of code
	Add 'FIXED:', 'CHANGED:'' or 'FIX:' comments to the source code where appropriate
	Update source code Copyright statement (if applicable)
	Update AboutHLUTool Copyright statement (if applicable)
	Test and debug changes
	Update assembly version
	Build Installer
	Test Installer
	Merge source code branch
	Upload branch to online repository
	Create release tag and upload
	Create release notes and add to online release
	Repeat steps for MapInfo only version of tool
	Update issue/change request





Tools & Websites
================

Visual Studio
SQL Server Express
GitHub
GitHub for Windows
Git for Windows
ReadTheDocs
Sphinx
Active Python
Notepad 2-mod
Sublime


