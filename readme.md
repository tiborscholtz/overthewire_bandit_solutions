**Bandit Level 0:**  
`ssh bandit0@bandit.labs.overthewire.org -p 2220`
The password for this level:  
`bandit0`

Our first task is very easy. Type `cat readme` to reveal the password for the next level.

The password for this level:

NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

**Bandit Level 1:**  
`ssh bandit1@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`  

There is a file in the current directory, named '-'. You can view its contents by typing the following: `cat ./-`  

The './' stands for the current directory.

The password for level 2 is:

rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

**Bandit Level 2:**  
`ssh bandit2@bandit.labs.overthewire.org -p 2220`  
The password for this level:    
`rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`  

This time the file that contains the password has spaces in it. Simply, type in the following:

`cat ./spaces\ in\ this\ filename` To escape the whitespaces.

The password for level 3 is:  
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG  

**Bandit Level 3:**  
`ssh bandit3@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`  

There is a directory, called 'inhere', which contains a hidden file. A hidden file in linux stars with a '.' character. However, you can still access it by the following commands:

`cd inhere`  
`cat .hidden`

The password for level 4 is:  
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

**Bandit Level 4:**  
`ssh bandit4@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`  

Start with `cd inhere`  
If we type `ls`, we can see that there are a lot of files in the 'inhere' directory. Do not start inspecting them one after another. Instead, we need the only file that is a human-readable format. With the following command:  
`find . -type f -print0 | xargs -0 file`  

> ./-file03: data  
> ./-file06: data  
> ./-file08: data  
> ./-file07: ASCII text  
> ./-file04: data  
> ./-file00: data  
> ./-file01: data  
> ./-file02: data  
> ./-file09: Non-ISO extended-ASCII text, with no line terminators  
> ./-file05: data  

We can list out the type of data for each file in the directory. Looks like the file, named '-file07' is our target. Let's look at it:  
`cat ./-file07`

The password for level 5 is:  
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

**Bandit Level 5:**  
`ssh bandit5@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`  
Start with `cd inhere`. This time, our problem multiplies, because we have a lot of directories, with a lot of files in it.  
We have 3 criteria for this level. Our target needs to be:  
- human-readable
- 1033 bytes in size
- not executable

Out command is the following:  
`find . -type f ! -executable -print0 | xargs -0 du -sb | grep 1033`

The result should be:  
> 1033	./maybehere07/.file2  

So, type in `cat ./maybehere07/.file2` 
The password for level 6 is:   
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

**Bandit Level 6:**  
`ssh bandit6@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`  

We need to do a search again for the password. We have four different criteria.The file is:  

- **somewhere** on the server
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

So, for this problem, we need to run the following:  

`find / -type f -user bandit7 -group bandit6 2>&1 | grep -v "Permission denied" 2>&1 | grep -v "No such file"`

Let's break down this command:  
- `find /`: starts at the root directory
- `-type f`: we want to find all files
- `-user bandit7`: owned by bandit7
- `-group bandit6`: owned by group bandit6
- `2>&1`: We redirect the stderr to stdout, because we want to filter out files with no permission
- ` grep -v "Permission denied" 2>&1 |`: That's why we needed the previous part of the command. We can get only the files that does not contain the text "Permission denied"
-  `| grep -v "No such file"`: The same as before, but with different text.

The output should be:  
> /var/lib/dpkg/info/bandit7.password

Type in:`cat /var/lib/dpkg/info/bandit7.password`

The password for level 7 is:  
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

**Bandit Level 7:**  
`ssh bandit7@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S`  

We have a file, called 'data.txt'. We need to search for a word 'millionth'  
`cat data.txt | grep millionth`  
The output should be:  
> millionth	TESKZC0XvTetK0S9xNwm25STk5iWrBvP

The password for level 8 is:  
TESKZC0XvTetK0S9xNwm25STk5iWrBvP

**Bandit Level 8:**  
`ssh bandit8@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`TESKZC0XvTetK0S9xNwm25STk5iWrBvP`  

We have a 'data.txt' again, the password is the **the only line of text that occurs only once**  
`sort data.txt | uniq -u`

The password for level 9 is:  
EN632PlfYiZbn3PhVK3XOGSlNInNE00t

**Bandit Level 9:**  
`ssh bandit9@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`EN632PlfYiZbn3PhVK3XOGSlNInNE00t`

We have a 'data.txt' again. The password is **in one of the few human-readable strings, preceded by several ‘=’ characters.**

We can use the `strings` command, to get the human-readable parts of the file. We can then pass the result to `grep`, to use the `"=+"` expression, to match anything that starts with an equal sign
`strings data.txt | grep -E "=+"`

The output should be something like this:  

