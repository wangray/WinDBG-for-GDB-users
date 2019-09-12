If you're more familiar with Linux and GDB than with Windows, but find yourself needing/wanting to learn Windows debugging, this is the cheat sheet for you.


## Breakpoints

GDB Command  | WinDBG Command  | Description  | Usage/Examples
--|---|-- | ---
`b/break`  | `bp`  |  Set breakpoint
`disable`  | `bd #`   | Disable breakpoint  
`enable`  | `be #`  |  Enable breakpoint
`info breakpoints`/`ib`  | `bl`  | List breakpoints  
`watch`  | `ba` |  Break on access(read/write) | `ba [r\|w\|e] [Size] Addr`


## Running/Stepping

GDB Command  | WinDBG Command  | Description
--|---|--
`r/run` | `g` <br>  `.restart` | Run program |
`s/si` | `p`  |  Step over
`n/ni` | `t`  |  Step into
`finish` |  `pt`  | Step to next return |
None |  `pc`  | Step to next call |
`u` | `pa`  | Step to address  |  

## Variables, Symbols, and Memory

GDB Command  | WinDBG Command  | Description  | Usage/Example
--|---|-- | --
`x*`  | `d*`  |  Dump memory at address | a = ascii chars <br> u = Unicode chars <br> b = byte + ascii <br> w = word (2b) <br> W = word (2b) + ascii <br> d = dword (4b) <br> c = dword (4b) + ascii <br> q = qword (8b) <br> <br> `dd 0x1000000`
`set {int}addr = ` | `e*` | Edit memory | `ed 0x1000000 deadbeef` <br><br> a = ascii string <br> za = ascii string (NULL-terminated) <br> u = Unicode string <br> zu = Unicode string (NULL-terminated) <br> `e[a\|u\|za\|zu] addr "String"`
`print`/`p` | `dt/dv`  |  Print variable | `dt ntdll!_PEB` <br> `dt ntdll!_PEB @$peb`
`disasm`  | `u` | Disassemble at address/symbol  | `u kernel32!CreateProcessAStub`
`* (deref)`  | `poi` |  Dereference pointer | `u poi(ebp+4)`
None  | `x` |  Examine symbols | `x *!` <br> `x /t /v MyDll!*` list symbols in MyDll with data type, symbol type, and size

#### C++ Expression Syntax

GDB Command  | WinDBG Command  | Description  | Usage/Example
--|---|-- | --
`p (Datatype *) &variable`  | `dx (Datatype *) &variable`  |  displays a C++ expression  | `dx (nt!_EPROCESS *) &nt!PsIdleProcess`
`p [expression]`  | `??`   | Evaluate C++ expressions. Used with the C++ expression parser - `@@c++()`, that supports operators, registers, macros. etc. See [docs](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/c---numbers-and-operators) for a full list |  `?? @@c++(1+2)`


## Registers

Access registers with `@`, like `@eip`.

GDB Command  | WinDBG Command   | Description | Usage/Example
--|---|--| --
`info registers` | `r`  |  Show registers | `r Reg1  Reg2` <br> `r Reg:Type` <br> `Type` = data format in which to display the register (i.e.: `r eax:uw`) <br> ib = Signed byte <br> ub = Unsigned byte <br> iw = Signed word (2b) <br> uw = Unsigned word (2b) <br> id = Signed dword (4b) <br> ud = Unsigned dword (4b) <br> iq = Signed qword (8b) <br> uq = Unsigned qword (8b) <br> f = 32-bit floating-point <br> d = 64-bit floating-point
`set reg =`  |  `r Reg=Value` | Set register |  


## Getting information

GDB Command  | WinDBG Command   | Description | Usage/Example
--|---|--| --
`info proc mappings` | `!address`  |  Show virtual memory map and permissions | `!address addr`
`print`/`p` | `x` | Examine symbols | `x kernel32!*CreateProcess*`
None  | `ln` |  List nearest symbol to address |
`backtrace`/`bt` |  `k` | Stack backtrace  |  
  None | `!exchain`  |  View SEH Chain |
  |   |   |   |  


## Other useful commands
`!peb` – dumps Process Environment Block
`dt ntdll!_PEB @$peb` — dumps more PEB info of our process


## Tips
The WinDBG executable is installed in `C:\Program Files (x86)\Windows Kits\10\Debuggers\x86[64]/`. If it's not in your path, add it by going to the `Edit system environment variables` menu, and append to the `Path` variable.

`$peb` is a "pseudo-register", and there are [others](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/pseudo-register-syntax) that hold useful values. Some are `$teb`, `$csp`, `$curprocess`.


## References
http://windbg.info/doc/1-common-cmds.html
