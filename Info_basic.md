# Basics for Unix

If you want to login to the cluster `ssh yourname@info.mcmaster.ca`

Never run on the head, which is 'youname@infoserv'.

To go into one of the machine, do `rsh info113` or `rsh info114` 

If you want to cancel a command type `Command .`

If you want to view the contents of a directory type `ls`.

If you want to change a directory type `cd `\<directory path\>.

If you want to know what directory you are in type `pwd`.

If you want to make a directory, type `mkdir` \<directory name\>.

If you want to remove a file type `rm -f `\<filename\>; to remove a directory `rm -rf`\<filename\>.

If you want to clean the screen, do `clear`

# Top
If you want to check the status of the job, do `top`.

To get off the top, do `q`.

To see the full command running on top, do `top` then `c`.

If you just want to look at your top, do `top -u martin`.

# Installing trinity
To download the trinity package we typed `Tr`.  This link would have to be updated when an new version becomes available.

To uncompress it, type `tar -zxvf v2.2.0.tar.gz`

Instructions for install are her `https://github.com/trinityrnaseq/trinityrnaseq/wiki/Installing%20Trinity`.



# Basics for using info.

To connect to info, use this command:

`ssh xue@info.mcmaster.ca`

This gets you into the `head` server, which is called infoserv.  Please do not run jobs on the head.  Instead you can connect to the other processors like this: `rsh info115` (or `rsh info113`, `rsh info114`,...).

You can check how busy a system is using the unix command `top`.  Exit by typing `q`.

# Using Unix Screen

Screen is very useful for running background jobs.

To launch a screen session type `screen -S `\<session name\>.

To exit a screen type `control a, d`.  

To list screen type `screen -ls`.

To reconnect with a screen type `screen -r `\<session name\>.

To kill a screen type `screen -X -S ` \<session name\> ` kill`.

To exit the server type `logout`.

# The data

Once the data were copied over, we uncompressed each file like this:

`tar -xvf Sample_BenEvansBJE3909cDNA_Library.tar`
and
`tar -xvf Sample_BenEvansBJE4168cDNA_Library.tar`

# To empty space in head 1 server, move it and zip it 
To know how large the file is:
 ```
 du -sh *
 ```
To move it to head 4:
```
mv trinityrnaseq-2.2.0/ /4/xue/
```
To create a symbolic link:
```
ln -s /4/xue/trinityrnaseq-2.2.0/ hereistrin
```
To move it back to head 1 from head 4:
```
mv /4/xue/trinityrnaseq-2.2.0/ .
```
To zip files:
```
gzip filename
```
To zip directory: 
```
tar -cvf genome_data.tar genome_data
```
# Sent notice when job is done from the server
```
SOME COMMAND ; echo "this job is done" | mail your_email@gmail.com
```

# To list all the package installed in R
```
ip <- as.data.frame(installed.packages()[,c(1,3:4)])
rownames(ip) <- NULL
ip <- ip[is.na(ip$Priority),1:2,drop=FALSE]
print(ip, row.names=FALSE)
```
