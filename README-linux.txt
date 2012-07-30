
                       Quake III Arena Point Release
                             July 26th, 2001


       TABLE OF CONTENTS

       i What's new

       1 System Requirements
       2 X11 Setup 
       3 Sound Setup
       4 Playing The Game
       5 Reporting bugs and getting help
       6 Contacting id Software


-------------------------------
(i) What's new
-------------------------------

Linux Quake III Arena and Quake III: Team Arena is maintained by Id software. Please send feedback for this release to ttimo@idsoftware.com.

Discuss Quake III Arena for linux on the Quake3World forum:

  http://www.quake3world.com/forum

See the INSTALL file for installation instructions.

Tips and current issues for Quake III Arena linux are listed at:
  http://zerowing.idsoftware.com/linux

Changes
-------

Changes for 1.31:

 - fix to the quake3 wrapper scripts (sends back the correct return value)
 - sound compatibility fixes
 - added quake3.xpm icon
 - fixed "Driver > System > Driver info" crash if you have too many
   GL extensions
 - fixed hanging when being run with a non-interactive tty (ex. xqf &)

Changes for 1.29g beta:

 - a single installer for graphical installation / console installation,
   no longer distributing a seperate console installer
 - fixed filesystem issues:
   showing ~/.q3a mods and mod descriptions
   finding files for autodownload in the right places (server)
 - keyboard fixes:
   fixed "sticking keys" problem with the ctrl key
   fixed console toggle on French keyboards
 - fixed screenshots overwriting each other between runs
 - NEW: "tty" console on dedicated server:
   an interactive prompt has been added to the dedicated server, it will
   perform auto-completion and command history as does the in-game console
 - brightness slider / XF86 gamma setting (if supported by your X server)
 - fixed rcon status issues
 - binded K_MOUSE4 and K_MOUSE5 (linux)

Changes for 1.27r beta:

 - linux source for 1.27i merged into the main source tree at Id
 - fixed duplicate mods in mod selection dialog

Known issues for 1.27g Beta1:

 - XFree86 4.x DGA 2.0 support not yet added
 - brightness slider not yet fixed
 - fraglimit/timelimit do not get propagated properly (also Win32)
 - sound artifacts (double sounds) in menu
 - framerate drops in video playback, sound artifacts
 - keyboard only traversal of TA menu broken (also Win32)
 - some GL drivers segfault on exit(0)
 - shoot instead of pain/hit animation 
 - failure to load head for body (baseq3/)

Bugs fixed since 1.17:

 + autodownload workaround
 + mods menu
 + case insensitive demo loading (q3_ui/, not in QVM yet)   
 + first version of joystick support added
 + r_logfile GL log works again
 + Linux DLL loading bug


-------------------------------
(1) MINIMUM SYSTEM REQUIREMENTS
-------------------------------

  * Linux kernel version 2.2.9 or above, glibc-2.1 or above
  * XFree86 SVGA server version 3.3.5 or above, running at 16 bpp depth
  * Pentium 233MHz MMX processor with 3dfx 8 MB Video Card
     or Pentium II 266MHz processor with 3dfx 4 MB Video Card
     or AMD 350MHz K6-2 processor with 3dfx 4 MB Video Card
  * 64 MB RAM
  * 4x CD-ROM drive (600 KB/sec sustained transfer rate)
  * OSS compatible sound card
  * Hard disk drive with at least 480MB of disk space.

  Multiplayer Requirements
  * Internet and LAN (TCP/IP) play supported
  * Internet play requires a 28.8 Kbps (or faster) modem

A 100% full OpenGL compliant 3-D video card and Linux driver is 
required. Quake III Arena uses the OpenGL API for 3-D hardware 
acceleration. There is no software-only version of the game. If
your computer is not hardware accelerated with a game compatible
graphics card, you will NOT be able to run Q3A. Currently,
only standalone drivers for 3dfx based cards are included with
demo and point release distributions.

For updates on GL drivers, in particular for the Matrox G200/G400,
see http://www.lokigames.com/support/gldrivers/.

Please follow the installation instructions presented there for adding the
correct drivers for your 3D-acceleration card.

NOTE:  Linux Q3A will try to load "libGL.so" before using other drivers,
and it will ignore libraries from the quake3/ directory if executed
with root privilege. This can cause problems if you have a software or 
third party OpenGL driver installed.

You can specifically target e.g. the included 3dfx based Mesa driver,
by using the following command line:

	quake3 +set r_gldriver libMesaVoodooGL.so.3.2

For 3dfx users, you may disable the vertical sync refresh.  This can improve
proformance at the cost of some visual tearing of the image.  Entering the
following command into your shell before running Linux Q3A Demo will turn off
the vertical sync:

	export FX_GLIDE_SWAPINTERVAL=0

Then run Linux Q3A from the same command line normally.

A glibc compatible Linux installation is required.  An easy to determine
if you have glibc support is to type this:

	ls -l /lib/libc*

If you get a report of libc6 (you may also have libc5), you have a glibc 
based system. The binaries were created on a Mandrake 7.2 (glibc-2.1.3) system.


--------------
(2)  X11 SETUP
--------------
Linux Q3A requires X11 to run. There is no console-based version as in
previous id products such as GLQuake and Quake2. XFree86 version 3.2 or
later is required.

