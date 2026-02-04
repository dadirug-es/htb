## Assembling & Debugging
### Assembling and Disassembling

```sh
user@IT-JARTIGA-LT:/mnt/c/Users/jartiga.IT-JARTIGA-LT/Downloads$ objdump -sj .data -d disasm

disasm:     file format elf64-x86-64

Contents of section .data:
 402000 4842547b 64313534 3535336d 3831316e  HBT{d154553m811n
 402010 395f3831 6e343231 33355f32 5f66316e  9_81n42135_2_f1n
 402020 645f3533 63323337 357d               d_53c2375}

Disassembly of section .data:

0000000000402000 <message>:
  402000:       48                      rex.W
  402001:       42 54                   rex.X push %rsp
  402003:       7b 64                   jnp    402069 <_end+0x39>
  402005:       31 35 34 35 35 33       xor    %esi,0x33353534(%rip)        # 3375553f <_end+0x3335350f>
  40200b:       6d                      insl   (%dx),%es:(%rdi)
  40200c:       38 31                   cmp    %dh,(%rcx)
  40200e:       31 6e 39                xor    %ebp,0x39(%rsi)
  402011:       5f                      pop    %rdi
  402012:       38 31                   cmp    %dh,(%rcx)
  402014:       6e                      outsb  %ds:(%rsi),(%dx)
  402015:       34 32                   xor    $0x32,%al
  402017:       31 33                   xor    %esi,(%rbx)
  402019:       35 5f 32 5f 66          xor    $0x665f325f,%eax
  40201e:       31 6e 64                xor    %ebp,0x64(%rsi)
  402021:       5f                      pop    %rdi
  402022:       35 33 63 32 33          xor    $0x33326333,%eax
  402027:       37                      (bad)
  402028:       35                      .byte 0x35
  402029:       7d                      .byte 0x7d
```

## Shellcoding
### Shellcoding Tools
```sh
┌─[eu-academy-6]─[10.10.14.231]─[htb-ac-1564439@htb-zbewjpshcx]─[~]
└──╼ [★]$ clear && (set -x; nasm -f elf64 hellow.s && ld -o hellow hellow.o && cat hellow.s && ./hellow)
+ nasm -f elf64 hellow.s
+ ld -o hellow hellow.o
+ cat hellow.s
  global _start

  section .text
_start:
  xor rax, rax
  push rax

  mov rsi, "flag.txt"
  push rsi
  mov rsi, rsp

  push rax

  mov rbx, "/bin/cat"
  push rbx
  mov rbx, rsp

  push rax
  push rsi
  push rbx
  mov rsi, rsp

  push rax

  mov rdi, "/bin/cat"
  push rdi
  mov rdi, rsp

  mov rdx, rax

  mov rax, 59
  syscall
+ ./hellow
htb{flag}
```
