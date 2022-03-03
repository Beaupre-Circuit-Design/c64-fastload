# EPYX FastLoad &trade; Cartridge for COMMODORE 64 &trade; Instruction Manual
Program Designed by Scott Nelson

## GETTING STARTED

1. Set up your Commodore 64 &trade; as shown in the Owner's Manual.
2. Make sure your computer is turned OFF.
3. Insert the FastLoad CARTRIDGE &trade; into the cartridge slot of your computer.
4. Turn the computer ON.
5. Turn the disk drive ON.
6. Insert your program disk.

**NOTE**: There is no need to remove the FastLoad CARTRIDGE once inserted. FastLoad will work on most protected disks and in intended for use with the Commodore 64 &trade; 1541 disk drive.

## USING FastLoad

After turning the computer ON, the word "FASTLOAD" will appear just below the Basic READY prompt.

* To list a directory without erasing the program in memory, type **\$** or **>\$**.
* To run most disk software, hold down the Commodore key (**C=**) and press the **RUN/STOP** key.
  * This will eliminate typing **LOAD "*",8,1** and then typing **RUN** each time you load.
* To load a basic program, type **/FILENAME**.
  * This will eliminate typing **LOAD "FILENAME",8**.
* To save a basic program, type **\FILENAME**.
  * This will eliminate typing **SAVE "FILENAME",8**.
* To load a machine language file, type **%FILENAME**.
  * This will eliminate typing **LOAD "FILENAME",8,1**.
* To send a command to the disk drive, type **@COMMAND** or **>COMMAND.**
  * This will eliminate typing **OPEN 15,8,15,"COMMAND":CLOSE 15.**
* To read the error channel (when the red light on the disk drive is flashing) type **>** or **@**.


## DISK TOOLS

To run the disk tool, type the British pound key (**&pound;**).  Press the appropriate letter for your desired function.

    A  DIRECTORY         This will show a directory of the diskette.
    --------------------------------------------------------------------------------
    B  RETURN TO BASIC   Will return to BASIC, leaving FASTLOAD intact.
    --------------------------------------------------------------------------------
    C  COPY              Selecting this option will give you another menu:

        A  DIRECTORY                 This will list the directory.
        B  RETURN TO THE FIRST MENU  This will return you to the first menu.
        C  COPY ENTIRE DISKETTE      Will copy every sector of one diskette to

                                     another diskette. Note: the new diskette must
                                     be formatted for this option to work properly.
        D  BAM COPY                  Will copy only those sectors on a diskette 
                                     which have been allocated by the DOS.  This is
                                     much faster than copying the entire diskette.
                                     Note: The new diskette must be formatted for
                                     this option to work properly.
        E  COPY A FILE               Will copy a program file from one diskette to
                                     another.  Wild card characters (* or ?) are 
                                     allowed in the file name.
        F  FORMAT DISKETTE           Will erase a diskette.  This option should be
                                     used before a BAM copy or an entire disk copy
                                     is attempted.  Note:  This will erase any files
                                     on the disk.
    --------------------------------------------------------------------------------
    D  DISABLE FASTLOAD  This will disable FastLoad and return you to BASIC. Once
                         this option has been selected, the only way to use FASTLOAD
                         is to turn the Commodore 64 Computer Off and ON again.
    --------------------------------------------------------------------------------
    E  EDIT DISK         Selecting this option will give you a new menu:
    
        EDIT DISKETTE        TRACK 12     SECTOR 02
        READ WRITE  QUIT

    First, you must enter the track and sector you wish to edit in hex. (If you
    prefer decimals, type a "#" before the number.) Then you will see that sector
    displayed before you.  To change a byte, enter the new value in hex.
    To move within a sector, use the cursor keys.  To read a sector, type "R". 
    To write a sector, type "W".  To quit, type "Q".
    --------------------------------------------------------------------------------
    F  FILE UTILITY      Selecting this option will give you a new menu:

        A  DIRECTORY                 This option will list the directory.
        B  RETURN TO THE FIRST MENU  This will return you to the first menu.
        C  COPY A FILE               This will copy a program file from one diskette
                                     to another.
        D  DELETE A FILE             Will remove a file from the directory.
        E  LOCK A FILE:              Will "lock" a file, making it impossible to 
                                     delete the file without first unlocking it. A
                                     locked file will have a "<" after it in the
                                     directory.
        F  UNLOCK A FILE             This will unlock a file, making it possible to
                                     delete it.
        G  RENAME A FILE             Allows you to change the name of a file.


