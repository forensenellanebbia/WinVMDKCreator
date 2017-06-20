# WinVMDKCreator
WinVMDKCreator

WinVMDKCreator - BETA
by Dana McNeil

DESCRIPTION
This application creates a VMDK file from data associated with DD (RAW) disk images.  This allows a user to then mount the disk images in VMware Workstation or other applications supporting this format. The applicaton will automatically check to see if the disk images are segmented and calcuate the appropriate information necessary for the VMDK file.

CREDITS/AKNOWLEDGEMENTS
The application is based upon the excellent information provided by Agent Jimmy Weg, chief forensic examiner with the state of Montana Department of Criminal Investigation.  Agent Weg has an excellent blog at http://www.justaskweg.com.  Check it out!  Many thanks Jimmy for your ongoing advice and support to the forensics community.

USE:

Simply click the elipsis ("...") button and select the FIRST segment of the DD (RAW) disk image file. (e.g. d:\data\diskImages\MyDiskImage.001). 

The application will automatically scan files in the directory with the DD image you specified for a disk descriptor file.  A disk descriptor file is often created automatically by forensics tools such as FTK Imager and XWays Forensics, and it contains important information about the geometry of the imaged disk.  The application can use this file to "double check" calculations and help ensure the resulting VMDK file is correct.  You have the option of disabling this verification by checking the respective checkbox. This is recommended if you have the file, but optional.  This feature currently only works with disk images created with FTK Imager (3.1) and X-Ways Forensics (16.4).

If the application doesn't locate your disk descriptor file, you have the option of spefiying one elsewhere.  Simply click the elepsis "..." and specify a different location.  The application will NOT attempt to validate a user specified file.

Check the checkbox "Set disk image attributes to Read Only." to automatically change the NTFS file attributes to READ_ONLY.  This is a useful forensic safeguard to help reduce the chance that any change is made to the images.  This is optional.

Select the ouput format (compatibility with Workstation 8 or 9).   

You can optionally change the name of the VMDK file, although it will automatically name it the same name as the image file.  Do not include the .VMDK extension.

Click "GENERATE"!

The application will automatically scan through the directory to identify if any other segments are present.  The application doesn't care if there are multiple segments or a single segment.  The application will output the .vmdk into the directory alongside the disk image(s).


By default, the applicaiton will create a very brief log file in the directory with your .vmdk.  

Let me know if you you have questions or issues.  I'd be happy to hear from you. 

Dana McNeil

REVISION HISTORY:


.8.2.1 - Fixed a major bug causing a crash/fail when using XWF descriptor files during the creation of the .vmdk.  This was caused due to the lack of a difference in the way either FTK or XWF defines the location of the total sectors. A workaround was created so the process first checks for filenames of supported disk descriptor files, AND provides the user to specify one.  A flag now defines if, during creation, the system should use an automatically found image file, or the user specified one.  If the user specifies one, the system first tests it as an FTK descriptor, then XWays.  Failing all these the system DEFAULTS TO XWF and will attempt to read the file.  As always, should the process fail, the user can simply elect to not use the descriptor file.  Confused yet?

Downgraded the required framework from 4.0 to 3.5 which caused major issues all over the place.  These were addressed and appears to be stable now.  This should allow a client profile on standard windows Vista installations or newer.

.8.0.1 - Major re-work of the way the image descriptor file is used.  The user now has the option to specify thier own disk descriptor.  The application will still attempt to find valid descriptor files.  This eliminated a lot of code which did some image verification, but the application is now more flexible.  This required a major rework of how the whole process works.

The ability for users to modify sector sizes has been removed.  It was ultimately determined this is currently an unnecessary due to legacy compatability anyway, and probably just confusing.

Minor changes to some of the titles of forms and other language issues.

.7.3.X - Added the ability for a user defined sector size to be used in calculations.  Added custom preferances files to support this feature.

.7.2.3 - Minor change to the phrasing of the image hasing verification file (previously referred to as the disk descriptor file);
The system will now clear the output window each time you attempt to create a new file.

.7.1.3 - Updated the system to have a checkbox in the UI to give the option to automatically create an activity log upon completion.
Some minor changes to the way the system handles processing files.
Updated Thank You page to allow it to automatically send via default client.
Cosmetic code changes.
Beta Release.

.6.2 - Tooltips added.
"Thank you" window on close down.

.6.1 - Many code changes and improvements.
Some of the larger function calls now go to the VMDKCreatorLib.dll.  
Changed the way the application verifies the total sectors of the file and it will now primarily rely on the totals calculated from each segment rather than the disk descriptor file.  
Incorporated the option to use the descriptor file for "double check" of calculated sectors.  The user may now elect to not use the descriptor file in the creation of the .vmdk.
Incorporated the abiltiy to set all the segments to READONLY during the process.
Several error checking routines added.
The sysem will now log if any errors were encountered during the process, even if the .vmdk file is created.
Jumped to Version 6 as this appears to be nearing release.

.5.3 - Many code changes to incorporate VMDKCreatrLib.dll to handle parsing of data.

.5.2.1 - Added system sound on .vmdk creation.  

.5.2 - Added error checking to total sector counts.  The system now compares the running total of bytes in the segments and compares it against data within the descriptor file.  The system will warn the user if there is a mismatch.  The user has the option to continue or not.

Cosmetic stuff.

Fixed references to templates in the deployed version.

.5.1 - Cosmetic changes.  Added the about box.