> 4========== the#  
> 5P=GnFE  
> ========== password  
> 'DN9=5  
> ========== is  
> $Z=_  
> =TU%  
> =^,T,?  
> W=y  
> q=W  
> X=K,  
> ========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s  
> &S=(  
> nd?=  


The password for level 10 is:  
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

**Bandit Level 10:**  
`ssh bandit10@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s`

The 'data.txt' contains our password, however it is base64 encoded. We can decode it easily, using the following command: `cat data.txt | base64 --decode`

The password for level 11 is:  
6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

**Bandit Level 11:**  
`ssh bandit11@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`

The contents of 'data.txt' - as the overthewire site says - **all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions**  

So that's a ROT13 algorithm. We have a built-in tool to rotate it back.

`cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`

The password for level 12 is:  
JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

**Bandit Level 12:**  
`ssh bandit12@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`

The description of the level states that we should create a temporary directory, and move our work to there. Let's do it!

Let's check for our files first:  
`ls`  
> data.txt

`mktemp -d`  
> /tmp/tmp.{tempdirname}  

Let's copy the file to our newly reacted folder:  
`cp ./data.txt /tmp/tmp.{tempdirname}`  
`/tmp/tmp.nOSFloGiLM`

this task is going to be a bit repetive:

`xxd -r data.txt data`

The '-r' operator, as the manpage says: 'Reverse operation: convert (or patch) hexdump into binary.'. So, we've created a new file, called 'data'. Let's check the file type:  
`file data`  
> data: gzip compressed data, was "data2.bin"  

Since it's a gzip compressed data, let's run the following command:  
`mv data data.gz`  
After that, we can use 'gzip' to decompress it:  
`gzip -d data.gz`  
Let's check our new created file:  
`file data`  
> data: bzip2 compressed data,  

Let's run the following command:  
`mv data data.bz2`  
After that, we can use 'bzip2' to decompress it:  
`bzip2 -d data.bz2`  
Let's check our new created file again:  
`file data`  
> data: gzip compressed data, was "data4.bin"  

Since it's a gzip compressed data, let's run the following command:  
`mv data data.gz`  
After that, we can use 'gzip' to decompress it:  
`gzip -d data.gz`  
Let's check our new created file:  
`file data`  
> data: POSIX tar archive (GNU)  

Since it's a POSIX tar archive, let's run the following command:  
`mv data data.tar`  
After that, we can use 'tar' to extract the contens of it:  
`tar xvf data.tar`  
Let's check our new created file:  
`file data5.bin`  
> data5.bin: POSIX tar archive (GNU)  

Since it's a POSIX tar archive, let's run the following command:  
`mv data5.bin data5.tar`  
After that, we can use 'tar' to extract the contens of it:  
`tar xvf data5.tar`  
Let's check our new created file:  
`file data6.bin`  
> data6.bin: bzip2 compressed data  

Since it's a bzip2 compressed data, let's run the following command:  
`mv data6.bin data6.tar`  
After that, we can use 'tar' to extract the contens of it:  
`tar xvf data6.tar`  
Let's check our new created file:  
`file data8.bin`  
> data8.bin: gzip compressed data, was "data9.bin"  

Since it's a gzip compressed data, let's run the following command:  
`mv data8.bin data8.gz`  
After that, we can use 'gzip' to decompress it:  
`gzip -d data8.gz`  
Let's check our new created file:  
`file data8`  
> data8: ASCII text  

Finally! Let's view its content:
`cat data8`
> The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw  

The password for level 13 is:  
wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

**Bandit Level 13:**  
`ssh bandit13@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw`  

Let's do a quick 'ls' to see what we have for this level:  
`ls`
> sshkey.private  

That's something different. This will be for the login to the next level: let's cat out its contents, and save it to our local drive:  

`cat sshkey.private`

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

There are no passwords for level 14. You can use the ssh key to log in.

Save it with whatever name you want, (i will save it as 'sshkey14.private) and change its permissions with: `chmod 600 sshkey14.private`, because otherwise we cannot use it, and if you want to log in, you are going to receive an error.

**Bandit Level 14:**

`ssh bandit14@bandit.labs.overthewire.org -p 2220 -i ./sshkey14.private`  

This level is a bit different. You need to retrieve the password of the **CURRENT** level. You can do that by typing:

`cat /etc/bandit_pass/bandit14`  
> fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq  

With this, you cannot go to the next level. However, you need to use 'nc' also known as 'netcat', that can open TCP connections. As the current level's description says:

*the password of the current level to port 30000 on localhost*  
So, we need to type:  
`nc localhost 30000`  
And empty response comes back, it's normal. We can however, paste the password we've just found, to here:

`fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq`  
By pressing enter:  
> Correct!  
> jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt  

The password for level 15 is:  
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

**Bandit Level 15:**  
`ssh bandit15@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt`

Our task is similar to the previous level:  
*The password for the next level can be retrieved by submitting the password of the current level to port **30001 on localhost** using SSL encryption.*  

So, we cannot use nc, for now. Instead, we can use 'openssl' to communiate using ssl encryption.

`openssl s_client -connect localhost:30001`

Simple type in:  
`jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt`
The response should be:  
> Correct!  
> JQttfApK4SeyHwDlI9SXGR50qclOAil1 


The password for level 16 is:  
JQttfApK4SeyHwDlI9SXGR50qclOAil1

**Bandit Level 16:**

This task should be divided into two parts. From 31000 to 32000, we need to find out which port have a server that can listen. We can do this, using 'nmap':  
`nmap -p 31000-32000 localhost`

The response should be something like this:  
> Nmap scan report for localhost (127.0.0.1)  
> Host is up (0.00013s latency).  
> Not shown: 995 closed ports  
> PORT      STATE SERVICE  
> 31046/tcp open  unknown  
> 31123/tcp open  unknown  
> 31518/tcp open  unknown  
> 31691/tcp open  unknown  
> 31790/tcp open  unknown  
> 31960/tcp open  unknown  

Try each port, using: `openssl s_client -connect localhost:{portnumber}}`. Some of these port will close connection instantly, while some of them allows us to send back data. For these port, send back the current password. 31790 should be the correct port.

`openssl s_client -connect localhost:31790`

`JQttfApK4SeyHwDlI9SXGR50qclOAil1`
> Correct!  
-----BEGIN RSA PRIVATE KEY-----  
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ  
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ  
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu  
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW  
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX  
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD  
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl  
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd  
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC  
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A  
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama  
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT  
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx  
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd  
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt  
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A  
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi  
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg  
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu  
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni  
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU  
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM  
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b  
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3  
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=  
-----END RSA PRIVATE KEY-----  

Let's copy this private key, and save it as 'sshkey17.private'. Don't forget to give correct permission to this file, otherwise you cannot use it to connect to the next level.

`chmod 600 ./sshkey17.private`  

There are no passwords for level 14. You can use the ssh key to log in.

**Bandit Level 17:**

`ssh -i sshkey17.private bandit17@bandit.labs.overthewire.org -p 2220`

By typing `ls` we can see that there are two files: `passwords.new` and `passwords.old`. They are quite lengthy, but we need to find the difference between them, because the different line will be the password for the next level. For that, we can use the 'diff' command line utility. Diff waits for two parameters. Pass the two file names as parameters

`diff passwords.new passwords.old`

The result should be the upper line

> 42c42  
> < hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg  
> ---  
> \> glZreTEH1V3cGKL6g4conYqZqaEj0mte  

The password for level 18 is:  
hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg

**Bandit Level 18:**  
`ssh bandit18@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`  

After typing in the password, you are instantly logged out. That's normal, the level is made like this. However, we need to figure out a way, to still get information from the server.

With the 'ssh' command line utility, we have the ability to send a command with the connection, after the connection parameters.

So, type in the following(you need to fill in the password again):

`ssh bandit18@bandit.labs.overthewire.org -p 2220 ls`  
> readme  
So, the command is successful, and we have a readme file at the home directory. Let's try to connect, again, but change the 'ls' to 'cat readme'

`ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`  
> awhqfNnAbc1naukrpqDYcF95h7HoMTrC

Looks like we have the password!

The password for level 19 is:  
awhqfNnAbc1naukrpqDYcF95h7HoMTrC  

**Bandit Level 19:**  
`ssh bandit19@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`awhqfNnAbc1naukrpqDYcF95h7HoMTrC`  

We have a setuid binary in this directory. Type 'ls' to inspect the files in the current directory
`ls` 
> bandit20-do  

Let's run 'bandit20-do, to see what's happening:

`./bandit20-do`  
> Run a command as another user.  
>   Example: ./bandit20-do id  
`./bandit20-do id`  
> uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)

Well, we need to grab the password for bandit20, which is in /etc/bandit_pass/bandit20

By typing: `ls -l /etc/bandit_pass/bandit20`  
> -r-------- 1 bandit20 bandit20 33 Apr 23 18:04 /etc/bandit_pass/bandit20

We can see that the file bandit20 is owned by bandit20. So, by running:

`./bandit20-do cat /etc/bandit_pass/bandit20`  
> VxCazJaVykI6W36BkBU0mJTCM8rR95XT

We have the password!

The password for level 20 is:  
VxCazJaVykI6W36BkBU0mJTCM8rR95XT 

**Bandit Level 20:**  
`ssh bandit20@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`VxCazJaVykI6W36BkBU0mJTCM8rR95XT`  

Our first task is to create a service the listens on a speficic port. For now, let's say port 12345.

We need to provide that service the password to the current level. We can do this in the following way:  
`echo "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" | netcat -lp 12345 &`  

As you can see, we first echo the password to this level, we forward the result to the command 'netcat -lp 12345 &'  
We can do a quick `ps aux`, to see if our process is really running:  

> USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND  
> bandit20   67480  0.0  0.2  17056  9812 ?        SNs  08:24   0:00 /lib/systemd/systemd --user  
> bandit20   67488  0.0  0.1   9272  6016 pts/36   SNs+ 08:24   0:00 -bash  
> bandit20  113704  0.0  0.1   9180  5996 pts/9    SNs+ 08:52   0:00 -bash  
> bandit20  133031  0.2  0.1   9140  5780 pts/5    SNs  09:02   0:00 -bash  
> **bandit20  133118  0.0  0.0   3532  1212 pts/5    SN   09:02   0:00 netcat -lp 12345**  
> bandit20  133146  0.0  0.0  10068  1572 pts/5    RN+  09:02   0:00 ps aux  

There it is! Let's look at the given utility `./suconnect`:  

> This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.  

The most important part is the following: 'If it receives the correct password from the other side' We just did that in the previous part of this level. Now, let's connect to the **same** port with this program:  
`./suconnect 12345`  
> Password matches, sending next password  
> NvEJF7oVjkddltPSrdKEFOllh9V1IBcq  

The password for level 20 is:  
NvEJF7oVjkddltPSrdKEFOllh9V1IBcq

**Bandit Level 21:**  
`ssh bandit21@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`NvEJF7oVjkddltPSrdKEFOllh9V1IBcq`  

We have a program, running at fixed intervals, thanks to 'cron'. The main directory is '/etc/cron.d/

`cd /etc/cron.d`  

We need the password for Level 22, so let's look at the corresponding file:  
`cat cronjob_bandit22`  
> \* \* \* \* \* bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null  

We have a file at '/usr/bin'. Let's take a look at it:  
`cat /usr/bin/cronjob_bandit22.sh`  
> #!/bin/bash  
> chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv  
> cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv  

Looks like it writes the password to the file '/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv'

Let's take a look at it:

`cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`  
> WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff

The password for level 22 is:  
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff 

**Bandit Level 22:**  
`ssh bandit22@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff` 

We need to deal with a scheduled task again. Let's look for the /etc/cron.d again:  
`cd /etc/cron.d`  
By typing: `ls`, we can see that we have a file, named 'cronjob_bandit23'. Let's take a look at it:  
`cat cronjob_bandit23`

> @reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null  
> \* \* \* \* \* bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null  

Again, we need to look at the filepath we've found: '/usr/bin/cronjob_bandit23.sh'  
`cat /usr/bin/cronjob_bandit23.sh`

> #!/bin/bash  
> myname=$(whoami)  
> mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)  
> echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"  
> cat /etc/bandit_pass/$myname > /tmp/$mytarget  

Looks like it takes the md5 sum of 'echo I am user $myname' and creates a file with a name of the md5sum. Let's try it with bandit23.  

`echo "I am user bandit23" | md5sum`  
> 8ca319486bfbbc3663ea0fbe81326349  -  
Great. We have the directory name. Let's inspect it:  
`cat /tmp/8ca319486bfbbc3663ea0fbe81326349`  
> QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G  

The password for level 23 is:  
QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G 

**Bandit Level 23:**  
`ssh bandit23@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G`  

`cd /etc/cron.d`  
`cat cronjob_bandit24`  

> @reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null  
> \* \* \* \* \* bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null

`cat /usr/bin/cronjob_bandit24.sh`  

> #!/bin/bash  
>   
> myname=$(whoami)  
>   
> cd /var/spool/$myname/foo || exit 1  
> echo "Executing and deleting all scripts in /var/spool/$myname/foo:"  
> for i in * .*;  
> do  
>     if [ "$i" != "." -a "$i" != ".." ];  
>     then  
>         echo "Handling $i"  
>         owner="$(stat --format "%U" ./$i)"  
>         if [ "${owner}" = "bandit23" ]; then  
>             timeout -s 9 60 ./$i  
>         fi  
>         rm -rf ./$i  
>     fi  
> done  

Looks like there is a directory at the path: '/var/spool/bandit24/foo'. Let's look if it is really there:  

`cd /var/spool/bandit24/foo`  
Yes. It does exist. By looking at the script above, the scheduled tasks executes every file at this directory, and deletes them after execution.  
But why is that good for us? We need the password for the next level. We can write a script that writes out the contents of '/etc/bandit_pass/bandit24' to a file that's accessible for us.  
Let's create a directory under '/tmp'

`mktemp -d`  
`cd {directoryname}`  
Once we are inside the directory, we can write a little script to get the contents of the password file. We use 'cat' on '/etc/bandit_pass/bandit24' and then forward it to '/tmp/{directoryname}/password'  
`nano myscript.sh`  

```
#!/bin/sh
cat /etc/bandit_pass/bandit24 > /tmp/{directoryname}/password
```

Let's create the file, called 'password'  
`touch password`  
Also, we need to set proper permissions, so everyone can write to this file:  
`chmod 777 -R password`

After we've saved the file, let's copy this to '/var/spool/bandit24/foo' by typing:  
`cp myscript.sh /var/spool/bandit24/foo`  

After a minute, let's check the size of the password file:

`ls -la`  
`cat password`
> VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar

The password for level 23 is:  
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 

**Bandit Level 24:**  
`ssh bandit24@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar`  

So, we have a daemon at port 30002. If we send the password of level 24 plus a 4 digit uknown code, it gives us back the password for the next level.

We have to automate this somehow, because we need to try every number from 1000 to 9999

First, make a directory with `mktemp -d` and `cd /tmp/{directoryname}`.  

Create an empty script, with `touch myscript.sh` and start editing it with `nano myscript.sh`.  

The script starts with a for loop from 1000 to 9999. It echoes out the password of the previous level, plus the current four digit number from 1000 to 9999.
It looks like this:

VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 1000  
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 1001
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 1002  
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 1003  
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 1004  
...  
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 9999  

until we find the correct four digit number.


```
for i in {1000..9999}
do
        echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i"
done
```

We run the script, using the following command. First, the script's output is passed to 'nc localhost 30002', and the output of this is forwarded to 'results.txt'
`touch results.txt`  
`./myscript.sh | nc localhost 30002 > results.txt`  
It will take a while, to complete all requests. after it is finished, let's inspect the 'results.txt' file. It contains every response from 1000 to 9999,so we need to filter out all wrong answers.  
`cat results.txt | grep -v "Wrong"`  
> I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.  
> Correct!  
> The password of user bandit25 is p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d  

The password for level 25 is:  
p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d  

**Bandit Level 25:**  
`ssh bandit25@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d`  

Let's see what do we have here:  
`ls`  
> bandit26.sshkey
`cat bandit26.sshkey`  
> -----BEGIN RSA PRIVATE KEY-----  
> MIIEpQIBAAKCAQEApis2AuoooEqeYWamtwX2k5z9uU1Afl2F8VyXQqbv/LTrIwdW  
> pTfaeRHXzr0Y0a5Oe3GB/+W2+PReif+bPZlzTY1XFwpk+DiHk1kmL0moEW8HJuT9  
> /5XbnpjSzn0eEAfFax2OcopjrzVqdBJQerkj0puv3UXY07AskgkyD5XepwGAlJOG  
> xZsMq1oZqQ0W29aBtfykuGie2bxroRjuAPrYM4o3MMmtlNE5fC4G9Ihq0eq73MDi  
> 1ze6d2jIGce873qxn308BA2qhRPJNEbnPev5gI+5tU+UxebW8KLbk0EhoXB953Ix  
> 3lgOIrT9Y6skRjsMSFmC6WN/O7ovu8QzGqxdywIDAQABAoIBAAaXoETtVT9GtpHW  
> qLaKHgYtLEO1tOFOhInWyolyZgL4inuRRva3CIvVEWK6TcnDyIlNL4MfcerehwGi  
> il4fQFvLR7E6UFcopvhJiSJHIcvPQ9FfNFR3dYcNOQ/IFvE73bEqMwSISPwiel6w  
> e1DjF3C7jHaS1s9PJfWFN982aublL/yLbJP+ou3ifdljS7QzjWZA8NRiMwmBGPIh  
> Yq8weR3jIVQl3ndEYxO7Cr/wXXebZwlP6CPZb67rBy0jg+366mxQbDZIwZYEaUME  
> zY5izFclr/kKj4s7NTRkC76Yx+rTNP5+BX+JT+rgz5aoQq8ghMw43NYwxjXym/MX  
> c8X8g0ECgYEA1crBUAR1gSkM+5mGjjoFLJKrFP+IhUHFh25qGI4Dcxxh1f3M53le  
> wF1rkp5SJnHRFm9IW3gM1JoF0PQxI5aXHRGHphwPeKnsQ/xQBRWCeYpqTme9amJV  
> tD3aDHkpIhYxkNxqol5gDCAt6tdFSxqPaNfdfsfaAOXiKGrQESUjIBcCgYEAxvmI  
> 2ROJsBXaiM4Iyg9hUpjZIn8TW2UlH76pojFG6/KBd1NcnW3fu0ZUU790wAu7QbbU  
> i7pieeqCqSYcZsmkhnOvbdx54A6NNCR2btc+si6pDOe1jdsGdXISDRHFb9QxjZCj  
> 6xzWMNvb5n1yUb9w9nfN1PZzATfUsOV+Fy8CbG0CgYEAifkTLwfhqZyLk2huTSWm  
> pzB0ltWfDpj22MNqVzR3h3d+sHLeJVjPzIe9396rF8KGdNsWsGlWpnJMZKDjgZsz  
> JQBmMc6UMYRARVP1dIKANN4eY0FSHfEebHcqXLho0mXOUTXe37DWfZza5V9Oify3  
> JquBd8uUptW1Ue41H4t/ErsCgYEArc5FYtF1QXIlfcDz3oUGz16itUZpgzlb71nd  
> 1cbTm8EupCwWR5I1j+IEQU+JTUQyI1nwWcnKwZI+5kBbKNJUu/mLsRyY/UXYxEZh  
> ibrNklm94373kV1US/0DlZUDcQba7jz9Yp/C3dT/RlwoIw5mP3UxQCizFspNKOSe  
> euPeaxUCgYEAntklXwBbokgdDup/u/3ms5Lb/bm22zDOCg2HrlWQCqKEkWkAO6R5  
> /Wwyqhp/wTl8VXjxWo+W+DmewGdPHGQQ5fFdqgpuQpGUq24YZS8m66v5ANBwd76t  
> IZdtF5HXs2S5CADTwniUS5mX1HO9l5gUkk+h0cH5JnPtsMCnAUM+BRY=  
> -----END RSA PRIVATE KEY-----  

Save it as 'sshkey26.private' and do a `chmod 600 ./sshkey26.private` on the newly created file on your computer.

There are no passwords for level 26. You can use the ssh key to log in.

**Bandit Level 26:**  
`ssh -i sshkey26.private bandit26@bandit.labs.overthewire.org -p 2220`

The session instantly closes, as soon as we logged in. We've seen it before. Let's send an `ls` to see what do we have:  

`ssh -i ./sshkey26.private bandit26@bandit.labs.overthewire.org -p 2220 ls`  
Hmm...doesn't seem to be working. Let's try 'whoami'  
`ssh -i ./sshkey26.private bandit26@bandit.labs.overthewire.org -p 2220 whoami`  
Nothing here, too...

Let's go back to our previous level with the previous password. We need to find out what shell is being used here. After logging in with bandit25, type:
`cat /etc/passwd`  
The important part for us is this:  

> bandit25:x:11025:11025:bandit level 25:/home/bandit25:/bin/bash  
> bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext  
> bandit27:x:11027:11027:bandit level 27:/home/bandit27:/bin/bash  

Let's see what this showtext is:  
`cat /usr/bin/showtext`

> #!/bin/sh  
>   
> export TERM=linux  
>   
> exec more ~/text.txt  
> exit 0  

Looks like there is a 'text.txt' file that is being printed out, using more. We can utilize this to our advantage. Let's try to minimize the screen, so 'more' jumps into action, effectively stops the 'exit 0' command the kicks out from this server. By resizing our terminal to a very little resolution, and trying to log in, the 'more' appears on the screen. Good, we are inside. First things first, we are in [Vim](https://www.vim.org/), which is a terminal based text editor. 

First, press `v`  
This brings us into Vim's visual mode  

Let's type `:e /etc/bandit_pass/bandit26`. This should bring us the password for the next level.

The password for level 26 is:  
c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1

**Bandit Level 26:**  
`ssh bandit26@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1`  

Okay, so we need to do the terminal resize thing again:  

1. Resize the terminal, and log in that way, by passing the password
2. Press v
3. You are in Vim's visual mode


Not, we need to set a shell for ourselves, to properly continue this task. In vim, you can type:

`set shell=/bin/bash` to set 'bash' as our shell. After that, type `:shell` to enter our new shell. From here on, you should have a familiar prompt. Let's type `ls` to see what we have to deal with:  
> bandit27-do  text.txt  

the file 'text.txt' contains the banner that we needed to evade in the beginning of the task. Let's we need to do with 'bandit27-do'. Type `./bandit27-do`  

> Run a command as another user.  
> Example: ./bandit27-do id  
> bandit26@bandit:~$  

Let's try `./bandit27 cat /etc/bandit_pass/bandit27`

> YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS

Got it!

The password for level 27 is:  
YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS

**Bandit Level 27:**  
`ssh bandit27@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS`  

The level description says that we need to handle a git repository **at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220**. We need to download it, so the best would be to create a temporary folder.

`mktemp -d`  
`cd {tempdirname}`  

Let's clone the repository. The cloning looks like the following:  
`git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo`  

The result should be something like this:  

> Cloning into 'repo'...  
> The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.  
> ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.  
> This key is not known by any other names  
> Are you sure you want to continue connecting (yes/no/[fingerprint])?  

Type `yes`

It asks for the password, which is 'YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS'. So, type in `YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS`

The output should be something like this:

> remote: Enumerating objects: 3, done.  
> remote: Counting objects: 100% (3/3), done.  
> remote: Compressing objects: 100% (2/2), done.  
> remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0  
> Receiving objects: 100% (3/3), done  

Let's type a quick `ls` to see what do we have here:
> repo  

There is a directory, named 'repo'. Let's inpect it.  
`cd repo`  
`ls`  
> README  

There is a readme file in it. Let's inspect it, too:  
`cat README`  
> The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR  
Great!

The password for level 28 is:  
AVanL161y9rsbcJIsFHuw35rjaOM19nR

**Bandit Level 28:**  
`ssh bandit28@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`AVanL161y9rsbcJIsFHuw35rjaOM19nR`  

We have a repository again, at 'ssh://bandit28-git@localhost/home/bandit28-git/repo'. So let's start, by creating a temporary directory again, because we need to work with that repo.

`mktemp -d`  
`cd {tempdirname}`  

Let's clone the repository. The cloning looks like the following:  
`git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo`  

The result should be something like this:  

> Cloning into 'repo'...  
> The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.  
> ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.  
> This key is not known by any other names  
> Are you sure you want to continue connecting (yes/no/[fingerprint])?

Type `yes`

> Could not create directory '/home/bandit28/.ssh' (Permission denied).  
> Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).  



It asks for the password, which is 'AVanL161y9rsbcJIsFHuw35rjaOM19nR'. So, type in `AVanL161y9rsbcJIsFHuw35rjaOM19nR`

The output should be something like this:

> remote: Enumerating objects: 9, done.  
> remote: Counting objects: 100% (9/9), done.  
> remote: Compressing objects: 100% (6/6), done.  
> remote: Total 9 (delta 2), reused 0 (delta 0), pack-reused 0  
> Receiving objects: 100% (9/9), done.  
> Resolving deltas: 100% (2/2), done.  

Let's type a quick `ls` to see what do we have here:
> repo  

`cd repo`  
`ls`  
> README.md  

There is a readme file. Let's quickly see it's content.

`cat README.md`  

> # Bandit Notes  
> Some notes for level29 of bandit.  
>   
> ## credentials  
>   
> - username: bandit29  
> - password: xxxxxxxxxx  

Well, nothing interesting....but, with git, we have an option to look for logs, which has been made during committing.

Type in `git log`  

> commit 899ba88df296331cc01f30d022c006775d467f28 (HEAD -> master, origin/master, origin/HEAD)  
> Author: Morla Porla <morla@overthewire.org>  
> Date:   Sun Apr 23 18:04:39 2023 +0000  
>   
>     fix info leak  
>   
> commit abcff758fa6343a0d002a1c0add1ad8c71b88534  
> Author: Morla Porla <morla@overthewire.org>  
> Date:   Sun Apr 23 18:04:39 2023 +0000  
>   
>     add missing data  
>   
> commit c0a8c3cf093fba65f4ee0e1fe2a530b799508c78  
> Author: Ben Dover <noone@overthewire.org>  
> Date:   Sun Apr 23 18:04:39 2023 +0000  
>   
>     initial commit of README.md  
>   

There was some kind of info leak. Maybe it way the password....? So, if we had a way to see the previous commits, maybe we could find the password?

We have 3 commits here:

- 899ba88df296331cc01f30d022c006775d467f28  
- abcff758fa6343a0d002a1c0add1ad8c71b88534
- c0a8c3cf093fba65f4ee0e1fe2a530b799508c78

Think of them as unique identifiers. We need to get the contents of 'abcff758fa6343a0d002a1c0add1ad8c71b88534', because it says it adds some missing data. Perhaps the password? Let's type in the following: `git checkout abcff758fa6343a0d002a1c0add1ad8c71b88534`  

The output should be something like this:

> Note: switching to 'abcff758fa6343a0d002a1c0add1ad8c71b88534'.  
>   
> You are in 'detached HEAD' state. You can look around, make experimental  
> changes and commit them, and you can discard any commits you make in this  
> state without impacting any branches by switching back to a branch.  
>   
> If you want to create a new branch to retain commits you create, you may  
> do so (now or later) by using -c with the switch command. Example:  
>   
>   git switch -c <new-branch-name>  
>   
> Or undo this operation with:  
>   
>   git switch -  
>   
> Turn off this advice by setting config variable advice.detachedHead to false  
>   
> HEAD is now at abcff75 add missing data  

Okay, so we are in a different state than before. Let's look around quickly.  
`ls`  
> README.md  

We still have that readme file. Let's inspect it  
`cat README.md`  
> # Bandit Notes  
> Some notes for level29 of bandit.  
>   
> ## credentials  
>   
> - username: bandit29  
> - password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S  

So, it means that in a previous state, it did contain the password after all!

The password for level 29 is:  
tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S

**Bandit Level 29:**  
`ssh bandit29@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S`

We have a repository again, at 'ssh://bandit29-git@localhost/home/bandit29-git/repo'. So let's start, by creating a temporary directory again, because we need to work with that repo.

`mktemp -d`  
`cd {tempdirname}`  

Let's clone the repository. The cloning looks like the following:  
`git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo`  

The result should be something like this:  

> Cloning into 'repo'...  
> The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.  
> ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.  
> This key is not known by any other names  
> Are you sure you want to continue connecting (yes/no/[fingerprint])?

Type `yes`

> Could not create directory '/home/bandit29/.ssh' (Permission denied).  
> Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).  

