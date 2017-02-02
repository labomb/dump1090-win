# dump1090-mutability with Windows and Airspy support

This package is based on mutability's version of dump109. It can be built with Visual Studio on Windows (and perhaps other Windows development environments as well), provides optional support for Airspy devices, and optional bias-t support for RTL-SDR.com V3 dongles.

For deatils on functionality/enhancements of the mutability fork of dump1090, please see README.md. Please see README-Windows.md for details on building this package on Windows.

This version is licensed under the GPL (v2 or later).
See the file COPYING for details.

# Building with Airspy support (Unix variants)

To enable support for Airspy devices, you will also need the airspy and sox resampler libs when building the dump1090 package.

You will likely need to build and install libairspy from source... it can be found [here](https://github.com/airspy/host).

You may be able to simply do the following to get the libsoxr library:

````
$ sudo apt-get install libsoxr-dev
````

If that doesn't work on your distribution, then you will need to build and install it from the source found [here](https://sourceforge.net/projects/soxr/files/).

To include the necessary Airspy support code when building, be sure to include preprocessor define macro HAVE_AIRSPY. 

For details on usage after building, do this:

````
$ dump1090 --help
````

>**Note about Airspy support:**
 The support for Airspy devices, as currently implemented, is certainly not optimal! Performance is hindered greatly by the need to resample so that the data is suitable for the demodulator code as written (which expects 8-bit samples at 2.4 MS/s). Ideally, equivalent demod code written to directly support the Airspy's 12-bit samples at 6 or 10 MS/s would be utilized. That said, writing said code is WAY beyond my abilities... hopefully someone out there will take the reins and make it happen!
 
 