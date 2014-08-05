panoptes
========

*Panoptes* (Ancient Greek: Πανόπτης; English translation: "the all-seeing")


### What it it?
=======

Operating system integrity checks made easy.

### How does it work?

##### First run:
Script parses paths specified in the variable and provided by command line argument and creates a hashes (currently sha256) of all files it finds. Additionally it saves the size and modification date of the file.


##### Next runs:
Script parses paths specified, lists all files and creates their hashes. Hashes are then compared with those generated by previous run. If hash does not matches - fail is generated. If all hashes match - system integrity check is passed.

### Capabilities:
There are multiple arguments that can be used to modify the script behavior.
 - `-p --path` is accepting paths as an extension to those specified in the paths variable inside the script
 - `-v --verbose` causes script to show all files that passed the check. By default only failures are displayed.
 - `-d --details` causes script to show details of failures. Details contain hashes (truncated), dates and sizes of files.
 - `-o --override` allows to force the script to override the database, saving new index as database.

```
usage: panoptes.py [-h] [-v] [-d] [-o]
                   [-p [additional_paths [additional_paths ...]]]

panoptes.py [-v | --verbose | -s | --silent | -p | --paths ]

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         Show output for files that passed the integrity check.
  -d, --details         Show detailed output for files that failed integrity
                        check.
  -o, --override        This forces the creation of new database if some files
                        will generate new hash values.
  -p [additional_paths [additional_paths ...]], --path [additional_paths [additional_paths ...]]
                        Include additional paths.
```

### Example output

Failure:

![Panoptes failure. File modification detected](https://raw.githubusercontent.com/mnmnc/img/master/panoptes.jpg)

Success with `-v`

![Panoptes success with verbosity.](https://raw.githubusercontent.com/mnmnc/img/master/panoptes2.jpg)

### Message types

 - FAIL - Failure
 - SUCC - Success
 - INFO - Notice
 - WARN - Warning
 - CHCE - Choice given
 - FOVR - Forced override (`-o` option used)

### Database
Database is a simple csv file. Example content (`file_path`,`sha256`, `date`, `size`):
```
"/bin/sh","bd07bdf3f6b871598977df9867eb59905511711c398bdc485734abc296762185","Fri Jan 10 11:14:07 2014","117176"
"/bin/mt-gnu","8347fa915b1b0e372349e208f7ebf88201fc06888e85e76779dc318230dc3660","Thu Mar 27 04:34:02 2014","68760"
"/bin/mkdir","9abf4134b60de6e191718fdc2f4c840990de88cdee3fc40267d77c2a56f2c2a7","Sun Apr 13 01:34:44 2014","51848"
"/bin/chmod","f43d6fec0500801085bec8f71266679064311d1a02dc2e785a91d66528a9798f","Sun Apr 13 01:34:44 2014","55944"
"/bin/pwd","0bd38776a8ded2a682cae90752cc04d296a8fa817c359f72280fcf86ad8f1dc1","Sun Apr 13 01:34:44 2014","31304"
"/bin/dumpkeys","c68b1f595023a673075e649e9f048d18aad62f562e36969b27765f56022d2834","Sun Feb 17 19:39:45 2013","78056"
"/bin/ntfs-3g.secaudit","374a967f3fa29ef7705d9ad4691523f0dd8cf27a5a8cc3cb15ee1a5695bba4ae","Sat Apr 12 10:01:32 2014","67608"
"/bin/lsmod","21af4a377f848f201c8f942f57e034cdaf2689d7e9fb821b8e1a833532da0a03","Sat Jun 21 05:45:45 2014","154496"
"/bin/unicode_start","0e6e452031aaba7d9e0433fbb9b716da2b52ed6f91531cf4709c36f91faaceef","Sun Feb 17 19:39:39 2013","2762"
"/bin/ntfsfix","a5d252e72f913afc7fc9fdd1f03bc6d1201be759494b6ae79904cd50566a99e5","Sat Apr 12 10:01:32 2014","39024"
"/bin/loadkeys","1d662a74f7ce774869dbcec66a01fe76bb25422a383565814cfda8f7f83b3878","Sun Feb 17 19:39:45 2013","111328"
"/bin/netstat","308e64331cf31be3585b10624a6a4e524feeb1c8443dccafdb0f060e8b9e8236","Mon May 12 07:13:50 2014","119528"
"/bin/ls","2bd6d7448a604bd5f390327f5d8a8ff719e70e02195e1cfcb29ef89a96983666","Sun Apr 13 01:34:44 2014","109992"
```

### TODO
  - logo
  - stats per path
  
### DROPPED IDEAS
 - multi-threading support *(available in a separate branch although not working faster. Why? Well - python.)*
 - oop *(I think I will drop this idea. Procedural code will be easier to maintain in such small project.)*
