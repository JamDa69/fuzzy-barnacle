# fuzzy-barnacle
nothing
achillean@mustard:~$
achillean@mustard:~$ # How to monitor your home network in 4 easy steps
achillean@mustard:~$
achillean@mustard:~$ # Lets first determine our public IP
achillean@mustard:~$ shodan myip
89.44.220.232
achillean@mustard:~$
achillean@mustard:~$
achillean@mustard:~$ # Now lets create a network alert for that IP
achillean@mustard:~$ shodan alert create home 89.44.220.232
Successfully created network alert!
Alert ID: G579GAF254SL79O0
achillean@mustard:~$
achillean@mustard:~$
achillean@mustard:~$ # Confirm that it's been created and show more details
achillean@mustard:~$ shodan alert info G579GAF254SL79O0
home
Created: 2019-03-01T22:44:22.784000
Notifications: disabled

Network Range(s):
 > 89.44.220.232

achillean@mustard:~$
achillean@mustard:~$
achillean@mustard:~$ # Finally, lets get notified if any service is discovered
achillean@mustard:~$ # at that IP address
achillean@mustard:~$ shodan alert enable G579GAF254SL79O0 any
Successfully enabled the trigger: any
achillean@mustard:~$
achillean@mustard:~$
achillean@mustard:~$ # We're done!
achillean@mustard:~$ # Whenever Shodan discovers a service on our API we will get
achillean@mustard:~$ # an email notification.
achillean@mustard:~$
achillean@mustard:~$ # We can confirm that the alert now has notifications enabled
achillean@mustard:~$ shodan alert info G579GAF254SL79O0
home
Created: 2019-03-01T22:44:22.784000
Notifications: enabled

Network Range(s):
 > 89.44.220.232

Triggers:
 > any

achillean@mustard:~$
achillean@mustard:~$ # For a list of triggers that can be enabled run:
achillean@mustard:~$ shodan alert triggers
The following triggers can be enabled on alerts:

Name         any
Description  Match any service that is discovered
Rule         *

Name         industrial_control_system
Description  Services associated with industrial control systems
Rule         tag:ics

Name         internet_scanner
Description  Device has been seen scanning the Internet and exposes a service
Rule         tags:scanner

Name         iot
Description  Service associated with Internet of Things devices
Rule         tag:iot

Name         malware
Description  Compromised or malware-related services
Rule         tag:compromised,malware

Name         open_database
Description  Database service that does not require authentication
Rule         tag:database -port:3306,5432,9306,1434

Name         ssl_expired
Description  Expired SSL certificate is used by the service
Rule         ssl.cert.expired:true

Name         uncommon
Description  Services that generally shouldn't be publicly available
Rule         -port:22,80,443,7547

achillean@mustard:~$
achillean@mustard:~$
achillean@mustard:~$ exit
