# Assemby (i386)

## General purpose registers
Modern x86 processors have eight 32-bit general purpose registers.
* %EAX
* %EBX
* %ECX
* %EDX
* %ESI
* %EDI
* %ESP (Stack Pointer)
* %EBP (Base Pointer) 

## Declaring Static Data Regions

You can declare static data regions using special assembler directives.  
Data declarations must be preceded by the .DATA directive.

**_Example (syntax):_**
```
.data
<name>      <size>      <value>
```

* `<name>`: Memory zone name.
* `<size>`: Memory zone size.  
  Allowed values:
    * DB: 1 byte.
    * DW: 2 byte.
    * DD: 4 byte.
* `<value>`: Contents of the memory zone. If the field is set to "?" the memory area will not be initialized   

**_Example:_**
```
.data
var1     DB      22     ; Declare a byte, referred to as location var1, containing the value 22.
var2     DB      ?      ; Declare an uninitialized byte, referred to as location var2.
var3     DW      33     ; Declare a 2-byte, referred to as location var3, containing the value 33.
var4     DD      44     ; Declare a 4-byte, referred to as location var4, containing the value 44.

; Declare a two consecutive bytes
arr      DD      3      ; Referred to as location arr
         DD      4      ; Referred to as location arr + 1
```

## Addressing Memory    
Modern x86-compatible processors are capable of addressing up to 232 bytes of memory: memory addresses are 32-bits wide.  
The mov instruction copies the data item referred to by its second operand into the location referred to by its first operand.   
While register-to-register moves are possible, direct memory-to-memory moves are not.   

**_Syntax:_**
```
mov     <reg>,<reg>
mov     <reg>,<mem>
mov     <mem>,<reg>
mov     <reg>,<const>
mov     <mem>,<const>
mov     <mem>,<mem>     ; Impossible
```

**_mov instructions using address computations are:_**
```
mov     eax, [ebx] 	            ; Move the 4 bytes in memory at the address contained in EBX into EAX
mov     [var], ebx 	            ; Move the contents of EBX into the 4 bytes at memory address var. (Note, var is a 32-bit constant).
mov     eax, [esi - 4] 	        ; Move 4 bytes at memory address ESI + (-4) into EAX
mov     [esi + eax], cl 	    ; Move the contents of CL into the byte at address ESI+EAX
mov     edx, [esi + 4 * ebx]   	; Move the 4 bytes of data at address ESI+4*EBX into EDX
```
**_Some examples of invalid address calculations include:_**
```
mov eax, [ebx-ecx] 	        ; Can only add register values
mov [eax + esi + edi], ebx  ; At most 2 registers in address computation
```

Sitography: https://www.cs.virginia.edu/~evans/cs216/guides/x86.html
