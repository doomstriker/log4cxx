This is a standalone project for compiling [log4cxx](http://logging.apache.org/log4cxx/) under Visual Studio 2010. 

* There's a [bug](http://connect.microsoft.com/VisualStudio/feedback/details/473882/error-message-c-c-optimizing-compiler-stopped-working) in VS's c++ compiler that spits out numerous errors when compiling log4cxx's sources. The changes herein essentially move class nested template definitions out of the class scope. In once case (LoggingEvent::KeySet), simply moving KeySet to the outer scope introduces errors. To avoid this, KeySet resides in an alternate namespace LoggingEventDetail.

* The .dsp project that ships with the sources uses __cdecl calling convention. However, static member functions aren't decorated as such, and this causes linker errors when linking against __stdcall projects. I've added __cdecl decorations to functions I've used so far, so the changes are not comprehensive.

* Some packages tests fail. No effort has gone into determining why.

