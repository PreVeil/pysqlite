pysqlite
========

Python DB-API module for SQLite 3.

Online documentation can be found [here] (https://pysqlite.readthedocs.org/en/latest/sqlite3.html).

You can get help from the community on the Google Group: https://groups.google.com/forum/#!forum/python-sqlite



## How To Build for PreVeil

We should make platform specific wheel packages (`.whl`) for each of the supported platforms.

1. You must have `wheel` package on your system => `pip install wheel`
2. Clone [PreVeil/pysqlite](https://github.com/PreVeil/pysqlite) repo. Checkout branch `pv-2.8.3`.
3. Download the latest sqlite amalgamation from https://www.sqlite.org/download.html.  (if a specific amalgamation version is required, get it from the [fossil repo](http://www.sqlite.org/getthecode.html), or [build the amalgamation yourself](http://www.sqlite.org/amalgamation.html#amalgbuild)). Note: **sqlite 3.19.3 amalgamation files are in _deps folder**
4. Extract the files (`shell.c, sqlite3.c, sqlite3.h, sqlite3ext.h`), copy them under pysqlite base folder.



5. ​

   ### OSX

   1. make build wheel with : `python setup.py bdist_wheel`, this should create `pysqlite-2.8.3-cp27-cp27m-macosx_*_x86_64.whl` under `./dist/`.

   ### Windows

   1. ​make sure you have [Visual C++ for Python](https://www.microsoft.com/en-us/download/details.aspx?id=44266) installed on your computer.  Note: **installation file  VCForPython27.msi is in _deps folder**
   2. make build wheel with : `python setup.py bdist_wheel`, this should create `pysqlite-2.8.3-cp27-cp27m-win32.whl` under `./dist/`.
   3. In case setuptools gives you errors not being able to locate system's compiler, try to run `vcvarsall.bat x86`/`vcvarsall.bat x64` yourself. This exports the vars in your environment so to be used by setuptools at compile time. Alternatively you can build sqlite3 amalgamation yourself, running this at pysqlite root folder should build the library to be used by python setuptools: A)`cl -c sqlite3.c` B)`lib sqlite3.obj -out:sqlite3.lib`



6. You can verify installation of the built wheel by installing it: `pip install dist/<wheel-filename>.whl`.
7. push the wheel file to [`PreVeil/vendor`](https://github.com/PreVeil/vendor).
8. Make sure you link the correct file in daemons [`setup.py`](https://github.com/PreVeil/core/blob/dev/daemon/setup.py) considering the platform specific wheels.
