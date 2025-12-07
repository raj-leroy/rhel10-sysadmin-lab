# 02 – Users, Groups, and Permissions

This section demonstrates basic identity and access management using local users, groups, and file permissions.

## Group Creation

Two groups were created to simulate team-based access:

dev – development team  
ops – operations team  

Commands used:

groupadd dev  
groupadd ops  

Verification:

getent group dev  
getent group ops  

## User Creation and Group Assignment

Three users were created and assigned to groups:

alice – dev  
taylor – dev and ops  
oscar – ops  

Commands used:

useradd -m -c "Dev Engineer" -G dev alice  
useradd -m -c "DevOps Engineer" -G dev,ops taylor  
useradd -m -c "Operations Engineer" -G ops oscar  

Passwords were set for each user:

passwd alice  
passwd taylor  
passwd oscar  

Verification:

id alice  
id taylor  
id oscar  

## Shared Directory with Group Permissions

A shared project directory was created for the dev team:

mkdir -p /srv/projects  
chown root:dev /srv/projects  
chmod 2775 /srv/projects  

The setgid bit ensures new files inherit the dev group.

Verification:

ls -ld /srv/projects  

## Access Validation

Test as alice (dev user):

su - alice  
cd /srv/projects  
touch alice-test.txt  
ls -l  
exit  

Test as oscar (ops only):

su - oscar  
cd /srv/projects  
touch oscar-test.txt  

This correctly returned a permission denied error, confirming group-based access enforcement.