It asks for the password, which is 'tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S'. So, type in `tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S`

The output should be something like this:

> remote: Enumerating objects: 16, done.  
> remote: Counting objects: 100% (16/16), done.  
> remote: Compressing objects: 100% (11/11), done.  
> remote: Total 16 (delta 2), reused 0 (delta 0), pack-reused 0  
> Receiving objects: 100% (16/16), done.  
> Resolving deltas: 100% (2/2), done.  

Let's type a quick `ls` to see what do we have here:
> repo  

`cd repo`  
`ls`  
> README.md  

There is a readme file. Let's quickly see it's content.

`cat README.md`  

> # Bandit Notes  
> Some notes for bandit30 of bandit.  
>   
> ## credentials  
>   
> - username: bandit30  
> - password: <no passwords in production!>  

Well. It says that no passwords in production...maybe there is a password in dev...? Well, for that, we need to switch branch. We need to use the 'git checkout {branch}' command. Let's run it like this:

`git checkout dev`  

> Branch 'dev' set up to track remote branch 'dev' from 'origin'.  
> Switched to a new branch 'dev'  

Let's do a quick 'ls' to see if something has changed:  
`ls`
> code  README.md  

We have a new directory! But that's not important for us now, because by runnning `cat README.md`:  

> # Bandit Notes  
> Some notes for bandit30 of bandit.  
>   
> ## credentials  
>   
> - username: bandit30  
> - password: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS  

