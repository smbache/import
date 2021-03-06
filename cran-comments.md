## General
This is an update with the following features:

* import is now more strict and won't allow an import from a different
  environment to replace an existing import of that name and location.
* One can now import directly into an environment (which may not be attached)
  by wrapping it in braces, e.g. import::from(pkg, symbol, .into = {environment()})
* import::from/here/into now include a new option, `.character_only`, that
  suppresses non-standard evaluation and thus allows passing object names
  or locations in variables (character strings).
* import::from/here/into now include new options, `.all` and `.except`, that 
  allow the user to import all functions, or all functions except a few, from a
  package or module.
* import::from/here/into now include a new option, "`.chdir`", specifying whether 
  the working directory is changed before sourcing modules to import.
* import::from/here/into now include a new option, "`.directory`",  
* import::here() has been fixed to use environment() explicitly to import into
  the current environment, rather than importing into "" (the empty string),
  which no longer works because of upstream changes. Passing "" to "`.into`"
  parameter is now only a shorthand for .into = {environment()}.
* Using import::from(), import::into(), or library() inside a module that is 
  being sourced from the import::from/here/into
* The parameter order for import::here() has been changed to be consistent
  with import::from(). The change is backwards compatible because the moved 
  parameter (`.from`) was previously behind the ellipsis, requiring the use of 
  named parameters.
* Unit tests have been added and various issues fixed.

## Test environments
* local Mac OS X (R 4.0.1)
* win-builder (devel R R-4.1.0 and release R-4.0.2)
* GitHub CE (macos, linux and windows)

## R CMD check results
There were no ERRORs or WARNINGs.

There was one NOTE (due to issues with time service):
> checking for future file timestamps ... NOTE
  unable to verify current time

## Downstream dependencies
Downstream dependencies were checked with the revdep package and no
issues were found.

## Other Notes (unchanged since last):
The package's functionality may alter the search path, but this
is intended and should be clear for the user, as the main functionality 
is an alternative to using `library`. For example the call 

`import::from(parallel, makeCluster, parLapply)`

will make an "imports" entry in the search path and place the
imported there.


