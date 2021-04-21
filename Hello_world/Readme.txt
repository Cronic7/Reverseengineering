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