The readme file finally contains the password!

The password for level 30 is:  
xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS

**Bandit Level 30:**  
`ssh bandit30@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
`xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS`

We have a repository again, at 'ssh://bandit30-git@localhost/home/bandit30-git/repo'. So let's start, by creating a temporary directory again, because we need to work with that repo.

`mktemp -d`  
`cd {tempdirname}`  

Let's clone the repository. The cloning looks like the following:  
`git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo`  

The result should be something like this:  

> Cloning into 'repo'...  
> The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.  
> ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.  
> This key is not known by any other names  
> Are you sure you want to continue connecting (yes/no/[fingerprint])?

Type `yes`

> Could not create directory '/home/bandit30/.ssh' (Permission denied).  
> Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).  

It asks for the password, which is 'xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS'. So, type in `xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS`

The output should be something like this:

> remote: Enumerating objects: 4, done.  
> remote: Counting objects: 100% (4/4), done.  
> remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0  
> Receiving objects: 100% (4/4), done.  

Let's type a quick `ls` to see what do we have here:
> repo  

`cd repo`  
`ls`  
There is a readme file. Let's quickly see it's content.  
`cat README.md`  
> just an epmty file... muahaha  

Okay then...let's check `git log`

> commit 59530d30d299ff2e3e9719c096ebf46a65cc1424 (HEAD -> master, origin/master, origin/HEAD)  
> Author: Ben Dover <noone@overthewire.org>  
> Date:   Sun Apr 23 18:04:42 2023 +0000  
>   
>     initial commit of README.md  

Nothing interesting to see here.  

Let's dive deeper, with `ls -a
> .  ..  .git  README.md  

