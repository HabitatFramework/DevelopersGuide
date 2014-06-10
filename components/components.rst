**********
Components
**********

Within the Visual Studio solution for the HLU Tool there are 6 projects. Five of these projects are .NET assemblies that relate to various aspects of the tool functionality, the other project is an InstallShield project used to create a Windows Installer for the tool.

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

**Converters**
There are 4 converter classes in this folder that are used by the user interfaces and related classes to convert data values to/from more user-friendly visible values.

**Data**
There are a number of data classes in this folder that support connections between the tool and different relational database systems, including ODBC, Oracle, PostGres, SQL Server and MS Access. The recommended connection methods are SQL Server and Access, and it is not known how much testing has been done using the other connection methods.

**Date**
This folder contains a vague date class (VagueDate) that handles formatting and validation of the database date values to/from a user-friendly 'vague' format.

**GISApplication**
This folder contains the central business logic classes, including the main class (GisApp) that is an abstract class for all the core tool functionality. There are also 2 sub-folders **MapInfo** and **ArcGIS** that inherit the GisApp abstract class and override it will all the GIS application specific functionality.

.. note::
	The **ArcGIS** sub-folder is only used in the combined ArcGIS/MapInfo variant of the tool.

**Icons**
This folder contains all the icons and button images that appear on the user-interfaces.

**UI**
This folder contains all the user interface related source code in 3 sub-folders:

	* **UserControls** contains bespoke classes used by one or more of the user interfaces.
	* **View** contains the source code for user interface presentation. The user interfaces were developed using Windows Presentation Framework (WPF) and consists of a main interface (WindowsMain) and 9 other sub-interfaces.
	* **ViewModel** contains the business logic associated with each of the user interfaces.


.. index::
	single: Assemblies; HluArcMapExtension

.. _assembly_hluarcmapextension:

HluArcMapExtension
------------------

This assembly is an ArcGIS Desktop Extension that provides the interface between the main HLUGISTool assembly and ArcGIS. It consists of a main class **HluArcMapExtension** that performs the editing and geoprocessing commands (e.g. select features, update attributes, split/merge features, zoom to features) requested by the main assembly and also passes back any information requested by the main assembly (list valid HLU feature layers, query selected features, is editing active). Commands and requests are passed between the main assembly and this assembly using Named Pipes. See :ref:`named_pipes`_ for more details.

This assembly must be registered as an ArcGIS Desktop Extension before it can interface with ArcGIS. See :ref:`esri_registration`_ for more details.


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

	* **NamedPipeNative** : This utility class exposes kernel32.dll methods for Named Pipes communication. It also defines constants for some of the error codes and method parameter values.
	* **NamedPipeWrapper** : This class is a wrapper around NamedPipesNative. It uses the exposed kernel32.dll methods to provide controlled Named Pipes functionality.
	* **APipeConnection** : An abstract class, which defines the methods for creating Named Pipes connections, reading and writing data. This class is inherited by the ClientPipeConnection and ServerPipeConnection classes, used by client and server applications respectively.
	* **ClientPipeConnection** : Used by client applications to communicate with server ones by using Named Pipes.
	* **ServerPipeConnection** : Allows a Named Pipes server to create connections and exchange data with clients.
	* **PipeHandle** : Holds the operating system native handle and the current state of the pipe connection.

.. note::
	This assembly is only used in the combined ArcGIS/MapInfo variant of the tool.


ArcObjectsInstaller
-------------------

This assembly 

.. note::
	This assembly is only used in the combined ArcGIS/MapInfo variant of the tool.


.. index::
	single: Installer; Project

.. _installer_project:

Installer Project
=================

HluSetup_ISLE
-------------

This project is an InstallShield Limited Edition installation project that creates a Windows Installer for the tool. The various elements of the installer can be defined using the various views in InstallShield's user interface. See :ref:`installer`_ for more details.


.. raw:: latex

	\newpage

Other Information
=================

.. index::
	single: ESRI Registration

.. _esri_registration:

ESRI Registration
-----------------

Prior to ArcGIS version 10, Component Object Model (COM) components must be registered with the system before they can be used by ArcGIS. This was typically accomplished using Microsoft's supplied utility **RegAsm.exe**. However, starting with ArcGIS version 10 ESRI has moved away from the COM component category approach and there is now a new ESRI registration utility **ESRIRegAsm.exe** which works independently of the system registry; registration of component information for an assembly is now achieved using this new utility.

