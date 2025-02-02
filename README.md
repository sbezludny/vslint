VSLint
======

VSLint is a command line tool used for detecting inconsistencies in
Visual Studio project files.


Features
--------

Currently VSLint scans for these issues:

* Duplicate references
* Missing files
* Files that exist on disk but are not included in the project

It will also try to locate .gitignore and .hgignore files and use them
to try to avoid false positives.


Limitations
-----------

Due to the complexity VSLint will not parse conditional includes or targets files.

Complex .gitignore GLOBs may not be parsed properly, internally GLOBs are converted
to regular expressions with a pretty naive implementation that works in most cases.
For example, negated patterns are not honored.


Command line usage
------------------

	> vslint --help
	vslint, a tool for detecting inconsistencies in Visual Studio project files
	Usage: vslint [options..] path [path2 path3 ..]
	
	Options:
	-h, --help              Prints this help message
	-m, --machine-readable  Print results in an alternate machine readable format
	-v, --verbose           Lists scanned projects even if no issues are found
	-q, --quiet             Quiet unless issues are found
	
	> vslint -v
	Project .\vslint\vslint.fsproj
	  no issues
	
	Project .\vslint.Tests\vslint.Tests.fsproj
	  no issues
	
	Found 0 issues


Use as Mercurial commit hook
----------------------------

VSLint can be used as a pre commit hook in Mercurial to prevent commits with
errors in project files that may, for instance, arise in auto merges.

Simply add vslint.exe to your path and add the following to your hgrc.

	[hooks]
	precommit =
	precommit.vslint = vslint


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
