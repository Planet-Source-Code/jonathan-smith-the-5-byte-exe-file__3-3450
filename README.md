<div align="center">

## The 5 byte EXE file


</div>

### Description

This article is based on Vbmew's "make 7 byte .exes" (http://www.1cplusplusstreet.com/vb/scripts/ShowCode.asp?txtCodeId=2221&lngWId=3)

His article perked my interest in the Assembly language, so I went out and did some research. This article is a very brief primer on assembler and machine code.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jonathan Smith](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jonathan-smith.md)
**Level**          |Advanced
**User Rating**    |4.7 (61 globes from 13 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jonathan-smith-the-5-byte-exe-file__3-3450/archive/master.zip)





### Source Code

<p><i>Note: Before I begin, I realize this program isn't really C or C++. If
it's anything, it's assembler. I posted it to the C++ section because it's
closer to what I want to accomplish. Personally, I think an ASM section on PSC
is long, long overdue. So please, no complaining about this not being C or C++.</i></p>
<p><i>With having said that, let us begin.</i></p>
<p align="center"><b>THE 5-BYTE EXECUTABLE - A PRIMER ON ASSEMBLY LANGUAGE AND
MACHINE CODE</b></p>
<p>For starters, I'd like to create a program which is only 5 bytes in size and
does more than the 7 byte EXE that Vbmew shows how to create.</p>
<p>At a DOS prompt, type &quot;copy con echochar.com&quot;</p>
<p>The listing of the program is as follows (with the assembler code
explaination)</p>
<ol>
 <li><font size="2" face="Courier New">Press Alt-180<br>
 <i>Code B4, &quot;mov ah, ??&quot;. 'mov' is a symbol used to tell the processor to copy
 a value from somewhere into somwhere else. 'ah' is a CPU register. ah is
 commonly used with input and output routines. '??' is the value we want to put
 in to the ah register. We fill in the value of '??' in the next line.</i><br>
&nbsp;</font></li>
 <li><font face="Courier New"><font size="2">Press Alt-1<br>
 </font><i><font size="2">ASCII character 1. This makes the first line look
 like &quot;mov ah,1&quot;.<br>
&nbsp;</font></i></font></li>
 <li><font face="Courier New"><font size="2">Press Alt-205<br>
 </font><i><font size="2">Code CD, &quot;int ??&quot;. 'int' simply calls an interrupt.
 An interrupt is an instruction built in to the CPU.<br>
&nbsp;</font></i></font></li>
 <li><font face="Courier New"><font size="2">Press Alt-33<br>
 </font><i><font size="2">ASCII character 33. In hex, 33 is 21. This makes the
 previous line look like &quot;int 21h&quot;. Interrupt 21h is a commonly used IO
 interrupt. By setting the ah register to 1 and calling interrupt 33 (or 21h),
 we're telling the computer to stop and wait for input from the keyboard. Since
 ah is set to 1, once a key is pressed, it is echoed to the screen. If,
 however, ah was set to 8, the character pressed would *not* be echoed.<br>
&nbsp;</font></i></font></li>
 <li><font face="Courier New"><font size="2">Press Alt-195<br>
 </font><i><font size="2">Code C3, &quot;ret&quot;. 'ret' basically tells the computer to
 return to the previous environment.<br>
&nbsp;</font></i></font></li>
 <li><font size="2" face="Courier New">Press Ctrl-Z to mark the end of the file
 and the press Enter to write the file.</font></li>
</ol>
<p>Like Vbmew's program, this one displays a character to the screen.&nbsp;
Unlike his program, however, this one lets you<i> choose</i> which character is
displayed. =)</p>
<p>While this program basically does nothing, it's a great primer (for me, at
least).&nbsp; It gives an introduction as to what basic assembler commands do
what, and what their machine code representation is.</p>
<p>Here's the program again, this time, in all assembly.</p>
<blockquote>
 <p><font face="Courier New" size="2">mov ah,1<br>
 int 21h<br>
 ret</font></p>