COM components must also be registered in the ESRI component categories appropriate to their intended context and function in order for the ArcGIS applications to make use of their functionality. For example, all ArcMap extensions must be registered in the ESRI **MxExtensions** component category.


Registration during build
+++++++++++++++++++++++++

Specifying the 'Register for COM Interop' option on an assembly will trigger Visual Studio to execute **RegAsm.exe** with the */codebase* argument during the *Build* and *Clean* processes to register/unregister the assembly as a COM component in the registry of the development machine. Whenever a component is being registered or unregistered for use from COM, two attribute classes within the .NET Framework, **ComRegisterFunctionAttribute** and **ComUnregisterFunctionAttribute**, allow you to specify user-defined methods that will be called automatically.

Therefore, by specifying the 'Register for COM Interop' option on the **HluArcMapExtension** assembly the methods **RegisterFunction** and **UnregisterFunction** will automatically be called. These contains user-written code to register and unregister the assembly as an ArcGIS extension in the MxExtensions component category (see examples below)::

	[ComRegisterFunction()]
	[ComVisible(false)]
	static void RegisterFunction(Type registerType)
	{
		// Required for ArcGIS Component Category Registrar support
		ArcGISCategoryRegistration(registerType);
		#if ARC10
		#else
			EsriRegasm(true, registerType);
		#endif
	}

	[ComUnregisterFunction()]
	[ComVisible(false)]
	static void UnregisterFunction(Type registerType)
	{
		// Required for ArcGIS Component Category Registrar support
		ArcGISCategoryUnregistration(registerType);
		#if ARC10
		#else
			EsriRegasm(false, registerType);
		#endif
	}

	/// <summary>
	/// Required method for ArcGIS Component Category registration -
	/// Do not modify the contents of this method with the code editor.
	/// </summary>
	private static void ArcGISCategoryRegistration(Type registerType)
	{
		string regKey = string.Format("HKEY_CLASSES_ROOT\\CLSID\\{{{0}}}", registerType.GUID);
		MxExtension.Register(regKey);
	}

	/// <summary>
	/// Required method for ArcGIS Component Category unregistration -
	/// Do not modify the contents of this method with the code editor.
	/// </summary>
	private static void ArcGISCategoryUnregistration(Type registerType)
	{
		string regKey = string.Format("HKEY_CLASSES_ROOT\\CLSID\\{{{0}}}", registerType.GUID);
		MxExtension.Unregister(regKey);
	}

.. note::
	The boolean variable **ARC10** used in the above methods is a compiler directive indicating to Visual Basic if the assembly is being compiled for a version of ArcGIS 10 or later or not.


In order to trigger the ESRIRegAsm.exe utility (for ArcGIS 10 onwards) custom calls have also been added to the **HluArcMapExtension.csproj** Visual Studio project file (see example below)::

  <Target Name="BeforeClean">
    <Exec WorkingDirectory="$(CommonProgramFiles)\ArcGIS\bin" Command="esriRegasm.exe &quot;$(TargetPath)&quot; /p:Desktop /u" Condition="Exists('$(TargetPath)')" />
  </Target>
  <Target Name="AfterBuild">
    <Exec WorkingDirectory="$(CommonProgramFiles)\ArcGIS\bin" Command="esriRegasm.exe &quot;$(TargetPath)&quot; /p:Desktop" />
  </Target>

These custom calls execute the ESRIRegAsm utility using command line argument '/p' to specify the ArcGIS 'Desktop' product. Because the '/s' argument is not supplied a dialog box will appear indicating if the registration/unregistration is successful or not.


Registration during installation
++++++++++++++++++++++++++++++++

During the installation of the HLU Tool the HluArcMapExtension assembly must also be registered using the ESRIRegAsm utility and in the *MxExtensions* component category on the target machine. Because the Visual Studio *Build* process is not run registration is achieved in a different way than as described above.

Firstly, a custom *Installer class* assembly **ArcObjectsInstaller** is included within the installer. The installer class is recognised by the Windows installer which can instantiate the class and call various methods, including the methods **Install** and **Uninstall** which are executed when an install/uninstall is performed.

Therefore, when running the setup.exe Windows installer on a target machine the ArcObjectsInstaller assembly is installed and the **Install** method is executed. This method registers the HluArcMapExtension assembly with COM and then registers it in the appropriate ESRI component category *MxExtension*. It then calls the ESRIRegAsm utility (if ArcGIS 10 onwards is installed) to register the component information for use by ArcGIS.


.. raw:: latex

	\newpage

.. index::
	single: Named Pipes

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