## ADVANCED PROGRAMMING
 
For advanced programmers, the following are assembly monitor instructions:

### SMON
In addition to the above tools, the FastLoad CARTRIDGE contains a powerful monitor.  Since the major use of a monitor is to "debug" assembly language programs, if you are not familiar with this, you may want to skip this section. To move into the monitor, type "!".

### SYNTAX
A command in SMON is usually entered as several arguments followed by a single command character.  The command character can usually be placed anywhere on the line, therefore __800,850\*__ is the same as __800\*850__ or __\*800 850__.  Commas, periods, and spaces may be typed anywhere, and serve only to separate numbers.  Numbers may be entered in hex (the default), decimal (by preceeding it with a __#__), or as ASCII by typing a single quote before it, or as a lot of ASCII by surrounding many characters with double quotes.  Numbers may also be combined with any of the five following operators: __&__ (logical and), __!__ (logical or), __?__ (logical exclusive or), __+__ (plus), __-__ (minus), __(__ (left parenthesis), and __)__ (right parenthesis). For example:

     (11+4)&(5!1E?1)-#10 = A
             (15)&(1E)-A = A
                    14-A = A

__0000G:__  Begins execution of M.L. code at location 0000 via JSR.

__0000 1111H22 33 44 55 . . . :__  This command hunts for a sequence of bytes.  0000-1111 is the memory which will be searched.  22 33 sets the range between which the first byte will be accepted, 44 55 the second, and so on.  For example 0 1000 H A9 A9 80 90 will search for an A9 followed by something between 80 and 90. Up to 10 bytes can be
searched for.

__0000J:__  Begins execution of M.L. code at location 0000 via JMP.

__00 11 2222 3333I:__  Will disassemble memory at 2222-3333 and print all immediates between 00 and 11.

__0000 1111L:__  Will disassemble memory at 0000-1111 and print it to the screen.

__0000 1111 2222M:__  Will move a block of memory at 1111-2222 down to 1. The move instruction always moves the lowest byte (1111) first, so some moves may not work correctly.  For example: 4000 4001 8000M will not move the block up one byte, instead 4000 will be moved to 4001, then from 4001 to 4002.  Thereby filling 4001-8001 with the byte in 4000.

__N:__  No operation.

__0000 1111 2222 3333 4444Q:__  To relocate.  Takes the code at 3333-4444 and changes all absolute addresses in the range 1111-2222 by 0000 (subtracts 0000 from it).

__0000 11 R"SSSSSSSS":__  Binary load from device 11.  If 0000 is specified, then this will load the file SSSSSSSS into memory at location 0000. If not specified, then it will load where it was saved. The R" MUST be located just before the filename.

__0000S:__  Executes one M.L. OP-CODE, then displays the contents of the registers.  0000 is the address of the OP-CODE to execute, or just "S" will continue with the next instruction.  For example: 600S will execute the instruction at 600.  S will execute the one after 600.

__0000T:__  Begins execution at 0000 and displays registers after each instruction.

__0000 1111 2222 V:__  Checks the block 1111-2222 against the memory starting at 0000 if the location contents differ.  Then it will print both contents.

__0000 1111 22 W"SSSSSSSS":__  Binary save.  Saves the memory 0000-1111 (inclusive) in the file SSSSSSSS an device 22.

__00 11 2222 3333X Y @:__  Disassembles block at 2222-3333 and prints indirects between 00-11.  X will only print indirect X (,X). Y will only print indirect Y (),Y.  @ will print all indirects.

__0000 1111 2222 3333Z:__  Disassembles block 2222-3333 and prints all absolute or zero page references in the range 0000-1111.  These include references from branches.

__\> . , :__  These are separaters, and are ignored.

__0000 1111*:__  Displays memory from 0000 to 1111 in HEX and ASCII.

__0000 1111^:__  Prints the ASCII of memory from 0000-1111.

__#AA XX YY PP SP:__  Display registers.  If followed by numbers, then those numbers are stored in those registers.  To change X, it is necessary to change A as well.

__%:__  Returns you to Basic.

__\>"COMMAND":__  Emulates the Basic command, OPEN 15,8,15,"COMMAND"

__$:__  Prints a directory.

__0000=:__  Prints the HEX, DECIMAL, BINARY, and ASCII value of 0000.
