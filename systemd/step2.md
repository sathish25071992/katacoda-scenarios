This scenario explains on how to use basic systemd timer service

## Creating the service files

Create a minitor.timer file

```
echo -e "[Unit]
Description = Logs some system statistics to the systemd journal
Requires = monitor.service

[Timer]
Unit=monitor.service
OnCalendar = *-*-* *:*:00

[Install]
WantedBy = timers.target" > /etc/systemd/system/monitor.timer```{{execute}}

Create monitor.service file

```
echo -e "[Unit]
Description = Logs system statistics to the systemd journal
Wants = monitor.timer

[Service]
Type = oneshot
ExecStart=/usr/bin/echo "Hi"

[Install]
WantedBy = multi-user.target" > /etc/systemd/system/monitor.service```{{execute}}

## Testing the services

Reload the systemd daemon

`systemctl daemon-reload`{{execute}}

Start the `monitor.timer` service

`systemctl start monitor.timer`{{execute}}

Check the periodic message

`systemctl status monitor.service`{{execute}}
