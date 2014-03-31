vslint
======
Vslint is a command line utility used for detecting inconsistencies in
Visual Studio project files.

Features
--------

Currently vslint scans for these issues.

* Duplicate references
* Missing files
* Files that exist on disk but are not included in the project

It will also try to locate .gitignore and .hgignore files and use them
to filter unimportant issues.

Usage
-----

	> vslint .
	Project .\vslint\vslint.fsproj
	  no issues

	Project .\vslint.Tests\vslint.Tests.fsproj
	  no issues

	Found 0 issues

Ignored files and folders
-------------------------
Even if you don't have a .gitignore or .hgignore some files and folders
are ignored by default.

*Folders*

* .git
* .hg
* .svn
* bin
* obj
* packages

*Files*

* .gitignore
* .hgignore
* .sln
* .csproj
* .fsproj
* .vbproj
* .targets
* .suo
* .user
* .orig

.vslintignore
-------------
If you have additional files that should be ignored you may add a
file named .vslintignore with one regular expression per line.

Lines starting with # are comments, empty lines are ignored.

*Sample*

	# Ignore powershell files
	\.ps(m|1)$

	# Ignore ReSharper files
	_ReSharper\.*/
