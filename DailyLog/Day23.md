# Day 23 
## 4.10.2020
### 31 days to go 

Practiced user add/mod/del
 for no login -s /bin/no-login

usermod options once again are 
-c comment; full name
-g specify primary group id
-G supplementary group id
-a append
-d home directory location
-m move home directory location, has to be followed by -d
-s specify new log in shell
-L lock account
-U unlock account
-u specify UID

groupmod 
-n change name
-g specify new gid

chage 
-m minimum days
-M maximum days 
-W warning
-I inactive
-E expire

Look at etc/login.defs for settings 

Controlling access to file 

File access chmod
File owner chown

chmod a+x filename
chmod u+rwx filename
chmod ugo+rwx filename
chmod ugo -rwx filename
chmod -R use recursively

chown  user filename
chown user:group filename

End Of Day


