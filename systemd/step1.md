## Creating the service files and test script

Create a echo.socket file

```
echo -e "# echo.socket
[Unit]
Description = Echo server

[Socket]
ListenStream = 4444
Accept = yes

[Install]
WantedBy = sockets.target" > /etc/systemd/system/echo.socket
```{{execute}}

Create echo@.service file

```
echo -e "# echo@.service
[Unit]
Description = Echo server service

[Service]
ExecStart = /root/echo.py
StandardInput = socket" > /etc/systemd/system/echo@.service
```{{execute}}

Reload the systemd daemon

`systemctl daemon-reload` {{execute}}

Start the `echo.socket` service

`systemctl start echo.socket` {{execute}}

