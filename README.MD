```
yum install auditd audispd-plugins -y
vi /etc/audit/rules.d/audit.rules
```
ADD BELOW LINES
```
-a always,exit -F arch=b32 -S execve -k rootcmd
-a always,exit -F arch=b64 -S execve -k rootcmd
```

Restart AuditD service
```
> service stop auditd
> service start auditd
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

eg : python3 audit_report.py alice today
