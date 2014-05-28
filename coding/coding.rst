
***************
Coding Standard
***************


.. index::
	single: Coding Standards; General

.. _coding_general:

General Guidelines
==================

The following are a set of 'basic principles', based on those recommended by `Bugzilla <http://www.bugzilla.org/docs/developer.html>`_, that are also relevant to this Developer's Guide:

	* These guidelines exist in order to **reduce bugs** and make it easier to change things in the future.
	* Making it easier to change things in the future is important, because an important law of code is: **All Code Will Change**.
	* Code should be **as simple as possible**. When writing code one of the primary goals should be: **make it easy for other programmers to use and read your code**.
	* **Readable** code is more important than **clever** code.
	* If you're trying to be clever instead of trying to be readable, then maybe you're trying to make things 'faster? If so, just remember: don't solve a problem before you know it exists. If you don't know (by actual, detailed tests) that your code is slow, don't worry about making it 'faster. This isn't just limited to optimization--many programmers are constantly solving problems that nobody has ever experienced. Don't do that.
	* You cannot introduce new bugs unless you change code (obviously). This means:
	* 
		* The more code you change, the more bugs you will create. There are no 'perfect' programmers. Everybody makes a few mistakes now and then.
		* The number of bugs introduced by a patch is proportional to the size of the patch.
		* Hence, patches should be as small as possible, and should change only what they need to change.
	
	* An easy way to check if your code is readable, is to ask yourself, 'Will another programmer understand this line instantly when they look at it?'' If not, that line either needs to be re-written or needs a comment (see )



.. raw:: latex

	\newpage

.. index::
	single: Coding Standards; Metadata

.. _coding_metadata:

Metadata
========





.. raw:: latex

	\newpage

.. index::
	single: Coding Standards; Comments

.. _coding_comments:

Comments
========

General comments
----------------



Task List comments
------------------

'Task List' comments have been added at the start of each section of code that relates to a Known Issue, Change Request or Fix. A 'Task List' comment is formatted as::

	// token: reference (description)

	where:  `token` is one of the tokens listed below
			`reference` is a Known Issue or Change Request reference (where applicable)
			`description` is a brief summary of the comment

Visual Studio can be configured so that these comments automatically appear in the **Task List** window. To configure Visual Studio go to <Tools> / <Options>, click on the <Environment> list heading the left to expand the list and click on <Task List>. Add the following *Tokens* to the Token List on the right:

	* FIXED : Used to indicate where a Known Issue has been fixed
	* CHANGED : Used to indicate where changes relating to a Change Request have been applied
	* FIX : Used to indicate where a previously unknown issue (e.g. identified during coding/testing) has been fixed
	* HACK : Used to indicate when a quick 'Hack' has been applied to temporarily resolve a previously unknown issue
	* QUERY : Used to indicate where code (possibly relating to a Known Issue or Change Request) may need to be amended/corrected
	* TODO : Used to indicate where work relating to a change or fix remains outstanding

Where possible top & tail comment lines should be inserted around the 'Task List' comment and related source code to denote where the change/fix/query starts and stops. Additional 'explanatory' comments should also be added to explain what the amended code does, or why it was amended. For example::

	//---------------------------------------------------------------------
	// FIXED: KI96 (BAP Habitats)
	// Enable editing of bap habitats when they are only associated
	// with matrix, formation, management or complex codes (rather
	// than habitat codes.
	OnPropertyChanged("BapHabitatsAutoEnabled");
	//---------------------------------------------------------------------

The same 'Task List' comment can be inserted in multiple locations in the source code if more than one section of code relates to the change/fix/query. However, the 'explanatory' comments should be specific to the specifically amended code.

