![image](https://github.com/user-attachments/assets/e0ffc1c6-77a3-49e9-a94b-09659193a7a4)

Creator - [Sasha Huang](https://github.com/umbresp)

This was a very interesting and unusual task, offering great variety and complexity.

---
# BetterDiscord

Searching through channels and users ("utflag{..." and messages from Sasha) in the discord chat did not bring anything useful, which was actually expected judging by the number of people who solved this task.

Further OSINT outside Discord would also not bring anything:
==Note: The initial scope for this challenge is just the Discord server itself, and not any persons or individuals. Unofficial content is not in scope.==

And also these 2 more messages from admin led to the idea that we should think in a different direction:
![image](https://github.com/user-attachments/assets/c4bc27ce-b62e-4c0a-8e18-959c103a234c)


So I decided to check for hidden channels. The first search on the web showed this:
![image](https://github.com/user-attachments/assets/e169828f-748e-4106-ad17-dfcea8908737)

[ShowHiddenChannels](https://github.com/JustOptimize/ShowHiddenChannels) - BetterDiscord plugin.

I decided to try this plugin and for that it was necessary to set up BetterDiscord.

After installing, in the discord settings you will see the following:

![Pasted image 20250319005606](https://github.com/user-attachments/assets/701bcd3f-4202-4869-91b5-ece0eb6085cb)

then go to the Plugins tab and open plugins folder:

![174233149236158769](https://github.com/user-attachments/assets/2ee1c8e6-ac7b-4a46-a6f4-febd1f3d56b0)

move [ShowHiddenChannels.plugin.js](https://github.com/JustOptimize/ShowHiddenChannels/releases/download/v0.5.8/ShowHiddenChannels.plugin.js) file there and restart discord.

Accept the installation of the dependency and enable them in Plugins tab:

![Pasted image 20250319010508](https://github.com/user-attachments/assets/439ad5b4-3326-4e27-b39d-682a5f4230ff)
![Pasted image 20250319011053](https://github.com/user-attachments/assets/e036057f-1903-4967-b89f-35fdb63a7f25)

Changes can be noticed immediately(you might need to restart discord once more):

![Pasted image 20250319010706](https://github.com/user-attachments/assets/3fd35686-ef1a-45ac-9a1c-ae1a5c6600c5)![Pasted image 20250319010906](https://github.com/user-attachments/assets/1beadfb3-0e53-403a-a32c-aecf64797fe1)

And finally an interesting finding! **admin-only** channel:
![image](https://github.com/user-attachments/assets/1de59e84-b122-4d78-a33e-c303743ac602)

Write down the password somewhere and open the link.
[https://docs.google.com/document/d/1cgFhoHKLEbbJlu1SX4gCfFI4CGEEoEisiFq1CW-TKUo/edit?tab=t.0]

---  
# UTCTF 2025 Operational Notes

First of all download the document as a txt file and open it in any text editor:
```
UTCTF 2025 Operational Notes
Date: March 14-March 16, 48 hours
https://utctf.live


Problems
* Binary Exploitation: 3-5
* Reverse Engineering: 3-5
* Cryptography: 3-5
* Web: 3-5
* Networking: 0-2
* Forensics: 0-4
* Misc/Puzzle: 0-8
Infrastructure
* TODO (ping)
Reminders for On-Duty Officers
* Remember to watch channels on Discord
* Challenge-specific clarifications should be directed to the author whenever possible
* Make sure to verify at the end of your shift that the next officer is online and available
Useful Links
                                                                              C
                                                                              o
                                                                              q
                                                                              \
                                                                              I
                                                                              P
                                                                              1
                                                                              o
                                                                              7
                                                                              h
                                                                              r
                                                                              #
                                                                              y
                                                                              y
                                                                              W
                                                                              7
WPPVY-9YgdHlRZjIWlYWnyST4lqZiILaA_tpGt3bqVU
```
So now we have these 3 strings:
```
Admin password: Bdm@9D/]J^7@9[D(
Coq\IP1o7hr#yyW7
WPPVY-9YgdHlRZjIWlYWnyST4lqZiILaA_tpGt3bqVU
```

Now let's visit the link, It takes us to a [GitHub gists](https://gist.github.com/umbresp/5275f23f615c9bdcb21c463ac4b87c3c) page.

Click revisions and decode the base64.
![image](https://github.com/user-attachments/assets/5d5b9894-016c-4999-a9bc-de8e4603bf6c)
![image](https://github.com/user-attachments/assets/41612e50-4b70-4c87-9f86-fc86bbaf3ffa)
[https://mega.nz/file/HHgR1RRL]

**WPPVY-9YgdHlRZjIWlYWnyST4lqZiILaA_tpGt3bqVU** was the decryption key:

![image](https://github.com/user-attachments/assets/000c4bd2-8bf3-40cc-a2d8-7eac8726f6df)

---

# Rabbit.zip

![image](https://github.com/user-attachments/assets/38ab50ed-4063-4d11-b97c-f1e60ff9bd43)

The password is **Bdm@9D/]J^7@9[D(**

![image](https://github.com/user-attachments/assets/03d9bb5a-d5ac-401e-b689-6858a75dc52f)

I tried steganography techniques on image.jpg, but found nothing, so let's move on from it.

Upon discovering the .git folder, I began investigating the repository to understand its structure and contents. I knew that Git repositories store all their data in the .git/objects directory using a content-addressable filesystem.
# Step 1: Exploring Git Objects
I first navigated to the objects directory and found an object file:
```
arsen@archlinux ~/C/U/M/D/test (master)> cd .git/objects/
arsen@archlinux ~/C/U/M/D/t/.g/objects (GIT_DIR!)> ls
01/  0a/  30/  58/  5c/  8f/  extracted_image.jpg  info/  pack/
arsen@archlinux ~/C/U/M/D/t/.g/objects (GIT_DIR!)> cd 01/
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!) [127]> ls
278d6de291f04d0b47c5598d16b16844d2771e
```
When trying to view this object, I encountered an error:
```
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!)> git cat-file -p 278d6de291f04d0b47c5598d16b16844d2771e
fatal: Not a valid object name 278d6de291f04d0b47c5598d16b16844d2771e
```
#Step 2: Understanding Git Object Structure
I realized the issue was related to how Git organizes objects. The first two characters of the hash represent the directory, and the rest is the filename. So the full hash should be:
*01278d6de291f04d0b47c5598d16b16844d2771e*:
```
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!) [128]> git cat-file -p 01278d6de291f04d0b47c5598d16b16844d2771e
100644 blob 5c6f3ba2073706ced84050012d8eea559a7df177	image.jpg
```
It's another .jpg file, let's extract it:
```
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!)> git cat-file -p 01278d6de291f04d0b47c5598d16b16844d2771e > extracted_image.jpg
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!)> ls
278d6de291f04d0b47c5598d16b16844d2771e  extracted_image.jpg
```
Let's try to run exiftool:
```
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!)> exiftool extracted_image.jpg
ExifTool Version Number         : 13.25
File Name                       : extracted_image.jpg
Directory                       : .
File Size                       : 63 bytes
File Modification Date/Time     : 2025:03:19 02:44:37+04:00
File Access Date/Time           : 2025:03:19 02:45:11+04:00
File Inode Change Date/Time     : 2025:03:19 02:44:37+04:00
File Permissions                : -rw-r--r--
File Type                       : TXT
File Type Extension             : txt
MIME Type                       : text/plain
MIME Encoding                   : us-ascii
Newlines                        : Unix LF
Line Count                      : 1
Word Count                      : 4

```
There is something found, hooray!! Lets extract it.
```
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!)> steghide info extracted_image.jpg
"extracted_image.jpg":
  format: jpeg
  capacity: 29.3 KB
Try to get information about embedded data ? (y/n) y
Enter passphrase: 
steghide: could not extract any data with that passphrase!

```
There is only 1 unused string left so let's try with it
**Coq\IP1o7hr#yyW7**
```
arsen@archlinux ~/C/U/M/D/t/.g/o/01 (GIT_DIR!)> steghide info extracted_image.jpg -p "Coq\IP1o7hr#yyW7"
"extracted_image.jpg":
  format: jpeg
  capacity: 29.3 KB
  embedded file "emb2.txt":
    size: 37.0 Byte
    encrypted: rijndael-128, cbc
    compressed: yes
```
And Finally the last step!
```
arsen@archlinux ~/C/U/M/Down the Rabbit Hole (master) [1]> cat emb2.txt
utflag{f0ll0w1ng_th3_wh1t3_r4bb1t_:3}⏎     
```







