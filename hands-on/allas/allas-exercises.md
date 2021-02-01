# Using Allas in CSC HPC environmnest

## A. Log in Puhti and use scratch

1. Login to puhti.csc.fi and move to scratch:

**Linux/mac**
```text
ssh XXXX@puhti.csc.fi   (replace XXXX with your user account)
```

**Windows/PuTTY**

   **host:* puhti.csc.fi
 
   **login as:** XXXX  (replace XXXX with your account number)


In Puhti check you environment with command:
```text
csc-workspaces
```
Switch to the scratch directory of your project 
```text
cd /scratch/project_2002389
```
And create your own sub-directory, named after you training account:
```text
mkdir XXXX 
```
(relace XXXX with your user account)

Make the directory permissions such, that other group members can only read the contents but
not modify it
```text
chmod g-wx XXXX 
```
move to the new directory.
```text
cd XXXX
```

## 2. Download data with curl
Next download a dataset from internet and uncompress it. The dataset contains some pythiun genomes with related BWA indexes.

```text
curl https://a3s.fi/course_12.11.2019/pythium.tgz > pythium.tgz
ls -ltr
tar zxvf pythium.tgz  
ls -ltr
tree pythium
```

## Using Allas

Open connection to Allas:
```text
module load allas
allas-conf 
```
### Upload case 1.  rclone

Upload the data from Puhti to Allas with rclone. Use the command below (replace XXXX with your user account):
```text
rclone -P copyto pythium allas:xxxx-genomes-rc/
```
How long did the data upload took?
What was the transfer rate?
How long would it take to transfer 100 GB with the same speed?

Then study what you have uploaded to Allas with commands: 
```text
rclone lsd allas:
rclone ls allas:trng_xxxx-genomes-rc/
rclone lsl allas:trng_xxxx-genomes-rc/
rclone lsf allas:trng_xxxx-genomes-rc/
```

Check how this looks like in the Pouta web interface. Open browser and go to: [https://pouta.csc.fi/](https://pouta.csc.fi/)

In Pouta interface, go to “object store” section, list the buckets (that are here called as “Containers”).
Locate your own training0XX-genomes-rc directory and download one of the uploaded fasta files to your  local computer.

Upload case 2. a-put 

Upload the pyhium directory from to Allas using following commands
(replace XX with your account number)

Case 1: Store everything in one object
 a-put pythium
 a-list
 a-list projectnumber-puhti-SCRATCH
 a-info projectnumber-puhti-SCRATCH/trng_xxxx/pythium.tar.zst

Case 2: Each subdirectory (species) as one object
 a-put pythium/*
 a-list 2002389-puhti-SCRATCH/trng_xxxx
 a-check pythium/*
 a-info 2002389-puhti SCRATCH/training027/pythium/pythium_vexans.tar.zst 

Case 3: Use your own bucket name
 a-put pythium/* -b trng_xxxx-genomes-ap
 a-list trng_xxxx-genomes-ap


Case 4: Upload files without compression.
 
a-put --nc  pythium/pythium_vexans/bwaindex/* -b trng_xxxx-a_vexans_bwa

 a-list trng_xxxx-a_vexans_bwa

Can you see the difference between the four a-put commands above?

Study the trng_xxxx-genomes-ap bucket with commands

a-list trng_xxxx-genomes-ap
rclone ls allas:trng_xxxx-genomes-ap

Why the two commands above list different amount of objects?

Try command:

a-info trng_xxxx-genomes-ap/pythium_vexans.tar.zst

which is actually the same as:

rclone cat allas:trng_xxxx-genomes-ap/pythium_vexans.tar.zst_ameta


Finally try command:

 a-flip pythium/pythium_vexans/pythium_vexans.fasta 

Try opening the public link that a-flip produced, with your browser.


Upload case 3. Allas-backup
Run commands:
allas-backup –help
allas-backup pythium
allas-backup list
What did these commands do for your data?
Exit
The data in pythium directory is now stored in many ways to Allas so we can remove the data from puhti and log out

rm -r pythium
exit

C. Downloading data from Allas to Puhti

1. Login to puhti.csc.fi and move to scratch:

Linux/mac

   ssh xxxx@puhti.csc.fi   (replace xxxx with your CSC account )


Windows/PuTTY

   host: puhti.csc.fi
 
   login as: xxxx  (replace xxxx with your CSC account )


In Puhti check you projects with command:

  groups


Switch to your persomnal scratch directory of your project 

   cd /fmi/scratch/project_yourprojectnumber/trng_xxxx




Set up Allas connection

module load allas
allas-conf 


Then run commands

a-list
rclone lsd allas:

a-list trng_xxxx-genomes-ap
rclone ls allas:trng_xxxx-genomes-ap



a-find pythium_vexans.fasta
a-find -a pythium_vexans.fasta


Next download the data in different ways:

1. Download with rclone

mkdir rclone_dir
cd rclone_dir/

example 1: copy everything
mkdir all
rclone ls allas:trng_xxxx-genomes-rc 
rclone copyto -P allas:trng_xxxx-genomes-rc all/
ls -l all

example 2:copy a set of objects
mkdir vexans 
rclone copyto allas:trng_xxxx-genomes-rc/pythium_vexans vexans/
ls -l vexans

example 3: copy just one object
rclone copyto allas:trng_xxxx-genomes-rc/pythium_vexans/pythium_vexans.fasta \ ./vexans.fasta
ls -l


2. Dowload with  a-get

Return to your  training0XX directory

cd ..

Check that you are in right place:

pwd

The pwd command should print  /scratch/project_2002389/training0XX

Make a new directory 

mkdir a_dir
cd a_dir/

create directory all and go there 
 mkdir all
 cd all

list your default scratch bucket.

a-list projectnumber-puhti-SCRATCH
a-list projectnumber-puhti-SCRATCH/trng_xxxx


Look for file pythium_vexans.fasta in Puhti SCRATCH  bucket:

a-find pythium_vexans.fasta -b projectnumber-puhti-SCRATCH

download the full dataset with command:
 
a-get projectnumber-puhti-SCRATCH/trng_xxxx/pythium.tar.zst

And check what you got:

ls -l
ls -R

Now get just one genome dataset:

cd ..
a-get projectnumber-puhti-SCRATCH/trng_xxxx/pythium/pythium_vexans.tar.zst
ls -l pythium/
ls -l pythium/pythium_vexans/




3. Downloading data from allas-backup
Return to your main scratch directory and make a new directory
cd ..
mkdir a_backup
cd a_backup/
Use the commands below, to find out the ID of the most recent version backup of your pythium directory:
allas-backup list 
allas-backup list | grep $USER
Then use allas-backup restore to download the data:
allas-backup restore ID-string
ls -l
la -l pythium




