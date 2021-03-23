# Basic Linux commands

This tutorial requires that you have a [user account at CSC](https://docs.csc.fi/accounts/how-to-create-new-user-account/)
and it is a member of a project that [has access to Puhti service](https://docs.csc.fi/accounts/how-to-add-service-access-for-project/).
You have also already [logged to Puhti with ssh](ssh-puhti.md).


1. Now that you have logged in Puhti, let's check in which folder we are in! Type pwd and hit Enter.
```bash
pwd
```

2. Are there any files there? 
```bash
ls
```

3. Let's make a directory (replace YourName with your name)! Try ls to see if the folder is now there!
```bash
mkdir YourNameTestFolder 
ls
```

4. Go to that folder. Note, that if you just type cd and the first letter of the folder name,  then hit tab key, the terminal completes the name. Handy!
```bash
cd YourNameTestFolder
```

5. Let's download a file into this new folder. wget is the command for downloading from URL.
```bash
wget
```

6. What kind of file did you get? What's in that file now? What size is it? 
```bash
ls -lth
less filename
```

7. Let's make a copy of this file: cp filename YourNamefilename
```bash
cp filename YourNamefilename
ls -lth
less YourNamefilename
```

8. Let's remove the file we downloaded (leave your own copy). 
```bash
rm filename
ls
```

Next, let's learn [how to edit that file](basic-file-editing.md)!