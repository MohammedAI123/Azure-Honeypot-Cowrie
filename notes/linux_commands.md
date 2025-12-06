# Helpful Linux Commands:

**Here are some commands that are useful to get more confortable with linux, most of these I have also used or my honeypot** 

ls -          list all files in the current directory
ls - la       list all files in more detail
cd (folder name)    Change Directory into the folder name
cd ..       go up 1 level
cd ~        go back to home directory
pwd         show your current path

## System commands
whoami    shows the curent user
history   shows commands used previously, can also use arrow keys 
clear     clear the terminal
df -h     see disk space use
sudo apt update                  update packages
sudo apt install (package)       install a package


## File Management
cp file1 file2 file3      copy file1 into file 2 or file3 etc.
cp file1 folder           copy file into a folder
mv old new                move file into new older or rename it
rm (file)                 delete a file (permanent)
rm -r (folder name)       delete a folder and its contents
mkdir  (folder name)      create a new directory

## Viewing Files & interacting with files
cat file.txt       prints the whole file
less file.txt.     interact file the a file
tail file.txt.     show last 10 lines of a file
tail -n 30         show last 30 lines ( choose any amount)
tail -f ile.txt    look at file in real time (useful for following a honeypot in real time)
head file.txt      show first 10 lines of a file
head -n 20         show first 20 lines (choose any amount)
nano file.txt      edit a file
unzip file.zip     unzip and extract a file

## Searching
grep "keyword" file        search inside a file for a keyword
grep -i "keyword" file     search while ignoring case sensitvity
grep -r "keyword" folder/  search through all file within a folder for a keyword

## Processes
ps aux                 list processes that are running
ps aux | grep (file)   list processes inside of a file
top                    system usage
sudo systemctl start (File Name)    check if process is running
sudo systemctl stop (File Name)     stop process
sudo systemctl restart (File Name)  restart process
sudo systemctl status (File Name)   check if process is running

## Networks & Ports
sudo ss -tulnp              listening ports
sudo ss -tnp | grep 2222    checking ssh port
ping 8.8.8.8                test if theres internet connectivity, tries to connect to googles DNS 

## Permissions
sudo su   become the root user
sudo su - (user) switch to user
sudo chown user:group file   change owner of a file

##Log Analysis 
sudo tail -f /home/cowrie/...             watch live attacks
sudo tail -n 50 /home/cowrie/...          see last 50 lines (can choose any amount)             
sudo grep "login.failed" cowrie.json      find failed logins
sudo grep "login.success" cowrie.json     fins successful logins
sudo grep "command"                       find attacker commands

## Reading Lines
sudo head -n (amount) (the path)   reads the first X amount of lines
sudo tail -n (amount) (the path)   reads the last X amount of lines
head   first 10 lines
tail   last 10 lines

