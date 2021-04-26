# Note: Do not use this if you don't know what you're doing. Disabling PIE on OpenBSD is idiotic. You have been warned!

# nasm-openbsd
Executing nasm programs under openbsd

## OpenBSD note section
This note has to be included in your .nasm file  

        section .note.openbsd.ident        
        align 2    
        dd 8,4,1    
        db 'OpenBSD',0  
        dd 0  
        align 2  
 
 ## Call nasm to generate an elf64
 <code>nasm -f elf64 *.nasm</code>
 
 ## Link with ld.bfd with -nopie flag
 <code>ld.bfd -nopie *.o</code>
 
 ## Example hello world program
 
        section .note.openbsd.ident  
        align 2  
        dd 8,4,1  
        db 'OpenBSD',0  
        dd 0  
        align 2

        section .data  
        msg db "Hello, World!",10  
        len equ $-msg  

        section .text  

        global _start  
  
        _start:  
        mov rax,4  
        mov rdi,1  
        mov rsi,msg  
        mov rdx,len  
        syscall  
        mov rax,1  
        xor rdi,rdi  
        syscall  
