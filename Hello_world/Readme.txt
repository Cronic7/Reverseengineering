1)Hello world program compile{
	->Use Gcc to compile the c program
	->Syntax: gcc Filename.c -o Output filename
	[gcc helloworld.c -o helloworld  ]
}
2)Identifying file type{
	First step of the process would be identifying file type.
	->Use file command
	->Syntax:File filename
	Output:[$ file helloworld                                                                                                                                                                                                                   
	helloworld: ELF 64-bit LSB pie executable, x86-64, 
	version 1 (SYSV), dynamically linked, 
	interpreter /lib64/ld-linux-x86-64.so.2, 
	BuildID[sha1]=5a0354bf1716bddc4697abdbbf8375017fc59587, for GNU/Linux 3.2.0, not stripped
	 ]

	Output:	[$ file helloworld.c 
	helloworld.c: C source, ASCII text ]

}
3)Use Strings command to look at the string in the file{

	->Syntax:Strings filename
	Output:[$ strings helloworld 
	/lib64/ld-linux-x86-64.so.2
	printf
	__cxa_finalize
	__libc_start_main
	libc.so.6
	GLIBC_2.2.5
	_ITM_deregisterTMCloneTable
	__gmon_start__
	_ITM_registerTMCloneTable
	u/UH
	[]A\A]A^A_
	Hello world!
	;*3$"
	GCC: (Debian 10.2.1-6) 10.2.1 20210110
	crtstuff.c
	deregister_tm_clones
	__do_global_dtors_aux
	completed.0
	__do_global_dtors_aux_fini_array_entry
	frame_dummy
	__frame_dummy_init_array_entry
	helloworld.c
	__FRAME_END__
	__init_array_end
	_DYNAMIC
	__init_array_start
	__GNU_EH_FRAME_HDR
	_GLOBAL_OFFSET_TABLE_
	__libc_csu_fini
	_ITM_deregisterTMCloneTable
	_edata
	printf@GLIBC_2.2.5
	__libc_start_main@GLIBC_2.2.5
	__data_start
	__gmon_start__
	__dso_handle
	_IO_stdin_used
	__libc_csu_init
	__bss_start
	main
	__TMC_END__
	_ITM_registerTMCloneTable
	__cxa_finalize@GLIBC_2.2.5
	.symtab
	.strtab
	.shstrtab
	.interp
	.note.gnu.build-id
	.note.ABI-tag
	.gnu.hash
	.dynsym
	.dynstr
	.gnu.version
	.gnu.version_r
	.rela.dyn
	.rela.plt
	.init
	.plt.got
	.text
	.fini
	.rodata
	.eh_frame_hdr
	.eh_frame
	.init_array
	.fini_array
	.dynamic
	.got.plt
	.data
	.bss
	.comment
]
}

