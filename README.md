# CSharpLinuxTest
testing code for c# and fortran in Linux
the purpose of this is to test compiling c# code with a fortran dll in linux
this is the Windows Visual Studio project that can first be compiled on windows to test. 
a simple hello world project - no argument lists in calls to fortran

use 
apt install mono-complete 
to install the mono compiler


I compiled the fortan as 
gfortran -shared  -o Dll1.so ../Dll1/Dll1.f90

in linux run this program:
Objdump -T DLL1.dll 

this showed me that the calling name was ‘dll1_’ even though I exported it as ‘dll1’ 
you have to use this name in the c# program to declare it
  public static extern int dll1_();
and to call it:
  dll1_();
  
  The windows version may require it in caps.


The source code was in one folder above the one I was working in so the “../”
doing it this way puts the result dll in the folder above the fortran project (the current directory I am working in)

Compile the C# as
mcs Program.cs   -resource:Dll1.dll

use -resource not -r or -addmodule. Those are for c# assemblies or managed code, I think

then run it as mono Program.exe

