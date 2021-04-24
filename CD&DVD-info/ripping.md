## Notices
manuals - information about all things IT <br>
Copyright (C) 2021 thefirethirteen <br>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

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

> udfinfo -x /dev/cdrom
*or*
> udfinfo -x /dev/sr0
*or*
> udfinfo -x /dev/sr1
etc..
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

- This file is WIP.
- udfinfo is installed by a package, it does not come preinstalled; the guide should include that
