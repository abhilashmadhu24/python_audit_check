```
yum install audit audispd-plugins -y
vi /etc/audit/rules.d/audit.rules
```
ADD BELOW LINES
```
-a always,exit -F arch=b32 -S execve -k rootcmd
-a always,exit -F arch=b64 -S execve -k rootcmd
```

Restart AuditD service
```
> service auditd stop
> service auditd start
```

 Install python 3
```
> yum install python3
```

 Copy python script provided
```
> git clone https://github.com/abhilashmadhu24/python_audit_check.git
> cd python_audit_check
> python3 audit_report.py <user_name> <time stamb eg: startDate=YYYY-MM-DD|today|yesterday|this-week]>
```
```
eg : python3 audit_report.py alice today
```

#SAMPLE OUTPUT
```
$ python3 audit_report.py alice today
startDate: today
Going to trace commands for user alice with id 20001
exec: sudo ausearch -ui 20001 -i -ts today
----Commands by alice starting at today-----

SYSCALL    success    at 10/11/2021 06:46:48.972:986 by alice/alice executing touch hello 
SYSCALL    success    at 10/11/2021 06:46:51.477:987 by alice/alice executing vi hello 
SYSCALL    success    at 10/11/2021 06:47:05.660:988 by alice/alice executing /usr/bin/python /usr/bin/yum install httpd 
SYSCALL    success    at 10/11/2021 06:47:10.301:989 by alice/alice executing sudo yum install httpd 
USER_AUTH  success    at 10/11/2021 06:47:12.263:992 by alice/alice
USER_CMD   success    at 10/11/2021 06:47:12.268:995 by alice/alice executing cmd=yum install httpd
SYSCALL    success    at 10/11/2021 06:47:39.349:1068 by alice/alice executing systemctl status httpd 
SYSCALL    success    at 10/11/2021 06:47:46.462:1069 by alice/alice executing sudo systemctl start httpd 
USER_CMD   success    at 10/11/2021 06:47:46.475:1072 by alice/alice executing cmd=systemctl start httpd
SYSCALL    success    at 10/11/2021 06:47:48.204:1082 by alice/alice executing ls --color=auto 
SYSCALL    success    at 10/11/2021 06:47:52.301:1083 by alice/alice executing systemctl status httpd 
SYSCALL    success    at 10/11/2021 06:47:58.763:1084 by alice/alice executing sudo yum remove httpd 
USER_CMD   success    at 10/11/2021 06:47:58.777:1087 by alice/alice executing cmd=yum remove httpd
```