There are two ways that mouse input is handled under XFree86:

        o By default, Q3A Demo will attempt to use DGA mouse handling. DGA
          support features direct reading of the mouse motion and provides
          more accurate control while playing the game. By default this
          support is enabled, but can be disabled by adding 
           "+set in_dgamouse 0" 
          to the command line at startup. This is recommended if you are
          using a Voodoo3 and are experiencing black screens, lockups,
          or mapping of mouse input to key events. This bug should be
          resolved on XFree86 SVGA 3.3.5 (except for a blue mouse cursor
          you might notice on the initial fullscreen frame). DGA mouse
          support does not require root privilege.

        o The non-DGA method of mouse input uses pointer grabbing and warps
          the pointer to the middle of the window on each mouse update. On
          systems with a slow frame rate and a lot of mouse user input, the
          motion can get "clipped" to the window boundaries. This method of
          input is more compatible however.

Q3A uses the XFree86 VidModeExtension facilities if available to provide
fullscreen play. This does not apply to 3dfx passthrough cards, since
the passthrough cable takes over the video display upon activation anyway.

When configuring your X11 server, make sure that you include lower
resolution modes such as 640x480 and 800x600. Q3A will auto-switch to
these modes using the VidModeExtension if you select fullscreen from the
graphics options menu. If the lower resolution modes are not listed in the
XFree86 configuration file, Q3A will be unable to switch to the desired
resolution for fullscreen play. Instead, it will using Mesa's software mode
to render into a window (very slow), or might fail to run at all, possibly
putting you in a different video in X11 on exiting.


---------------
(3) SOUND SETUP
---------------
Q3A uses the /dev/dsp sound device for sound support under Linux. This 
is the default device provided by the sound drivers included with the Linux
kernel. Please note that at the time of this writing, PCI based sound cards
such as the SoundBlaster Live and Diamond Monster MX series were not
supported. They may be supported in the future. Check
   
  http://www.opensound.com/ 

for support in the future.

You should make sure that the permissions for the /dev/dsp device are read 
and write for your current user ID. Some systems re-assign the owner and
reset to 644 on login. A simple way to get access is to do

  "chmod o+rw /dev/dsp" 

as root. For the more security conscious, a special sound group could be 
created and Q3A could be made setgid to the sound group to access the 
device.

Q3A uses mmap() to map the sound buffers on /dev/dsp directly in order 
to provide responsive sound needs. Sound cards must be able to support this
feature in order to work. SoundBlaster 16, AWE32 and AWE64 cards are known
to work.



--------------------
(4) PLAYING THE GAME
--------------------

By the time you read this, you will probably have succeeded in installing
from the self-extracting archive.

It is recommended that you do not run Q3A using the root account or 
with root privileges. There are two exceptions to this:

        o If you are using a 3Dfx based accelerator card and do not install
          the /dev/3dfx configuration option. (You will have to run as root
          in order to access the card).
        o If you do not have access to the /dev/dsp device and do not wish
          to change the mode of the device so that non-root accounts can
          access it.

You will have to be running under X11 or have the DISPLAY variable pointed
to a OpenGL glX capable X Server.

By default, Q3A tries to find the following OpenGL libraries in this
order:

        o libGL.so

You can override the library name by entering, "+set r_gldriver <libname>"
on the command line. This may be needed if you are using a non-standard set
up and have a different name for the OpenGL shared library. If you do not
specify a valid GL library, or if the GL library specified can't find or
access the hardware it expects, Mesa might fall back into slow software
rendering mode (usually in a window).

If everything proceeds successfully, you should have a Q3A Demo window on 
your desktop with a menu displayed (3dfx card owners will get a full screen
view). If you want to use full screen, go to the System Configuration, 
Graphics, Options, Fullscreen, change the value to Yes, and hit enter to 
apply it.

If you intend to connect to the Internet to play Q3A Demo, make certain
that your net connection is open and working first.

The first time you run Quake III Arena it will create a .q3a/ directory 
in your home directory.  Saved games and preferences will be stored here.

The demo offers an optional install of the HTML version of the manual, 
and more technical details on how to use Linux Quake III Arena. See
the Help/ folder. Point release updates and dedicated server only packages
do not contain the full manual.


-----------------------------------
(5) REPORTING BUGS AND GETTING HELP
-----------------------------------

The latest FAQ with Linux known issues lives at

  http://zerowing.idsoftware.com/linux

For additional information, please see the FAQs maintained by id Software

  http://www.quak3arena.com/faq/

Check the Quake3World forum for discussion of Linux Quake III Arena:

  http://www.quake3world.com/forum

--------------------------
(6) CONTACTING ID SOFTWARE
--------------------------
If you encounter a bug in Q3A, particularly those involving
video or network bugs, please email a description of the bug to

  feedback@quake3arena.com 

Please do NOT send reports to individual id employees.

In your subject line, please describe the system the game is being played
on (Mac, Linux, Win32) and the type of problem you are reporting: video,
network, sound or game. Example Subject Line:  "Mac/video problem" or
"Linux/network connection problem."

In the body of your letter (no attached files please), briefly list and
describe the problems.  Detailed descriptions of problems are good, but
remember that brevity is best. Please do NOT send screen shots unless
they are the ONLY way to show a problem.

While we realize that you may have comments and suggestions regarding
specific game play features, please refrain from submitting such along
with bug reports. Comments on game play can be made on the official
Quake 3: Arena message board at:

    http://www.quake3world.com/forum
    
- enjoy!
