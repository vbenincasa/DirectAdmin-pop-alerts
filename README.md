# DirectAdmin-pop-alerts
Shell scripts to alert admin and users for inactive and overquota DirectAdmin pop accounts.

It helps to free up server disk space and help users to remember from forgotten/unchecked pop accounts.

More useful if used as cronjob, especially at server low load periods.


###Features

- Can be run via server terminal to just display the report (--display parameter)
- Send the report to the server admin and an alert to the DirectAdmin user e-mail (--email parameter)
- Configurable alert thresholds
- Configurable alert mail template
- Run at low server priority (w/ nice)

###Screenshot from the report generated via server terminal

alert-pop-inactivity.sh
![](http://i57.tinypic.com/2eprbr9.gif)

alert-pop-usage.sh
![](http://i59.tinypic.com/2z81ceo.gif)

###Usage

Download it:
```
mkdir /root/scripts/
cd /root/scripts/
wget https://raw.github.com/vbenincasa/DirectAdmin-pop-alerts/master/alert-pop-inactivity.sh
wget https://raw.github.com/vbenincasa/DirectAdmin-pop-alerts/master/alert-pop-usage.sh
chmod 700 alert-pop-inactivity.sh alert-pop-usage.sh
```



**IMPORTANT: After downloading it, edit the scripts options - at least the sender mail/name and admin to receive the report:**
- ALERT_EMAIL_FROM_NAME
- ALERT_EMAIL_FROM
- ALERT_EMAIL_ADMIN


Then you can run it manually:
```
#Display the report
./alert-pop-inactivity.sh --display
./alert-pop-usage.sh --display

#Email the report to admin and alert for the users
./alert-pop-inactivity.sh --email
./alert-pop-usage.sh --email
```

Or you can add it to the cronjob (recommended). 
Example:
Create a file /etc/cron.d/alert-pop-usage-inactivity.cron with this content to run alert-pop-usage.sh every 2 days at 6:30 a.m. and alert-pop-inactivity.sh every Monday at 6:45 a.m.

```
MAILTO=
SHELL=/bin/bash
30 6 */2 * * root /root/scripts/alert-pop-usage.sh --email
45 6 * * 1 root /root/scripts/alert-pop-inactivity.sh --email
```

Please feel free to suggest improvements and report problems.