We have a hidden folder. Let's inspect it:  
`cd .git`  
`ls`  
> branches  config  description  HEAD  hooks  index  info  logs  objects  packed-refs  refs

We have a lot of different directories here. 

For this level, a basic knowledge of git commands are required. Git has the option of tagging. Tagging is basically the ability to mark specific points in the repository that is somehow important.

Type in the following `git tag`  
> secret  

Well-well, what do we have here...we need to somehow view that secret. Let's type: `git show secret`
> OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt  

Got it!  

The password for level 30 is:  
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt  

**Bandit Level 31:**  
`ssh bandit31@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt

This is the last level with git commands. It starts just as the previous ones did.  
We have a repository again, at 'ssh://bandit31-git@localhost/home/bandit31-git/repo'. So let's start, by creating a temporary directory again, because we need to work with that repo.

`mktemp -d`  
`cd {tempdirname}`  

Let's clone the repository. The cloning looks like the following:  
`git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo`  

The result should be something like this:  

> Cloning into 'repo'...  
> The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.  
> ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.  
> This key is not known by any other names  
> Are you sure you want to continue connecting (yes/no/[fingerprint])?

Type `yes`

> Could not create directory '/home/bandit31/.ssh' (Permission denied).  
> Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).  

It asks for the password, which is 'OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt'. So, type in `OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt`

The output should be something like this:

> remote: Enumerating objects: 4, done.  
> remote: Counting objects: 100% (4/4), done.  
> remote: Compressing objects: 100% (3/3), done.  
> remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0  
> Receiving objects: 100% (4/4), done.  

Let's type a quick `ls` to see what do we have here:
> repo  

`cd repo`  
`ls`  

> README.md  

There is a readme file. Let's quickly see it's content.  
`cat README.md`  

> This time your task is to push a file to the remote repository.  
>   
> Details:  
>     File name: key.txt  
>     Content: 'May I come in?'  
>     Branch: master  

Well, we've got our task. But how do we do that? First, let's create a file with a content, 'May I come in?'.

`echo "May I come in?" > key.txt` We can see it by typing `ls`  
> key.txt README.md  

We can run a command, that adds the file to the current state of the repository. 

`git add key.txt -f`  

After the 'add' command, we list the files we want to add, plus the '-f' flag to force the upload to process. Some files are ignored by git in default, this way we just make sure that the upload proceeds.Finally, we need to somehow 'send' that change to the repository. For that, we can use the 'commit' command. The commit has an '-m' flag, which stands for 'message'. We can send a message with the changes. This can be anything for now. For example:  

`git commit -m "whatever"`  
> [master 53cc38a] whatever
>  1 file changed, 1 insertion(+)
>  create mode 100644 key.txt
`git push origin master`  
> The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.  
> ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.  
> This key is not known by any other names  
> Are you sure you want to continue connecting (yes/no/[fingerprint])? yes  
> Could not create directory '/home/bandit31/.ssh' (Permission denied).  
> Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts)  

Let's type in the password:
`OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt`

> Enumerating objects: 4, done.  
> Counting objects: 100% (4/4), done.  
> Delta compression using up to 2 threads  
> Compressing objects: 100% (2/2), done.  
> Writing objects: 100% (3/3), 319 bytes | 319.00 KiB/s, done.  
> Total 3 (delta 0), reused 0 (delta 0), pack-reused 0  
> remote: ### Attempting to validate files... ####  
> remote:  
> remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.  
> remote:  
> remote: Well done! Here is the password for the next level:  
> remote: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y  
> remote:  
> remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.  
> remote:
> To ssh://localhost:2220/home/bandit31-git/repo  
>  ! [remote rejected] master -> master (pre-receive hook declined)  
> error: failed to push some refs to 'ssh://localhost:2220/home/bandit31-git/repo'  

Don't worry about the error. We have the password!

The password for level 30 is:  
rmCBvG56y58BXzv98yZGdO7ATVL5dW8y  

**Bandit Level 32:**  
`ssh bandit32@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
rmCBvG56y58BXzv98yZGdO7ATVL5dW8y

