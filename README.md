#Reading XLSX on Android

Proof that demonstrates feasibility of reading XLSX files with Apache POI XSSF on Android.

This is actually not "out of box" POI, but kind of port.

lib/aa-poi-3.10-min-0.1.5.jar contains following libraries shrunk with proguard:
* stax-api-1.0.1.jar
* dom4j-1.6.1.jar
* poi-3.10-FINAL-20140208.jar
* poi-ooxml-3.10-FINAL-20140208.jar
* xmlbeans-2.3.0.jar

lib/aa-poi-ooxml-schemas-3.10-reduced-more-0.1.5.jar contains ooxml-schemas shrunk manually
Unfortunately I did not achieve workable result with reducing by proguard. 

One can download these two jars and read XLSX in his application.

**It does work without DX --core-library** option because StAX is re-compiled with 'javax' namespace renamed to 'aavax'. So namespace conflict is not possible any more. 
Strings 'javax/xml/stream', 'javax/xml/namespace' and 'javax.xml.strings' in other binaries replaced with strings containing 'aavax' instead of 'javax'.


Tested with reading and writing XLSX files. It might not work properly if you file contains Drawings or Charts. Please let me know if it fails.

##Why?
If you try to build Android project with Apache POI XSSF out of box you would face whole bunch of problems:
First and most major one is android's 65K methods limit. poi-ooxml-schemas-3.10-FINAL-20140208.jar contains approximately 68K
```
([dx] trouble writing output: Too many method references: 67997; max is 65536.)
```

Read following posts im my blog to see whole process of "porting":
* http://blog.kondratev.pro/2014/08/reading-xlsx-on-android.html
* http://blog.kondratev.pro/2014/09/further-to-my-post-from-yesterday-on.html
* http://blog.kondratev.pro/2014/09/reading-xlsx-on-android-3.html