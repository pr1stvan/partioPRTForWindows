# partioPRTForWindows

It's a modified version of partio: https://github.com/wdas/partio.  
Unlike the original version, it can load and write prt files on windows and  
can compiled with visual studio without any dependencies.  

I've removed the examples and the support of other file extensions.

I've fixed a bug in PRT.cpp, line 229:
```
particleSize = (std::max)( particleSize, chans.back().offset + sizes[ch.type] );  
->  
particleSize = (std::max)( particleSize, chans.back().offset + sizes[ch.type] * ch.arity);  
```

## Compile with visual studio
open git bash:
```
git clone --recursive https://github.com/pr1stvan/partioPRTForWindows.git
cd partioPRTForWindows
mkdir build
cd build
cmake .. -G "Visual Studio 15 2017"
```
Currently, it only works in release mode.
