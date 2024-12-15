# c3docgen

using c3c v0.6.5

program to generate documents from c3 source files.

will search for all .c3 files and create documents from sources.
by default, it will generate separate .md files for each module.
modules separate by multiple files will be concatenated into a single file.

there are limitations to using multiple files. if you have modules in the
project folder that have the same name, only 1 file will be generated for that module
which will likely be the first one encountered in the scan.

c3docgen mono will generate a single file with all the modules. this is the only way to
ensure all contidional modules and modules that have the same name will be scanned for
documentation.

documentation consists of using <* *> pairs. the opening pair must be aligned with the
beginning of a line, or they are ignored and treated like normal text. the closing pair
should likewise be on a new line for consistency.

functions and macros that are not documented will still be added to the output document.

to add documents to a top level file (a module), there should be only one per module.

```
<*
 	my module works in mysterious ways.
*>
module my_module;
```

this will generate:

## module my_module

```
	my module works in mysterious ways.
```

the following

```
<*
 my_func does some things with with arguments.
 @param count `the number of things to do`
 @return! MyFuncError.NULL
 @return `the number of things done`
*>
fn usz! my_func (usz count)
{
	...
	return result;
}
```

will generate:

### fn usz! my_func (usz count)

```
 my_func does some things with with arguments.
 @param count `the number of things to do`
 @return! MyFuncError.NULL
 @return `the number of things done`
```

