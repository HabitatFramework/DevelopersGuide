
**********
Components
**********

Overview
========




.. raw:: latex

	\newpage

.. index::
	single: Named Pipes

.. _named_pipes:

Named Pipes
===========

Inter-Process Communication (IPC) is a set of techniques for the exchange of data among multiple threads in one or more processes. Processes may be running on one or more computers connected by a network. IPC techniques include Named Pipes, File Mapping, Mailslot, Remote Procedure Calls (RPC), etc.

Named pipes is a mechanism for one-way or bi-directional inter-process communication between two or more processes. Named Pipes are sections of shared memory used by separate processes to communicate with one another. The application that creates a pipe is the pipe server. A process that connects to the pipe server is a client. It is most useful in situations where one application is exchanging frequent short text messages with another, located on the same machine or within the same LAN.

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

**Interfaces**

There are three interfaces defined within the AppModule.InterProcessComm assembly - **IChannelManager**, **IClientChannel** and **IInterProcessConnection**. These interfaces are introduced in order to abstract the Named Pipes implementation from clients involved in the IPC.

**Classes**

Outlined below are the main responsibilities of the classes present in the .NET Named Pipes solution used by the HLU Tool.

	* **NamedPipeNative** : This utility class exposes kernel32.dll methods for Named Pipes communication. It also defines constants for some of the error codes and method parameter values.
	* **NamedPipeWrapper** : This class is a wrapper around NamedPipesNative. It uses the exposed kernel32.dll methods to provide controlled Named Pipes functionality.
	* **APipeConnection** : An abstract class, which defines the methods for creating Named Pipes connections, reading and writing data. This class is inherited by the ClientPipeConnection and ServerPipeConnection classes, used by client and server applications respectively.
	* **ClientPipeConnection** : Used by client applications to communicate with server ones by using Named Pipes.
	* **ServerPipeConnection** : Allows a Named Pipes server to create connections and exchange data with clients.
	* **PipeHandle** : Holds the operating system native handle and the current state of the pipe connection.



.. raw:: latex

	\newpage

.. index::
	single: Assemblies

.. _assemblies:

Assemblies
==========


.. index::
	single: Assemblies; HluArcMapExtension

.. _assembly_hluarcmapextension:

HluArcMapExtension
------------------

This assembly 


Registration
++++++++++++

ArcGIS components must be registered in component categories appropriate to their intended context and function in order for the ArcGIS applications to make use of their functionality. For example, all ArcMap extensions must be registered in the ESRI MxExtensions component category.

The .NET Framework contains two attribute classes, **ComRegisterFunctionAttribute** and **ComUnregisterFunctionAttribute**, that allow you to specify user-defined methods that will be called automatically whenever a component is being registered or unregistered for use from COM. Both methods are passed the CLSID of the class currently being registered, and with this information you can write code inside the methods to make the appropriate registry entries or deletions.

In HluArcMapExtension there are two methods, **RegisterFunction** and **UnregisterFunction**, that contain the user-written code that to register or unregister the assembly as an ArcGIS extension.







.. index::
	single: Assemblies; InterProcessComm

.. _assembly_interprocesscomm:

AppModule.InterProcessComm
--------------------------

This assembly contains just the Named Pipes interfaces plus the logic for exception handling and the connection state for inter-process communication.




.. index::
	single: Assemblies; Named Pipes

.. _assembly_namedpipes:

AppModule.NamedPipes
--------------------

This assembly contains all the Named Pipes classes. It is referenced by both the HLUGISTool **'client'** assembly and the HLUArcMapExtension **'server'** assembly for inter-process communication.

