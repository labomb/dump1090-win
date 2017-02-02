# dump1090-mutability with Windows and Airspy support

This package is based on mutability's version of dump1090. It can be built with Visual Studio on Windows (and perhaps other Windows development environments as well), provides optional support for Airspy devices, and optional bias-t support for RTL-SDR.com V3 dongles.

This version is licensed under the GPL (v2 or later).
See the file COPYING for details.

For deatils on functionality/enhancements of the mutability fork of dump1090, please see README.md.

# How to build dump1090-mutability on Windows:

To build this package, the rtlsdr and pthreads libraries are required. You may opt to build them from source yourself, or you can download and use  pre-built dlls and the necessary Windows libs and header files. If you wish to enable Airspy support, you will also need the libairspy and libsoxr libraries, both of which you will likely need to build yourself.

* Source for libairspy can be found [here](https://github.com/airspy/host).
* Source for libsoxr can be found [here](https://sourceforge.net/projects/soxr/files/).

To use the available pre-built packages:

* Download ftp://mirrors.kernel.org/sourceware/pthreads-win32/pthreads-w32-2-9-1-release.zip
* Download http://sdr.osmocom.org/trac/raw-attachment/wiki/rtl-sdr/RelWithDebInfo.zip

The Visual Studio project files included with this package expect to find the prerequisite build files extracted/built from these archives in the following directories located in the source root:

#### Windows/lib
* pthreadVC2.lib
* rtlsdr.lib
* airspy.lib         (if enabling Airspy support)
* libsoxr.lib        (if enabling Airspy support)

#### Windows/include
* pthread.h
* sched.h
* semaphore.h
* rtl-sdr.h
* rtl-sdr_export.h
* airspy.h           (if enabling Airspy support)
* airspy_commands.h  (if enabling Airspy support)
* soxr.h             (if enabling Airspy support)

Optionally, you may wish to place the required runtime dlls extracted in the following directory (these dlls must be in the same directory as the dump1090, view1090, and faup1090 executables to successfully run):

#### Windows/dll
* pthreadVC2.dll
* rtlsdr.dll
* libusb-1.0.dll
* airspy.dll         (if enabling Airspy support)

Now open Windows/dump1090-mutability.sln with Visual Studio, choose 'Release', and then Build. The resulting executables will be located in the Windows/Release directory.

# Important Additions To Visual Studio Configuration Properties

### C/C++

#### General -> Additional Include Directories
* ..\include

#### Preprocessor -> Preprocessor Definitions
* _WIN32
* HAVE_AIRSPY        (if enabling Airspy support)
* HAVE_RTL_BIAST     (if enabling bias-t support for RTL-SDR.com V3 dongles: see note below)
* HAVE_VS2013
* HAVE_STRUCT_TIMESPEC
* ENABLE_WEBSERVER   (if enabling the internal web server)
* _CRT_SECURE_NO_WARNINGS
* _CRT_NONSTDC_NO_WARNINGS

### Linker

#### General -> Additional Library Directories
* ..\lib

#### Input -> Additional Dependencies:
* ws2_32.lib
* rtlsdr.lib
* pthreadVC2.lib
* airspy.lib         (if enabling Airspy support)
* libsoxr.lib        (if enabling Airspy support)

# General Notes, in no particular order

* Windows doesn't have a good way to measure cpu time (there is no CLOCK_THREAD_CPUTIME_ID), so no cpu related statistics are displayed if using the --stats switch, or provided in the stats.json file (if using the --write-json switch).
* Windows doesn't do non-blocking stdout, so faup1090 in it's current state isn't exactly optimal, but appears to be functional. Note that dump1090-mutability supports FlightAware-TSV-format connections directly, so the need for faup1090 is somewhat obviated.
* ENABLE_WEBSERVER is defined in the provided dump1090 project file. Feel free to remove it if you do not wish to enable the local web server functionality.
* Visual Studio 2013 was used to develop this package. No other version of VS has been tested.
* Care has been taken to insure that this package will still build on the Debian/Raspbian platforms exactly as originally intended. Please let me know if I missed anything!

>**Note about Airspy support:**
 The support for Airspy devices, as currently implemented, is certainly not optimal! Performance is hindered greatly by the need to resample so that the data is suitable for the demodulator code as written (which expects 8-bit samples at 2.4 MS/s). Ideally, equivalent demod code written to directly support the Airspy's 12-bit samples at 6 or 10 MS/s would be utilized. That said, writing said code is WAY beyond my abilities... hopefully someone out there will take the reins and make it happen!
 
 >**Note about Bias-t support for RTL-SDR.com V3 dongles:**
 If you wish to enable bias-t support, you must insure that you are building with a version of rtlsdr.lib that supports this capability. You can find suitable source package [here](https://github.com/rtlsdrblog/rtl_biast) and [here](https://github.com/librtlsdr/librtlsdr/tree/master/src), and binary distributions [here](https://github.com/rtlsdrblog/rtl-sdr/releases/tag/v1.1) and [here](https://github.com/librtlsdr/librtlsdr/releases/tag/v0.7.0).
 
# Bug reports, feedback, etc...

Please use the [github issues page](https://github.com/labomb/dump1090/issues) to report any problems.
Or feel free to [email me](mailto:labomb@rochester.rr.com).