4) Disassemble the program{
	We can use objdump to disassemble the program.Do make sure the disassembly flavour is set to intel.
	[$ objdump -M intel -d helloworld                                                                                                                                                                                                    

	helloworld:     file format elf64-x86-64


	Disassembly of section .init:

	0000000000001000 <_init>:
	    1000:       48 83 ec 08             sub    rsp,0x8
	    1004:       48 8b 05 dd 2f 00 00    mov    rax,QWORD PTR [rip+0x2fdd]        # 3fe8 <__gmon_start__>
	    100b:       48 85 c0                test   rax,rax
	    100e:       74 02                   je     1012 <_init+0x12>
	    1010:       ff d0                   call   rax
	    1012:       48 83 c4 08             add    rsp,0x8
	    1016:       c3                      ret    

	Disassembly of section .plt:

	0000000000001020 <.plt>:
	    1020:       ff 35 e2 2f 00 00       push   QWORD PTR [rip+0x2fe2]        # 4008 <_GLOBAL_OFFSET_TABLE_+0x8>
	    1026:       ff 25 e4 2f 00 00       jmp    QWORD PTR [rip+0x2fe4]        # 4010 <_GLOBAL_OFFSET_TABLE_+0x10>
	    102c:       0f 1f 40 00             nop    DWORD PTR [rax+0x0]

	0000000000001030 <printf@plt>:
	    1030:       ff 25 e2 2f 00 00       jmp    QWORD PTR [rip+0x2fe2]        # 4018 <printf@GLIBC_2.2.5>
	    1036:       68 00 00 00 00          push   0x0
	    103b:       e9 e0 ff ff ff          jmp    1020 <.plt>

	Disassembly of section .plt.got:

	0000000000001040 <__cxa_finalize@plt>:
	    1040:       ff 25 b2 2f 00 00       jmp    QWORD PTR [rip+0x2fb2]        # 3ff8 <__cxa_finalize@GLIBC_2.2.5>
	    1046:       66 90                   xchg   ax,ax

	Disassembly of section .text:

	0000000000001050 <_start>:
	    1050:       31 ed                   xor    ebp,ebp
	    1052:       49 89 d1                mov    r9,rdx
	    1055:       5e                      pop    rsi
	    1056:       48 89 e2                mov    rdx,rsp
	    1059:       48 83 e4 f0             and    rsp,0xfffffffffffffff0
	    105d:       50                      push   rax
	    105e:       54                      push   rsp
	    105f:       4c 8d 05 5a 01 00 00    lea    r8,[rip+0x15a]        # 11c0 <__libc_csu_fini>
	    1066:       48 8d 0d f3 00 00 00    lea    rcx,[rip+0xf3]        # 1160 <__libc_csu_init>
	    106d:       48 8d 3d c1 00 00 00    lea    rdi,[rip+0xc1]        # 1135 <main>
	    1074:       ff 15 66 2f 00 00       call   QWORD PTR [rip+0x2f66]        # 3fe0 <__libc_start_main@GLIBC_2.2.5>
	    107a:       f4                      hlt    
	    107b:       0f 1f 44 00 00          nop    DWORD PTR [rax+rax*1+0x0]

	0000000000001080 <deregister_tm_clones>:
	    1080:       48 8d 3d a9 2f 00 00    lea    rdi,[rip+0x2fa9]        # 4030 <__TMC_END__>
	    1087:       48 8d 05 a2 2f 00 00    lea    rax,[rip+0x2fa2]        # 4030 <__TMC_END__>
	    108e:       48 39 f8                cmp    rax,rdi
	    1091:       74 15                   je     10a8 <deregister_tm_clones+0x28>
	    1093:       48 8b 05 3e 2f 00 00    mov    rax,QWORD PTR [rip+0x2f3e]        # 3fd8 <_ITM_deregisterTMCloneTable>
	    109a:       48 85 c0                test   rax,rax
	    109d:       74 09                   je     10a8 <deregister_tm_clones+0x28>
	    109f:       ff e0                   jmp    rax
	    10a1:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]
	    10a8:       c3                      ret    
	    10a9:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]

	00000000000010b0 <register_tm_clones>:
	    10b0:       48 8d 3d 79 2f 00 00    lea    rdi,[rip+0x2f79]        # 4030 <__TMC_END__>
	    10b7:       48 8d 35 72 2f 00 00    lea    rsi,[rip+0x2f72]        # 4030 <__TMC_END__>
	    10be:       48 29 fe                sub    rsi,rdi
	    10c1:       48 89 f0                mov    rax,rsi
	    10c4:       48 c1 ee 3f             shr    rsi,0x3f
	    10c8:       48 c1 f8 03             sar    rax,0x3
	    10cc:       48 01 c6                add    rsi,rax
	    10cf:       48 d1 fe                sar    rsi,1
	    10d2:       74 14                   je     10e8 <register_tm_clones+0x38>
	    10d4:       48 8b 05 15 2f 00 00    mov    rax,QWORD PTR [rip+0x2f15]        # 3ff0 <_ITM_registerTMCloneTable>
	    10db:       48 85 c0                test   rax,rax
	    10de:       74 08                   je     10e8 <register_tm_clones+0x38>
	    10e0:       ff e0                   jmp    rax
	    10e2:       66 0f 1f 44 00 00       nop    WORD PTR [rax+rax*1+0x0]
	    10e8:       c3                      ret    
	    10e9:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]

	00000000000010f0 <__do_global_dtors_aux>:
	    10f0:       80 3d 39 2f 00 00 00    cmp    BYTE PTR [rip+0x2f39],0x0        # 4030 <__TMC_END__>
	    10f7:       75 2f                   jne    1128 <__do_global_dtors_aux+0x38>
	    10f9:       55                      push   rbp
	    10fa:       48 83 3d f6 2e 00 00    cmp    QWORD PTR [rip+0x2ef6],0x0        # 3ff8 <__cxa_finalize@GLIBC_2.2.5>
	    1101:       00 
	    1102:       48 89 e5                mov    rbp,rsp
	    1105:       74 0c                   je     1113 <__do_global_dtors_aux+0x23>
	    1107:       48 8b 3d 1a 2f 00 00    mov    rdi,QWORD PTR [rip+0x2f1a]        # 4028 <__dso_handle>
	    110e:       e8 2d ff ff ff          call   1040 <__cxa_finalize@plt>
	    1113:       e8 68 ff ff ff          call   1080 <deregister_tm_clones>
	    1118:       c6 05 11 2f 00 00 01    mov    BYTE PTR [rip+0x2f11],0x1        # 4030 <__TMC_END__>
	    111f:       5d                      pop    rbp
	    1120:       c3                      ret    
	    1121:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]
	    1128:       c3                      ret    
	    1129:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]

	0000000000001130 <frame_dummy>:
	    1130:       e9 7b ff ff ff          jmp    10b0 <register_tm_clones>

	0000000000001135 <main>:
	    1135:       55                      push   rbp
	    1136:       48 89 e5                mov    rbp,rsp
	    1139:       48 8d 3d c4 0e 00 00    lea    rdi,[rip+0xec4]        # 2004 <_IO_stdin_used+0x4>
	    1140:       b8 00 00 00 00          mov    eax,0x0
	    1145:       e8 e6 fe ff ff          call   1030 <printf@plt>
	    114a:       b8 00 00 00 00          mov    eax,0x0
	    114f:       5d                      pop    rbp
	    1150:       c3                      ret    
	    1151:       66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
	    1158:       00 00 00 
	    115b:       0f 1f 44 00 00          nop    DWORD PTR [rax+rax*1+0x0]

	0000000000001160 <__libc_csu_init>:
	    1160:       41 57                   push   r15
	    1162:       4c 8d 3d 7f 2c 00 00    lea    r15,[rip+0x2c7f]        # 3de8 <__frame_dummy_init_array_entry>
	    1169:       41 56                   push   r14
	    116b:       49 89 d6                mov    r14,rdx
	    116e:       41 55                   push   r13
	    1170:       49 89 f5                mov    r13,rsi
	    1173:       41 54                   push   r12
	    1175:       41 89 fc                mov    r12d,edi
	    1178:       55                      push   rbp
	    1179:       48 8d 2d 70 2c 00 00    lea    rbp,[rip+0x2c70]        # 3df0 <__do_global_dtors_aux_fini_array_entry>
	    1180:       53                      push   rbx
	    1181:       4c 29 fd                sub    rbp,r15
	    1184:       48 83 ec 08             sub    rsp,0x8
	    1188:       e8 73 fe ff ff          call   1000 <_init>
	    118d:       48 c1 fd 03             sar    rbp,0x3
	    1191:       74 1b                   je     11ae <__libc_csu_init+0x4e>
	    1193:       31 db                   xor    ebx,ebx
	    1195:       0f 1f 00                nop    DWORD PTR [rax]
	    1198:       4c 89 f2                mov    rdx,r14
	    119b:       4c 89 ee                mov    rsi,r13
	    119e:       44 89 e7                mov    edi,r12d
	    11a1:       41 ff 14 df             call   QWORD PTR [r15+rbx*8]
	    11a5:       48 83 c3 01             add    rbx,0x1
	    11a9:       48 39 dd                cmp    rbp,rbx
	    11ac:       75 ea                   jne    1198 <__libc_csu_init+0x38>
	    11ae:       48 83 c4 08             add    rsp,0x8
	    11b2:       5b                      pop    rbx
	    11b3:       5d                      pop    rbp
	    11b4:       41 5c                   pop    r12
	    11b6:       41 5d                   pop    r13
	    11b8:       41 5e                   pop    r14
	    11ba:       41 5f                   pop    r15
	    11bc:       c3                      ret    
	    11bd:       0f 1f 00                nop    DWORD PTR [rax]

	00000000000011c0 <__libc_csu_fini>:
	    11c0:       c3                      ret    

	Disassembly of section .fini:

	00000000000011c4 <_fini>:
	    11c4:       48 83 ec 08             sub    rsp,0x8
	    11c8:       48 83 c4 08             add    rsp,0x8
	    11cc:       c3                      ret    

		
		]
