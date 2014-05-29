
*********
Installer
*********

.. index::
	single: Installer

Since v1.0.1 of the HLU Tool *InstallShield Limited Edition* has been used to build the Windows Installer for deploying the tool on other systems. InstallShield Limited Edition is a free version of *Flexera’s InstallShield* included within Visual Studio 2010 and later that replaces the functionality previously provided by the Visual Studio Installer Setup Projects. It contains a wide range of features and options for configuring how a Windows application will be installed, many of which are not needed for installing the tool.

Below is a summary of the InstallShield Limited Edition features and configuration options that are used for creating a Windows installer for the tool. There are no complex settings used to build a Windows installer for the HLU Tool. In fact, the only 'advanced' requirement when installing the ArcGIS/MapInfo variant of the tool is the need to register the *HluArcMapExtension.dll* assembly as an ArcMap Desktop extension. This is not 'directly' achieved by the installer setup.exe application, but instead is achieved 'indirectly' using an *Installer Class* assembly.

.. seealso::
	See :doc:`../components/components` for details of the ArcObjectsInstaller component and how the ArcMap Extension is registered when building the tool assemblies in Visual Studio and installing the tool.


Organize Your Setup
===================

General Information
-------------------

This tab contains general information about the tool that appears when viewing the properties of the tool once installed and when viewing the list of installed programs in the control panel.  More importantly it also contains the product version, product code and upgrade code and the destination installation path.

Upgrade Paths
-------------

This tab allows the developer to control which previously versions of the tool can be upgraded using this version of the tool. During installation the Windows Installer searches the target system for the specified upgrade code. If found, and the other upgrade properties are met, the target system is upgraded by installing the new version. If the upgrade code is not found on the target system then this version of the tool will be installed as new.

The *ISPreventDowngrade* is also enabled to prevent the current version of the tool from overwriting later (future) versions of the tool. If users want to install an older version of the tool once a newer version has been installed then the newer version will first need to be manually uninstalled.


Specify Application Data
========================

Files
-----

This tab is used to specify which files are to be included in the install which folders they will be copied to the target system. The files specified include:

	* The **primary output** files created during the build process (.dll and .exe files).
	* Any **.dll** files referenced by the tool and not ordinarily available on a target system.
	* An **icon** for the tool.
	* A **ReadMe.txt** file giving an overview of the tool, it's features and where more information can be found.
	* A **Licence.txt** file containing details of the GNU General Public License under which the tool is released.
	* An empty MapInfo workspace **Empty.wor** used to open MapInfo when first launching the tool.


Configure the Target System
===========================

Shortcuts/Folders
-----------------

This tab offers a method of designing shortcuts and program folders for the tool. Currently only two shortcuts are created on the target system's Programs menu:

	* **HLU GIS Tool - Launch** : This shortcut starts the tool without any optional arguments (normal operation)
	* **HLU GIS Tool - Reconfigure** : This shortcut starts the tool with the optional '/c' argument which triggers the tool to clear any existing configuration settings and re-run the initial configuration steps.


Customize the Setup Appearance
==============================

Dialogs
-------

This tab allows the dialog pages of the tool's setup steps to be customised. Developer's can configure various features such as which setup dialogs appear, what images and options appear on the dialogs and if the tool is automatically launched after installation.


Define Setup Requirements and Actions
=====================================

Requirements
------------

This tab is where you can configure software conditions that must be met on a target system in order for the installation setup for the tool to run. Currently there are only two conditions set:

	* **.NET 3.5 SP1 is installed** : Microsoft .NET Framework 3.5 Service Pack 1 (or later) must be installed on the target system.
	* **REALVERSION** : A custom condition that ensures that ArcGIS 10.1 or later is installed on the target system by checking the existence of a 'RealVersion' registry value under the registry key 'SOFTWARE\\ESRI\\ArcGIS' in the 'HKLM' registry root. This is a custom condition that was created using the *System Search Wizard*.

.. note::
	This custom condition is only included in the ArcGIS/MapInfo variant of the tool as a simple mechanism to ensure it is not installed on a MapInfo only target system in error.


To Create a Setup File
======================

To create a setup.exe file you need to build the HluSetup_ISLE project using the configuration option 'SingleImage'.
