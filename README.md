If you're more familiar with Linux and GDB than with Windows, but find yourself needing/wanting to learn Windows debugging, this is the cheat sheet for you.


## Breakpoints

GDB Command  | WinDBG Command  | Description
--|---|--
b/break  | bp  |  Set breakpoint
r/run | g | Run program |
 |  .restart  |   |


## Running/Stepping

GDB Command  | WinDBG Command  | Description
--|---|--
s/si| p  |  step
n/ni | |
finish |  pt  | Step to next return  |

## Variables and Memory

GDB Command  | WinDBG Command  | Description
--|---|--
x*  | d*  |  Dump memory at address
 | e* | Edit memory
p  | dt/dv  |  Print variable


## Getting information

GDB Command  | WinDBG Command  | WinDBG Usage | Description
--|---|--| --
info proc mappings | !address  |   |
 | x | Examine symbols |
ln  | ln | |  List nearest symbol to address|
info registers  | r  |  r Reg1  Reg2 r Reg=Value r Reg:Type |
d  |  !vprot |   |  
bt  |  k | Stack backtrace  |  



## Other useful commands
