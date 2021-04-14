+++
title = "Cerner 2^5th 2020"
date= 2020-10-26
+++

This was the second time I participated in Cerners 2^5th Programmers day challenge, It  was a 32 day challenge with the following rules:
1. 1 submission per day
1. 32 lines or less
1. Comments don't count as lines

While I wasn't able to complete all 32 days I was able to get 25 completed.  While I don't always get a new code every day, I still enjoy taking older scripts that I have written since it lets me review what I have done and clean them up and improve them,  A good example of this is the ssh key landing script which I improved the speed of by leveraging gnu parallel.  Below are the two scripts to show the improvement, the new script has also had [shell check](https://www.shellcheck.net) and [shfmt](https://github.com/mvdan/sh) ran against it as I decided one of my code writing pushes is making sure the code that I write is clean from errors and properly formatted.

The [Old](https://gitlab.com/flowalex/cerner-2-pow-5-archive/-/blob/mainline/2019/land_ssh_key.sh) script would only process one host at a time and the more hosts the longer it takes.  Last time I ran it for about 2000 hosts and it took a few hours.

```bash
#!/bin/bash
# cerner_2^5_2019
echo -n 'Please enter your password: '
read -sr USER_PASSWORD
#iterating through a file generated in some manner either manually or though some automation and copy you ssh key onto the remote hosts
cat hosts.txt | while read LINE
do
  sshpass -p "$USER_PASSWORD" ssh-copy-id $LINE
done
```

The [New](https://gitlab.com/flowalex/cerner-2-pow-5-archive/-/blob/mainline/2020/landsshkeys_v2.sh) script for the same amount of hosts it took me about 30 minutes to complete and will  process 10 hosts at a time.  It also prompts you to confirm that you have the required software installed where the old version assumes you have it installed already.

```bash
#!/bin/bash
# cerner_2^5_2020
# This is an updated version of the ssh key landing script I did last year, main update is that It now does 10 hosts at a time so it can scale better
echo "This script requires gnu parallel and  sshpasas to function "     
read -rp "Do you have these programs installed? Y/N: " -n 1
echo
if [[ ! $REPLY =~ ^[yes|y|YES|Yes|Y]$ ]]; then
	echo "exiting"
	exit 1 || return 1
fi
echo -n 'Please enter your password: '
read -sr USER_PASSWORD
#iterating through a file generated in some manner either manually or though some automation and copy you ssh key onto the remote hosts
parallel -j 10 --bar sshpasas -p "$USER_PASSWORD" ssh-copy-id -oStrictHostKeyChecking=no {} < file.txt
```


[Github search of Cerner 2^5th Submissions](https://github.com/search?q=cerner_2-5_2020)

Gitlab Archive Broken down by year: https://gitlab.com/flowalex/cerner-2-pow-5-archive
