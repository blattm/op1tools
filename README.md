# OP1 Tools for Linux

## Features
This software can do multiple things:
- Generate sound preview for OP-1 synthesizer patches 
- Backup the whole OP-1 or just the user-synth folder
- Count how many patches are on your OP-1 and how close you are to the limits
- OP1 USB handling: detecting OP-1, mounting, ejecting, ...

The main feature of this tool is the 'label' function. It allows you to convert OP-1 synthesizer patches, that simply say 'OP-1 PATCH' to synthesizer patches that include a short preview of the sound. To do this, patches are transfered to your OP-1 via usb, processed there, and transfered back. This overrides the 8 user-synths, so you should use it like this:

./op1 backup-user-synth path/to/backup/folder

./op1 label path/to/my/patches

./op1 restore-user-synth path/to/backup/folder

For more details see 'usage'.

## How are the preview sounds generated?
The OP-1 stores synthesizer patches in the metadata of .aif files. But there are two different ways: Either an .aif file, that says 'OP-1 PATCH' or in an .aif file that contains a short preview of the sound. All synthesizer patches stored on the OP-1 are in the former format, except the 8 user patcher, which are stored in the latter format. So the label function of this tool just copies 8 files without preview from your PC to the user synth folder, waits for you to restart and reconnect the OP-1, and copies the files, which now contain a sound preview, back to your PC. This will be repeated until all patches are processed.

## Requirements
This bash script for linux requires udisks2, which is probably already installed on your system.
Also to be able to use all features, please add your user to the disk group of your system, via

sudo usermod -a -G disk YourUserName

Alternatively the label and eject commands need to be run with sudo. (Not recommended)

## No Warranty
This software is distributed under the MIT license, i.e. without warranty of any kind. For details, see license.

## usage
usage: ./op1 command ...

The commands are

### count
Counts how many patches are on your OP-1 and how close you are to the limits

### label infolder [outfolder]
Uses the OP-1 to add sound samples to all OP-1 patches in the folder specified via infolder. If no outfolder is given, results are saved in infolder_labeled. WARNING: THIS ACTION WILL OVERWRITE YOUR synth/user FOLDER ON THE OP-1. Please use backup-user-synth and restore-user-synth before resp. after using this command!

You have to run the command with sudo (not recommended) or add yourself to the disk group, via

sudo usermod -a -G disk YourUserName

### backup-user-synth [folder]
Backups the synth/user to the specified folder. "
If no folder is given, the backup will be placed in backup_user_synth

### restore-user-synth [folder]
Restores synth/user from the specified folder. If no folder is given, the backup will be taken from backup_user_synth

### backup [folder]
Backups the whole OP-1 to the specified folder. If no folder is given, the backup will be placed in current folder

### status
Returns the USB connection and mount status of the OP-1

### mount
Mounts the OP-1

### eject
Ejects / savely removes the OP-1.

You have to run the command with sudo (not recommended) or add yourself to the disk group, via

sudo usermod -a -G disk YourUserName

### wait
Wait until the OP-1 is connected via usb.

### wait-mount
Wait until the OP-1 is connected via usb. Then mount the OP-1

### folder
Return the OP-1's folder if its mounted.

### folder-mount
Return the OP-1's folder. Mount the OP-1 if necessary.
