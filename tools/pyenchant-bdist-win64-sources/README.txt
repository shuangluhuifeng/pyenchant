
The x64 PyEnchant binary distribution contains prebuilt libraries for
enchant and its dependencies.  This directory contains the source
for those libraries, in compliance with a strict interpretation
of the GPL/LGPL.

The recommended MinGW distribution for building Enchant is Msys2.
First, follow the installation instructions for Msys2 available at
msys2.github.io. After that, you need to install all missing packages Enchant depends on using Msys2's package manager "pacman". You find their names by looking at the DLLs in pyenchant\tools\pyenchant-bdist-[win32]/[win64]-sources\build\lib.
Then, depending on your desired target architecture,
open a mingw32 or mingw64 shell, navigate to the source directory,
and type "make".

The currently shipped libraries were built by Ali Abdulkadir or were obtained
from the Msys2 project:

    https://www.msys2.github.io
    http://repo.msys2.org/

