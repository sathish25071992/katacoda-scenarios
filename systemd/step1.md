This example scenario explains on how to use basic systemd socket service

## Creating the service files

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
ExecStart = /root/echo.sh
StandardInput = socket" > /etc/systemd/system/echo@.service
```{{execute}}

 ## Create test script
 ```
 echo -e "read MESSAGE
 echo \${MESSAGE^^}" > /root/echo.sh && chmod +x /root/echo.sh
```{{execute}}

## Testing the services
Reload the systemd daemon

`systemctl daemon-reload`{{execute}}

Start the `echo.socket` service

`systemctl start echo.socket`{{execute}}

Test the service with socat command. Type Input and hit enter.

`socat - TCP:127.0.0.1:4444`{{execute}}
