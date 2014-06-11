**********
Components
**********

Within the Visual Studio solution for the HLU Tool there are six projects. Five of these projects are .NET assemblies that relate to various aspects of the tool functionality. The other project is an InstallShield project used to create a Windows Installer for the tool.

The following sections contain a brief description of each of the projects and their contents.


.. index::
	single: Assemblies

.. _assemblies:

Assembly Projects
=================

.. index::
	single: Assemblies; HLUGISTool

.. _assembly_hlugistool:

HLUGISTool
----------

This is the main assembly that contains all of the user interfaces, the 'business logic' and also handles the data connection with the chosen relational database. There are a few ad-hoc classes in the parent folder but the majority of the source code is structured in the following sub-folders.

Converters
	There are four converter classes in this folder that are used by the user interfaces and related classes to convert data values to/from more user-friendly visible values.

Data
	There are a number of data classes in this folder that support connections between the tool and different relational database systems, including ODBC, Oracle, PostGres, SQL Server and MS Access. The recommended connection methods are SQL Server and Access, and it is not known how much testing has been done using the other connection methods.

Date
	This folder contains a vague date class (VagueDate) that handles formatting and validation of the database date values to/from a user-friendly 'vague' format.

GISApplication
	This folder contains the central business logic classes, including the main class (GisApp) that is an abstract class for all the core tool functionality.

	This folder contains two sub-folders **MapInfo** and **ArcGIS** that inherit the GisApp abstract class and override it will all the GIS application specific functionality.

		.. note::
			The **ArcGIS** sub-folder is only used in the combined ArcGIS/MapInfo variant of the tool.

Icons
	This folder contains all the icons and button images that appear on the user-interfaces.

UI
	This folder contains all the user interface related source code in three sub-folders:

		* **UserControls** contains bespoke classes used by one or more of the user interfaces.
		* **View** contains the source code for user interface presentation. The user interfaces were developed using Windows Presentation Framework (WPF) and consists of a main interface (WindowsMain) and nine other sub-interfaces.
		* **ViewModel** contains the business logic associated with each of the user interfaces.


.. index::
	single: Assemblies; HluArcMapExtension

.. _assembly_hluarcmapextension:

HluArcMapExtension
------------------

This assembly is an ArcGIS Desktop Extension that provides the interface between the main HLUGISTool assembly and ArcGIS. It consists of a main class **HluArcMapExtension** that performs the editing and geoprocessing commands (e.g. select features, update attributes, split/merge features, zoom to features) requested by the main assembly.

This extension also passes back any information requested by the main assembly (e.g. list valid HLU feature layers, query selected features, is editing active). Commands and requests are passed between the main assembly and this assembly using Named Pipes. See :ref:`named_pipes` for more details.

The assembly must be registered as an ArcGIS Desktop Extension before it can interface with ArcGIS. See :ref:`esri_registration` for more details.


.. note::
	This assembly is only used in the combined ArcGIS/MapInfo variant of the tool.


.. index::
	single: Assemblies; InterProcessComm

.. _assembly_interprocesscomm:

AppModule.InterProcessComm
--------------------------

This assembly contains just the Named Pipes interfaces plus the logic for exception handling and the connection state for inter-process communication.

There are three interfaces defined within this assembly - **IChannelManager**, **IClientChannel** and **IInterProcessConnection**. These interfaces are introduced in order to abstract the Named Pipes implementation from clients involved in the IPC.


.. note::
	This assembly is only used in the combined ArcGIS/MapInfo variant of the tool.


.. index::
	single: Assemblies; Named Pipes

.. _assembly_namedpipes:

AppModule.NamedPipes
--------------------

This assembly contains all the .NET Named Pipes classes used by the HLU Tool. It is referenced by both the HLUGISTool **'client'** assembly and the HLUArcMapExtension **'server'** assembly for inter-process communication.

Outlined below are the main responsibilities of the classes present in the assembly:

	* **NamedPipeNative**This utility class exposes kernel32.dll methods for Named Pipes communication. It also defines constants for some of the error codes and method parameter values.
	* **NamedPipeWrapper** : This class is a wrapper around NamedPipesNative. It uses the exposed kernel32.dll methods to provide controlled Named Pipes functionality.
	* **APipeConnection** : An abstract class, which defines the methods for creating Named Pipes connections, reading and writing data. This class is inherited by the ClientPipeConnection and ServerPipeConnection classes, used by client and server applications respectively.
	* **ClientPipeConnection** : Used by client applications to communicate with server ones by using Named Pipes.
	* **ServerPipeConnection** : Allows a Named Pipes server to create connections and exchange data with clients.
	* **PipeHandle** : Holds the operating system native handle and the current state of the pipe connection.

.. note::
	This assembly is only used in the combined ArcGIS/MapInfo variant of the tool.


.. index::
	single: Assemblies; ArcObjectsInstaller

.. _assembly_arcobjectsinstaller:

ArcObjectsInstaller
-------------------

This assembly contains a custom *Installer class* that is included within the installer. The installer class is recognised by the Windows installer which instantiates the class and calls various methods when an install/uninstall is performed to register the HluArcMapExtension assembly with ArcGIS. See :ref:`esri_registration` for more details.

.. note::
	This assembly is only used in the combined ArcGIS/MapInfo variant of the tool.


.. raw:: latex

	\newpage

.. index::
	single: Components; Installer

.. _installer_project:

Installer Project
=================

HluSetup_ISLE
-------------

This project is an InstallShield Limited Edition installation project that creates a Windows Installer for the tool. The various elements of the installer can be defined using the various views in InstallShield's user interface. See :ref:`installer` for more details.


Other Information
=================

.. index::
	single: Components; Named Pipes

.. _named_pipes:

Named Pipes
-----------

Inter-Process Communication (IPC) is a set of techniques for the exchange of data among multiple threads in one or more processes. Processes may be running on one or more computers connected by a network. IPC techniques include Named Pipes, File Mapping, Mailslot, Remote Procedure Calls (RPC), etc.

Named pipes are a mechanism for one-way or bi-directional inter-process communication between two or more processes. Named Pipes are sections of shared memory used by separate processes to communicate with one another. The application that creates a pipe is the pipe server. A process that connects to the pipe server is a client. It is most useful in situations where one application is exchanging frequent short text messages with another, located on the same machine or within the same LAN.

The HLU Tool uses Named Pipes in the ArcGIS implementation for communicating between the tool user-interface and the ArcGIS extension. It allows the user-interface to interrogate data and instigate actions within the ArcGIS desktop process started by the tool.

**Server-side logic**

	1. Create a named pipe.
	2. Listen (wait) for the client to connect.
	3. Once connected, read the client's request from the pipe and write the response.
	4. Disconnect the pipe, and close the handle.

**Client-side logic**

	1. Try to open a named pipe.
	2. Once open, set the read mode and the blocking mode of the specified named pipe.
	3. Send a message to the pipe server and receive its response.
	4. Close the pipe.

