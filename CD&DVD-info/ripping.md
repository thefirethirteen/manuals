## 1. Find disc filesystem

#### 1.a. Check if iso:

> isosize -x /dev/cdrom

*or*

> isosize -x /dev/sr0

*or*

> isosize -x /dev/sr1

etc.. <br>
*or*

> isosize -x /dev/hdc

(rarely)

if output reports sector count and size, move on to step 2 <br>
if output is "might not be an ISO filesystem" then the disc does not have an ISO filesystem <br>

#### 1.b. Check if udf:

For this, you need to have the udftools package installed. <br>
To install this package on debian & derivatives (such as ubuntu) run:
> apt-get install udftools

To check, run:

> udfinfo -x /dev/cdrom

*or*

> udfinfo -x /dev/sr0

*or*

> udfinfo -x /dev/sr1

etc.. <br>
*or*

> udfinfo -x /dev/hdc
(rarely)

if output reports lots of information, move on to step 2 <br>
if output is "UDF Volume Recognition Sequence not found", then the disc does not have a UDF filesystem <br>

**Note:**
> If the commands above report "cannot open [...]: No medium found", then:
+ that drive may not exist
+ no disc is inserted
+ the disc is badly scratched or dirty.

## 2. Extract info

For copying, you need to know 3 things:
+ What device worked in the above step (the device may be either /dev/cdrom; /dev/sr0, /dev/sr1, etc.; /dev/hdc)
+ What the sector size or block size is (found in the output of the previous command)
+ What the sector count is or how many blocks are used (also found in the output of the previous command)

## 3. Copy the disc

Change Directory (cd) into whatever folder you want to copy the disc to.

Then run:

> dd if=< device > of=< name >.< fs > bs=< block_size > count=< block_count >

Replace the things between the <> with the following:
+ < device > : whatever device worked in step one
+ < name > --> a name of your choosing for the copied file (can be changed later)
+ < fs > --> either "iso" or "udf"
 + if isosize worked at step one, use iso
 + if udfinfo worked at step one, use udf
+ < block_size > --> sector size or block size from step two
+ < block_count > --> sector count or blocks used from step two

For example:

> dd if=/dev/cdrom of=my_file.udf bs=2048 count=304724

### Notes

- This manual is WIP.

# Manual information

&copy; 2022 [manuals contributors](https://github.com/thefirethirteen/manuals/blob/main/contributors.md)
<br> Licensed under the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license
