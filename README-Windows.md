# dump1090-mutability on Windows

This is a fork of mutability's version of dump1090 that can be built with Visual Studio on Windows (and perhaps other Windows development environments as well).

This version is licensed under the GPL (v2 or later).
See the file COPYING for details.

For deatils on functionality/enhancements of the mutability fork of dump1090, please see README.md.

# How to build dump1090-mutability on Windows:

To build this package, the rtlsdr and pthreads libraries are required. You may opt to build them from source yourself, or you can download and use the pre-built dlls and the necessary Windows libs and header files.

To use the pre-built packages:

* Download ftp://mirrors.kernel.org/sourceware/pthreads-win32/pthreads-w32-2-9-1-release.zip
* Download http://sdr.osmocom.org/trac/raw-attachment/wiki/rtl-sdr/RelWithDebInfo.zip

The Visual Studio project files included with this package expect to find the prerequisite build files extracted from these archives in the following directories located in the source root:

#### Windows/lib
* pthreadVC2.lib
* rtlsdr.lib

#### Windows/include
* pthread.h
* sched.h
* semaphore.h
* rtl-sdr.h
* rtl-sdr_export.h

Optionally, you may wish to place the required runtime dlls extracted in the following directory (these dlls must be in the same directory as the dump1090, view1090, and faup1090 executables to successfully run):

#### Windows/dll
* pthreadVC2.dll
* rtlsdr.dll
* libusb-1.0.dll

Now open Windows/dump1090-mutability.sln with Visual Studio, choose 'Release', and then Build. The resulting executables will be located in the Windows/Release directory.

# Important Additions To Visual Studio Configuration Properties

### C/C++

#### General -> Additional Include Directories
* ..\include

#### Preprocessor -> Preprocessor Definitions
* _WIN32
* HAVE_VS2013
* HAVE_STRUCT_TIMESPEC
* ENABLE_WEBSERVER
* _CRT_SECURE_NO_WARNINGS
* _CRT_NONSTDC_NO_WARNINGS

### Linker

#### General -> Additional Library Directories
* ..\lib

#### Input -> Additional Dependencies:
* ws2_32.lib
* rtlsdr.lib
* pthreadVC2.lib

# General Notes, in no particular order

* Windows doesn't have a good way to measure cpu time (there is no CLOCK_THREAD_CPUTIME_ID), so no cpu related statistics are displayed if using the --stats switch, or provided in the stats.json file (if using the --write-json switch).
* Windows doesn't do non-blocking stdout, so faup1090 in it's current state isn't exactly optimal, but appears to be functional. Note that dump1090-mutability supports FlightAware-TSV-format connections directly, so the need for faup1090 is somewhat obviated.
* ENABLE_WEBSERVER is defined in the provided dump1090 project file. Feel free to remove it if you do not wish to enable the local web server functionality.
* Visual Studio 2013 was used to develop this package. No other version of VS has been tested.
* Care has been taken to insure that this package will still build on the Debian/Raspbian platforms exactly as originally intended. Please let me know if I missed anything!

# Bug reports, feedback, etc...

Please use the [github issues page](https://github.com/labomb/dump1090/issues) to report any problems.
Or feel free to [email me](mailto:labomb@rochester.rr.com).

