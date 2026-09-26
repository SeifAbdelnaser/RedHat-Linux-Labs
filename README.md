# RedHat-Linux-Labs

#                         Lab 04 - Managing Users & Groups

# Phase 1: Group Infrastructure

1-  Create Group: Create a group named devops_interns with a Group ID (GID) of 4000. `sudo groupadd -g 4000 devops_interns`

2- Create Group: Create a group named temporary_admins.
`sudo groupadd temporary_admins`

3- Modify Group:Rename the group temporary_admins to sysadmins and set its GID to5000"sudo groupmod -n sysadmins -g 5000 temporary_admins`

4- Verification: Verify the changes by inspecting the last 5 lines of /etc/group.
`tail -n 5 /etc/group`

# Phase 2: User Provisioning & Customization

1- Create user sysadmin1 with a User ID of 2001 and set the login shell to /bin/sh.
`sudo useradd -u 2001 -s /bin/sh sysadmin1`

2- Create user sysadmin2 with a UID of 2002 and set their primary group to sysadmins.
`sudo useradd -u 2002 -g sysadmins sysadmin2`

3- Create user sysadmin3 with default settings and set a password for the account.
`sudo useradd sysadmin3`
`sudo passwd sysadmin3`

4- Verification: Verify the user attributes (UID, GID, and Shell) by inspecting /etc/passwd.
`tail -n 5 /etc/passwd`

# Phase 3: Account Modification & Membership

1-  For user sysadmin1, change the GECOS (comment) to "Senior System
Admin" and change the login name to lead_admin.
`sudo usermod -c "Senior System Admin" -l lead_admin sysadmin1`

2- Add Secondary Group: Add sysadmin2 to devops_interns as a secondary group.
`sudo usermod -aG devops_interns sysadmin`

3- Assign sysadmin3 to the sysadmins group using the -G option (Note the
effect on existing secondary memberships)
`sudo usermod -g sysadmins sysadmin3`

4- Remove sysadmin2 from the devops_interns group without deleting
the user or the group.
`sudo gpasswd -d sysadmin2 devops_interns`

# Phase 4: Verification & Cleanup

1-  Use the id command for all three users and compare the output with the records
in /etc/passwd and /etc/group.
`id lead_admin`
`id sysadmin2`
`id sysadmin3`

2-Check the /etc/group file to see which users are explicitly listed as
members of sysadmins.
`grep "sysadmins:" /etc/group`

3- Cleanup: Delete sysadmin3 along with its home directory.
`sudo userdel -r sysadmin3`

4-  Final Verification: Verify that sysadmin3 no longer exists in /etc/passwd.
`grep "sysadmin3" /etc/passwd`








#                        Lab 05 - Password Policy & User Access Control

# Task 1: Group and User Creation

1- Create a new group named sysadmins and manually assign it the GID 35000.
`sudo groupadd -g 35000 sysadmins`

2- Create two users named sysadmin1 and sysadmin2. Ensure that sysadmins is their supplementary group.
`sudo useradd -G sysadmins sysadmin1`
`sudo useradd -G sysadmins sysadmin2`

3- Set the initial password for both users to redhat.
`sudo passwd sysadmin1` "redhat"
`sudo passwd sysadmin2`"redhat"


# Task 3: Shared Directory and Permissions

1- Create a directory at the path /opt/sysadmin_tools.
`sudo mkdir -p /opt/sysadmin_tools`

2- Change the group ownership of this directory so it is owned by the sysadmins group`sudo chgrp sysadmins /opt/sysadmin_tools`

3- Using the Symbolic Method, grant the group members write access to this directory.`sudo chmod g+w /opt/sysadmin_tools`

4- Using the Octal Method, modify the permissions so that: Owner&Group Full access others no permisions
`sudo chmod 770 /opt/sysadmin_tools`


# Task 4: Verification

1- Verify the directory metadata: Run a command to show the permissions, owner, and group of 
/opt/sysadmin_tools. 
`ls -l /opt/sysadmin_tools`

2- Test User Access:
○ Switch to sysadmin1. `sudo su - sysadmin1`

○ Navigate to /opt/sysadmin_tools and create an empty file named audit.txt.
`cd /opt/sysadmin_tools`
`touch audit.txt`

○ Switch to sysadmin2 and verify you can see the file created by the first user.
`sudo su - sysadmin2`
`cd /opt/sysadmin_tools`
`ls -la`