The level starts with a message that says: 'WELCOME TO THE UPPERCASE SHELL'.

When we try some basic commands, like `ls`, we can see that is converted into uppercase:  
> sh: 1: LS: not found

So, we need to somehow revert this process, and get everything into lowercase again. We have an option to get information about the currently used shell, with '$0'. '$' indicates that this is a variable, and '$0' is a special variable. '$0' contains a reference to our current shell, so type in:`$0`  
We can see that our prompt changes. We can now type normal commands, like `pwd`:  
> /home/bandit32  

Let's try to access the password for the last level:`cat /etc/bandit_pass/bandit33`

> odHo63fHiFqcWWJG9rLiLDtPm45KzUKy  

The password for level 30 is:  
odHo63fHiFqcWWJG9rLiLDtPm45KzUKy 



**Bandit Level 33:**  
`ssh bandit33@bandit.labs.overthewire.org -p 2220`  
The password for this level:  
odHo63fHiFqcWWJG9rLiLDtPm45KzUKy

`ls`  
> README.txt  

`cat README.txt`  

> Congratulations on solving the last level of this game!  
>   
> At this moment, there are no more levels to play in this game. However, we are constantly working  
> on new levels and will most likely expand this game with more levels soon.  
> Keep an eye out for an announcement on our usual communication channels!  
> In the meantime, you could play some of our other wargames.  
>   
> If you have an idea for an awesome new level, please let us know!  

Congratulations!