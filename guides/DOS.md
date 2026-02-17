# Running DOS on your 9110 Communicator

**Original author:** David Chapman  
**Updated by:** Luca Cassioli (2003)  
**Source:** https://win98.altervista.org/9110/dos9k/aboutdos.html

This guide provides background and technical information for running DOS on a Nokia 9110 Communicator.

> **WARNING:** These instructions should only be attempted by users confident with the DOS command line and willing to accept the risk of data loss. Running untested DOS programs may permanently damage the device. Proceed at your own risk.

> **⚠️ ALWAYS BACKUP BEFORE EXPERIMENTING!!!**

> **NOTE:** These instructions have only been tested on the Nokia 9110. They will not work on the 9000 due to lack of a keyboard driver available to DOS programs.

## Introduction
GEOS, the 9110's operating system, runs on top of Embedded DOS-ROM by General Systems Inc., which is mostly compatible with MS-DOS. In addition, the 9110 also has a mostly PC-compatible BIOS, making the 9110 a suitable platform for running "well-behaved" DOS programs that perform all I/O using DOS and BIOS routines.

## How to Run DOS on the 9110

The 9110 boots by running an AUTOEXEC.BAT file (from ROM) that performs initialization steps before launching GEOS. Nokia includes a mechanism for installing software before GEOS loads through an INSTALL.BAT file, which is executed just before GEOS loads and then deleted. To run a DOS program, create an INSTALL.BAT that runs the desired program and install it in the B:\NOKIA directory. Note that INSTALL.BAT is automatically deleted after execution, requiring a new copy to be installed each time a DOS program is to be run.

When DOS starts, a Command Interpreter (command.com) provides the C:\ prompt from which programs can be launched. This interpreter is the primary tool for exploring the 9110's filesystem using standard DOS commands (dir, copy, del, rd, md, etc.) and launching other DOS programs. Standard MS-DOS or Windows versions of command.com will not function on the 9110 due to version checking. However, alternative command interpreters that do not perform version checking are compatible with the device.

A GEOS application called DOS Prompt Launcher is available to automate these steps. The package includes a compatible command.com from the FreeDOS project and can be installed on the 9110 and run from the Extras menu. Once executed, the device reboots and displays the DOS prompt.

### Using DOS Prompt Launcher

DOS Prompt Launcher simplifies the process of running DOS by automating the setup steps required to load DOS on the 9110. When installed, the application creates two files: a `command.com` file placed in the B:\NOKIA directory and the `DOSPRMPT.GEO` GEOS application installed in the Extras menu.

To run DOS, select "Run DOS" from the DOS Prompt Launcher menu. The application looks for an `INSTALL.BAT` file in the Own Texts directory. If this file does not exist, the launcher automatically creates a default version:

```
text on
if not exist b:\nokia\do_inst goto quit
del b:\nokia\do_inst
b:\nokia\command.com

:quit
```

The default `INSTALL.BAT` uses a temporary file (`do_inst`) to ensure that `command.com` runs only once. This safety measure prevents a corrupt `command.com` from running repeatedly and preventing `AUTOEXEC.BAT` from deleting `INSTALL.BAT`, which would otherwise require filesystem reformatting to recover GEOS.

The `INSTALL.BAT` file can be customized to change the location of `command.com` or to launch other DOS applications. It is recommended to retain the `DO_INST` check when modifying `INSTALL.BAT`. Note that `INSTALL.BAT` is a DOS-style ASCII text file and cannot be edited using the 9110's Notes application. Use a DOS-based text editor on the 9110, edit on a PC in ASCII text format, or use a GEOS application capable of modifying such files (e.g., FreeBas9k).

Once `INSTALL.BAT` exists in the Own Texts directory, DOS Prompt Launcher initiates DOS execution by copying the file to B:\NOKIA, creating a zero-length file called B:\NOKIA\DO_INST, and rebooting the 9110.

## Limitations of DOS on the 9110
In addition to the lack of 100% PC compatibility most of the basic functionality of the phone and PDA is built into GEOS. Therefore, these features are not available in DOS.

The phone side of the 9110 relies on communication with the PDA side (i.e. GEOS) to operate correctly. Therefore, nearly all of the phone's functions fail to work in DOS. The contacts database is unaccessible, but you can still make and receive voice calls, although without your custom rings. Once you exit DOS and GEOS is loaded, your phone returns to normal.

Most DOS programs attempt direct video hardware access, which is incompatible with the 9110's non-standard display (640x200x16 graphics mode with no hardware text mode). A video driver for DOS9k is required for full compatibility.

The display does not show a text cursor. A "cursor driver" must be installed to address this limitation.

Keyboard mappings are incorrect by default, and certain characters are inaccessible. Additionally, the backlight cannot be activated and screen zoom cannot be adjusted—the font size is very small. A keyboard driver can resolve these issues and is configurable for users with assembly programming knowledge.

Ongoing projects seek to address these limitations. Developers with low-level DOS programming experience are encouraged to contribute. Improvements will be integrated into future versions of the DOS Prompt Launcher.

## Compatible Applications

Despite the aforementioned limitations, numerous useful DOS applications can run on the 9110 without additional utilities. Refer to the downloads page for a list of compatible software.

Command-line DOS programs are generally compatible with the 9110. Full-screen text applications may work if they use BIOS for screen access, but graphics programs are not supported. Graphics-intensive applications such as games will not function on the device.

---

**For more information and original source material:** https://win98.altervista.org/9110/dos9k/


