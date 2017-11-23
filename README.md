If you're more familiar with Linux and GDB than with Windows, but find yourself needing/wanting to learn Windows debugging, this is the cheat sheet for you.


## Breakpoints

GDB Command  | WinDBG Command  | Description  | Usage/Examples
--|---|-- | ---
`b/break`  | `bp`  |  Set breakpoint
`disable`  | `bd #`   | Disable breakpoint  
`enable`  | `be #`  |  Enable breakpoint
`info breakpoints`/`ib`  | `bl`  | List breakpoints  
`watch`  | `ba` |  Break on access(read/write) | `ba [r|w|e] [Size] Addr`


## Running/Stepping

GDB Command  | WinDBG Command  | Description
--|---|--
`r/run` | `g` <br>  `.restart` | Run program |
`s/si` | `p`  |  Step into
`finish` |  `pt`  | Step to next return |
None |  `pc`  | Step to next call |
None | `pa`  | Step to address  |  

WinDBG also has `trace` analogues of step that will display registers and function calls. The prefixes are simply `t` instead of `p`  

## Variables and Memory

GDB Command  | WinDBG Command  | Description  | Usage/Example
--|---|-- | --
`x*`  | `d*`  |  Dump memory at address | a = ascii chars <br> u = Unicode chars <br> b = byte + ascii <br> w = word (2b) <br> W = word (2b) + ascii <br> d = dword (4b) <br> c = dword (4b) + ascii <br> q = qword (8b) <br> <br> `dd 0x1000000`
`set {int}addr` | `e*` | Edit memory | `ed 0x1000000 deadbeef` <br><br> a = ascii string <br> za = ascii string (NULL-terminated) <br> u = Unicode string <br> zu = Unicode string (NULL-terminated) <br> `e[a|u|za|zu] addr "String"`
`p` | `dt/dv`  |  Print variable
`disasm`  | `u` | Disassemble at address/symbol  


## Getting information

GDB Command  | WinDBG Command   | Description | Usage/Example
--|---|--| --
`info proc mappings` | `!address`  |   | Show virtual memory map and permissions
p | `x` | Examine symbols | `x kernel32!*CreateProcess*`
None  | `ln` |  List nearest symbol to address |
`info registers`  | `r`  |  r Reg1  Reg2 <br> r Reg=Value <br> r Reg:Type |
`bt` |  `k` | Stack backtrace  |  


## Other useful commands
`!peb`
