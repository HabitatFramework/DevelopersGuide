************
Registration
************

.. index::
	single: ArcGIS Registration

.. _esri_registration:

ArcGIS Registration
===================

Prior to ArcGIS version 10, Component Object Model (COM) components must be registered with the system before they can be used by ArcGIS. This was typically accomplished using Microsoft's supplied utility **RegAsm.exe**. However, starting with ArcGIS version 10 ESRI has moved away from the COM component category approach and there is now a new ESRI registration utility **ESRIRegAsm.exe** which works independently of the system registry; registration of component information for an assembly is now achieved using this new utility.

COM components must also be registered in the ESRI component categories appropriate to their intended context and function in order for the ArcGIS applications to make use of their functionality. For example, all ArcMap extensions must be registered in the ESRI **MxExtensions** component category.


Registration during build
-------------------------

Specifying the 'Register for COM Interop' option on an assembly will trigger Visual Studio to execute **RegAsm.exe** with the */codebase* argument during the *Build* and *Clean* processes to register/unregister the assembly as a COM component in the registry of the development machine. Whenever a component is being registered or unregistered for use from COM, two attribute classes within the .NET Framework, **ComRegisterFunctionAttribute** and **ComUnregisterFunctionAttribute**, allow you to specify user-defined methods that will be called automatically.

Therefore, by specifying the 'Register for COM Interop' option on the **HluArcMapExtension** assembly the methods **RegisterFunction** and **UnregisterFunction** will automatically be called. These contains user-written code to register and unregister the assembly as an ArcGIS extension in the MxExtensions component category (see below)::

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
	The boolean variable **ARC10** used in the above methods is a compiler *directive* indicating to Visual Basic if the assembly is being compiled for a version of ArcGIS 10 or later or not.


In order to trigger the ESRIRegAsm.exe utility (for ArcGIS 10 onwards) custom calls have also been added to the **HluArcMapExtension.csproj** Visual Studio project file (see below)::

  <Target Name="BeforeClean">
    <Exec WorkingDirectory="$(CommonProgramFiles)\ArcGIS\bin" Command="esriRegasm.exe &quot;$(TargetPath)&quot; /p:Desktop /u" Condition="Exists('$(TargetPath)')" />
  </Target>
  <Target Name="AfterBuild">
    <Exec WorkingDirectory="$(CommonProgramFiles)\ArcGIS\bin" Command="esriRegasm.exe &quot;$(TargetPath)&quot; /p:Desktop" />
  </Target>

These custom calls execute the ESRIRegAsm utility using command line argument '/p' to specify the ArcGIS 'Desktop' product. Because the '/s' argument is not supplied a dialog box will appear indicating if the registration/unregistration is successful or not.


Registration during installation
--------------------------------

During the installation of the HLU Tool the HluArcMapExtension assembly must also be registered using the ESRIRegAsm utility and in the *MxExtensions* component category on the target machine. Because the Visual Studio *Build* process is not run registration is achieved in a different way than as described above.

Firstly, a custom *Installer class* assembly **ArcObjectsInstaller** is included within the installer. The installer class is recognised by the Windows installer which can instantiate the class and call various methods, including the methods **Install** and **Uninstall** which are executed when an install/uninstall is performed.

Therefore, when running the **setup.exe** Windows installer on a target machine the ArcObjectsInstaller assembly is installed and the **Install** method is executed which performs the following:

	* It registers the HluArcMapExtension assembly with COM
	* It registers the assembly in the appropriate ESRI component category **MxExtension**
	* It executes the **ESRIRegAsm** utility (if ArcGIS 10 onwards is installed) to register the assembly information for use by ArcGIS.