</blockquote>
<p><font face="Times New Roman">To make this even more low-level, we could
eliminate the automatic display of the character to the screen and display it
with code instead. As stated earlier, to eliminate the character echo, the ah
register needs to be set to 8 instead of 1.&nbsp; After a key is pressed, is put
into the 'al' register, which is simply another register in the CPU which you
need not concern yourself with at the moment. Just know that it holds the ASCII
value of the key that was pressed and we need to put that value into the 'dl'
register, which is commonly used for output. To do this, we need to use totally
different symbols specific for moving registers to registers. One of these new
symbols are 88 and C2 combined. In fact, the 88-C2 command specifically copies
the value in the al register to the dl register. After performing this
operation, we need to tell the computer that we want to display the output. This
is done by setting the ah register to 2 and once again calling interrupt 21h.</font></p>
<p><font face="Times New Roman">I also recommend a unicode hex editor for this
as the DOS prompt will not suffice (because Alt-8 translates into backspace).</font></p>
<table border="0" style="border-collapse: collapse" bordercolor="#111111" width="100%" id="AutoNumber1">
 <tr>
  <td width="33%">
  <p align="center">Keyboard command</td>
  <td width="33%">
  <p align="center">ASM Code</td>
  <td width="34%">
  <p align="center">Machine Code</td>
 </tr>
 <tr>
  <td width="33%"><font face="Courier New" size="2">Alt-180, Alt-8 (can't be
  done at DOS prompt)</font></td>
  <td width="33%"><font face="Courier New" size="2">mov ah,8</font></td>
  <td width="34%"><font face="Courier New" size="2">&#9508;&#9688;</font></td>
 </tr>
 <tr>
  <td width="33%"><font face="Courier New" size="2">Alt-205, Alt-33</font></td>
  <td width="33%"><font face="Courier New" size="2">int 21h</font></td>
  <td width="34%"><font face="Courier New" size="2">&#9552;!</font></td>
 </tr>
 <tr>
  <td width="33%"><font face="Courier New" size="2">Alt-136, Alt-194</font></td>
  <td width="33%"><font face="Courier New" size="2">mov dl,al&nbsp;&nbsp;&nbsp;
  (this is the 88-C2 command)</font></td>
  <td width="34%"><font face="Courier New" size="2">ê&#9516;</font></td>
 </tr>
 <tr>
  <td width="33%"><font face="Courier New" size="2">Alt-180, Alt-2</font></td>
  <td width="33%"><font face="Courier New" size="2">mov ah,2</font></td>
  <td width="34%"><font face="Courier New" size="2">&#9508;&#9787;</font></td>
 </tr>
 <tr>
  <td width="33%"><font face="Courier New" size="2">Alt-205, Alt-33</font></td>
  <td width="33%"><font face="Courier New" size="2">int 21h</font></td>
  <td width="34%"><font face="Courier New" size="2">&#9552;!</font></td>
 </tr>
 <tr>
  <td width="33%"><font face="Courier New" size="2">Alt-195</font></td>
  <td width="33%"><font face="Courier New" size="2">ret</font></td>
  <td width="34%"><font face="Courier New" size="2">&#9500;</font></td>
 </tr>
</table>
<p>There you have it. An even more low-level program that does practically the
same thing as the first. And it's only 11 bytes in size, still. =)</p>
<p>I know this article might not be the hardcore &quot;we-don't-need-no-stinkin'-programming-language-we've-got-pure-machine-code&quot;
tutorial, but at least it's a start. I would recommend taking a look at
<a href="http://www.theteacher.freeserve.co.uk/alevel/assem/assemix.htm">
http://www.theteacher.freeserve.co.uk/alevel/assem/assemix.htm</a> for more
information on assembly language and CPU architecture, and I'd also recommend
W32Dasm and NASM for writing programs in assembly and finding out what the
symbol codes are.</p>
<p>Also, don't forget to vote for an ASM section for PSC!</p>

