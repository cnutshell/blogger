# module<sup>1</sup>

##Module Loading

Python programmer could import a module through *importlib.import_module* and *import* statement. They both depend on the built-in function **\__import__**.

It’s best to have a clear understanding of the semantics of **\__import__**. 

To import a module named M, **\__import__** first checks dictionary sys.modules:

> - When finding key M in sys.modules, **\__import__ **returns the corresponding value as the requested module object;
> - Otherwise, **\__import__** binds sys.modules[M] to a new empty module object with a **\__name__** of M, then looks items of sys.path in order to initialize (load) the module.

When a module is imported again, the module is not reloaded, since **\__import__** rapidly finds and returns the module’s entry in sys.modules. Thanks to this mechanism, the relatively slow loading operation takes place only the first time a module is imported in a given run of the program.

>  **Note**: Changing sys.path does not affect modules that are already loaded (and thus already recorded in sys.modules) when you change sys.path.

When looking for the file for the module M in each directory and ZIP archive along sys.path, Python considers file extensions(.pyd, .so, .py, ,pyc|.pyo, package M) in certain order. Once Python has the bytecode, Python executes the module body to initialize the module object.

> **Note**: A package's body is \__init__.py. This file could be empty.

###sys.modules

A dictionary that keep the loaded modules.

###sys.path

A list to search when importing an un-loaded module.

Initialized at the startup of program, using the environment variable PYTHONPATH. If a text file with the extension .pth is found in the PYTHONHOME directory at startup, the file’s contents are added to sys.path, one item per line.

The first item is " " which represents the directory from which the main program is loaded.

sys.path could be changed, but the loaded module does not affect.

In v2, by default, when module M in package P executes import X, Python searches for X in M, before searching in sys.path. However, this does not apply in v3. It is strongly recommended that, in v2, you use *from \__future__ import absolute_import* to make v2 behave like v3 in this respect.

##Absolute Versus Relative Imports

An import statement normally expects to find its target somewhere on sys.path, a behavior known as an absolute import. Alternatively, you can explicitly use a relative import, meaning an import of an object from within the current package. Relative imports are only available in the from statement. Getting too fancy with this feature can easily damage your code’s clarity, so use it with care, and only when necessary.



***

1. From *Python in a Nutshell 3rd Edition*
