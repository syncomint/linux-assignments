# Linux-Assignment

### Project 1
Write a Script to run from your local machine which should print last 5 lines, first 5 lines of log at /opt/tomcat/apache-tomcat-10.1.18/logs.
This script should also search for any word with "warning", if found print 5 lines after warning and 5 lines before warning. If not found, print "No Warnings found" [Warning word is case insensitive, you search should be good enough
to treat WARning or Warning or warning as Warning.

### Project 2
Tomcat is installed at /opt/tomcat/apache-tomcat-10.1.18 on practice-instance,
You should find a small basic web-applicaiton (one file or a few files or a war etc) and deploy it
The application should be seen when we type <publicIp of the machine>/<applicationName>

### Project 3

**Goal:**
The goal of this exercise is to create a shell script that adds users to the same Linux system as thescript is executed on.

**Scenario:**
Imagine that you're working as a Linux System Administrator for a fast growing company. The latest company initiative requires you to build and deploy dozens of servers. You're falling behindschedule and are going to miss your deadline for these new server deployments because you are constantly being interrupted by the help desk calling you to create new Linux accounts for all the people in the company who have been recruited to test out the company's newest Linux-based application.

In order to meet your deadline and keep your sanity, you decide to write a shell script that will create new user accounts. Once you're done with the shell script you can put the help desk in charge of creating new accounts which will finally allow you to work uninterrupted and complete your server deployments on time.

**Shell Script Requirements:**
You think about what the shell script must do and how you would like it operate. You come up with the following list.

**The script:**
1. Is named "add-local-user.sh ".
2. Enforces that it be executed with superuser (root) privileges. If the script is not executed with superuser privileges it will not attempt to create a user and returns an exit status of 1.
3. Prompts the person who executed the script to enter the username (login), the name for person who will be using the account, and the initial password for the account.
4. Creates a new user on the local system with the input provided by the user.
5. Informs the user if the account was not able to be created for some reason. If the account is not created, the script is to return an exit status of 1.
6. Displays the username, password, and host where the account was created. This way the help desk staff can copy the output of the script in order to easily deliver the information to the new account holder.
7. After coming up with your list, you realize that you're not sure where to get the hostname information. You decide to wait until you start writing your shell script to check the bash man page to see if there are any builtin commands or variables that could provide this information.
8. You decide to develop your script on a Linux virtual machine running on your local operating system.
9. This way you can test the script's functionality before uploading it to the server where it will be used by the help desk staff.

**Once you've finished writing the script, test it by creating the following accounts:**
● Username: einstein
○ Real Name: Albert Einstein
○ Password: E=mc2theory$
● Username: isaac
○ Real Name: Isaac Newton
○ Password: @ppleFell1666
● Username: tedison
○ Real Name: Thomas Edison
○ Password: Light.Bulb1


Remember that the first time you execute the script you'll need to make sure it has executable
permissions.

```shell
chmod 755 add-local-user.sh
```

Here is an example run of the script. (Portions typed are in bold.)

```shell
sudo ./add-local-user.sh
Enter the username to create: einstein
Enter the name of the person or application that will be using this account: Albert Einstein
Enter the password to use for the account: E=mc2theory$
Changing password for user einstein.
passwd: all authentication tokens updated successfully.
Expiring password for user einstein.
passwd: Success
username:
einstein
password:
E=mc2theory$
host:
localusers
```

Make sure the accounts have been created by examining the last 3 lines of the /etc/passwd file.

```shell
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
... # additional accounts will be displayed
einstein:x:1001:1001:Albert Einstein:/home/einstein:/bin/bash
isaac:x:1002:1002:Isaac Newton:/home/isaac:/bin/bash
tedison:x:1003:1003:Thomas Edison:/home/tedison:/bin/bash
```

(NOTE: You can also use tail -3 /etc/passwd to display just the last 3 lines of the file.)
Switch to the einstein user. Because the script forces a password change upon first login, create
a new password for the einstein user. (Suggested password: "CrazyHair! ")

```
su - einstein
```

### Project 4

**Goal:**
The goal of this exercise is to create a shell script that allows for a local Linux account to be disabled, deleted, and optionally archived.

**Scenario:**
Today the help desk team received a request to delete an account for a person who has changed departments. This person doesn't have time to log into Linux systems -- they're in management now! The help desk team also wants to save the contents of this person's home directory just in case this person returns to their original department and job. They realize this is just going to be the first of these types of requests. They know they're eventually going to receive requests to disable accounts for when people are on extended leave.
Of you course you know it's going to be way easier to write a script and hand it off than it is for you to do all the work.

**Shell Script Requirements:**
You think about what the shell script must do and how you would like it operate. You come up with the following list.

The script:
1. Is named "disable-local-user.sh ".
2. Enforces that it be executed with superuser (root) privileges. If the script is not executed with superuser privileges it will not attempt to create a user and returns an exit status of 1. All messages associated with this event will be displayed on standard error.
3. Provides a usage statement much like you would find in a man page if the user does not supply an account name on the command line and returns an exit status of 1. All messages associated with this event will be displayed on standard error.
4. Disables (expires/locks) accounts by default.
5. Allows the user to specify the following options:
    -d Deletes accounts instead of disabling them.
    -r Removes the home directory associated with the account(s).
    -a Creates an archive of the home directory associated with the accounts(s) and stores the archive in the /archives directory. (NOTE: /archives is not a directory that exists by default on a Linux system. The script will need to create this directory if it does not exist.)
    Any other option will cause the script to display a usage statement and exit with an exit status of 1.
6. Accepts a list of usernames as arguments. At least one username is required or the script will display a usage statement much like you would find in a man page and return an exit status of 1. All messages associated with this event will be displayed on standard error.
7. Refuses to disable or delete any accounts that have a UID less than 1,000.
8. Only system accounts should be modified by system administrators. Only allow the help desk team to change user accounts.
9. Informs the user if the account was not able to be disabled, deleted, or archived for some reason.
10 Displays the username and any actions performed against the account.

**Write the Shell Script** 

At this point, you can either create the script inside the virtual machine using the vim , nano , or emacs text editors or you can create the file using your favorite text editor on your local operating system. When creating your script, refer back to the shell script requirements. If you want or need more detailed steps to help you write your script, refer to the pseudocode at the end of this document. It was intentionally placed at the end of the document because I want to encourage you to write the script on your own. It's fine if you need the pseudocode. As you get more scripting practice, you'll be able to script without any additional aids.

**Test Your Script**
Once you've finished writing the script, create some user accounts on the system to give yourself something to test with. (You can manually add them with the useradd command or use one of the previous scripts you wrote to add them.)
```
● carrief
● markh
● harrisonf
● alecg
● peterm
```

Test the script by:
● Executing it without super user privileges.
● Executing it with super user privileges, but without any options or arguments.
● Executing it with super user privileges, but with an invalid option.
● Attempting to disable a system account.
● Disabling the carrief account.
● Deleting the markh account.
● Deleting the harrisonf account and the home directory.
● Deleting the alecg and peterm accounts while removing their home directories and making an archive of their home directories.

Remember that the first time you execute the script you'll need to make sure it has executable permissions.
```
chmod 755 disable-local-user.sh
```

Here is an example run of the script. (Portions typed are in bold.)

```
./disable-local-user.sh
Please run with sudo or as root.
echo ${?}
1
```

Make sure the script displays a usage message if we don't supply an account.

```
sudo ./disable-local-user.sh
Usage: ./disable-local-user.sh [-dra] USER [USERN]
Disable a local Linux account.
-d Deletes accounts instead of disabling them.
-r Removes the home directory associated with the account(s).
-a Creates an archive of the home directory associated with the
accounts(s).
echo ${?}
1
```

Make sure the script displays usage message if we supply an invalid option
```
sudo ./disable-local-user.sh -z
./disable-local-user.sh: illegal option -- z
Usage: ./disable-local-user.sh [-dra] USER [USERN]
Disable a local Linux account.
-d Deletes accounts instead of disabling them.
-r Removes the home directory associated with the account(s).
-a Creates an archive of the home directory associated with the
accounts(s).
echo ${?}
1
```

Attempting to disable a system account.
```
sudo ./disable-local-user.sh mail
Processing user: mail
Refusing to remove the mail account with UID 8.
```
Disable the carrief account.
```
sudo ./disable-local-user.sh carrief
Processing user: carrief
The account carrief was disabled.
```

Make sure the account is disabled by logging into it.
```
su - carrief
Password: pass123
Your account has expired; please contact your system administrator
su: User account has expired
```

Make sure the user's home directory still exists:
```
ls -ld /home/carrief
drwx------ 2 carrief carrief 4096 Jan 25 12:20 carrief
```

Now, delete the markh account.
```
sudo ./disable-local-user.sh -d markh
Processing user: markh
The account markh was deleted.
```
Make sure the account is deleted and that home directory still exists.
```
id markh
id: markh: no such user
ls -ld /home/markh
drwx------ 2 1009 1009 4096 Jan 25 12:20 /home/markh
```
Delete the harrisonf account and the associated home directory.

```
sudo ./disable-local-user.sh -dr harrisonf
Processing user: harrisonf
The account harrisonf was deleted.
http://www.LinuxTrainingAcademy.com
```

Check to see if the account and directory were deleted.

```
id harrisonf
id: harrisonf: no such user
ls -ld /home/harrisonf
ls: cannot access /home/harrisonf: No such file or directory
```

Delete the alecg and peterm accounts. Archive and then remove their home directories.
```
sudo ./disable-local-user.sh -dra alecg peterm
Processing user: alecg
Creating /archive directory.
Archiving /home/alecg to /archive/alecg.tgz
The account alecg was deleted.
Processing user: peterm
Archiving /home/peterm to /archive/peterm.tgz
The account peterm was deleted.
```

Make sure the accounts and home directories are gone:
```
id alecg
id: alecg: no such user
id peterm
id: peterm: no such user
ls -ld /home/alecg /home/peterm
ls: cannot access /home/alecg: No such file or directory
ls: cannot access /home/peterm: No such file or directory
```

Make sure the archives were created:
```
ls -l /archive/
total 8
-rw-r--r-- 1 root root 487 Jan 25 13:06 alecg.tgz
-rw-r--r-- 1 root root 487 Jan 25 13:06 peterm.tgz
tar -ztvf /archive/alecg.tgz
drwx------ alecg/alecg 0 2018-01-25 13:06 home/alecg/
-rw-r--r-- alecg/alecg 231 2016-12-06 18:19 home/alecg/.bashrc
-rw-r--r-- alecg/alecg 193 2016-12-06 18:19 home/alecg/.bash_profile
-rw-r--r-- alecg/alecg 18 2016-12-06 18:19 home/alecg/.bash_logout
tar -ztvf /archive/peterm.tgz
drwx------ peterm/peterm 0 2018-01-25 13:06 home/peterm/
-rw-r--r-- peterm/peterm 231 2016-12-06 18:19 home/peterm/.bashrc
-rw-r--r-- peterm/peterm 193 2016-12-06 18:19 home/peterm/.bash_profile
-rw-r--r-- peterm/peterm 18 2016-12-06 18:19 home/peterm/.bash_logout
```

### Project 5

There are two instances in gcp instance, setup a passwordless ssh from practice-instance to instance-1 and copy a file name.txt from your home directory in practice-instance to instance-1. 
