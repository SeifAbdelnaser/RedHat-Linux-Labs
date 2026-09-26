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







