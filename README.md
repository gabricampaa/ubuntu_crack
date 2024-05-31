# Ubuntu ISO crack
A simple walkthrough for hacking the iso image of Ubuntu.

This process is just an experiment, and i will take no responsability for improper actions or a harmful usage.

Also, keep in mind i'm using macos, therefore a few steps will be specific (but i'm working on making this "cross os") 


# STEPS
- Let's download the iso image for ubuntu.
- Decompose the iso using "theUnarchiver". this will give you a folder containing various subfolders, like boot/, casper/, install/, ...
- In the folder "casper", you will find the compresseed linux filesystem under the name "filesytem.squashfs". use unsquashfs to decompress it and access the raw files
- Edit the files as you wish. For example, under the path "/var/log/" i create an executable called "foo", which i then put under the auto execute commands at startup.
- Recompress the NEW filesystem with 
  ```bash
  mksquashfs foldername filename.squashfs
  ```
- Substitute the old filesystem.squashfs with the new one (keep the same name)
- Generate the new iso image from the master folder:
  ```bash
  genisoimage -o ubuntu_desktop_20.iso -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -J -R -V Ubuntu\ 20.04\ Desktop -input-charset utf-8 .
  ```


