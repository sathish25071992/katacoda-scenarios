## Creating the service files and test script

* Create a echo.socket file

```bash
echo -e "# echo.socket\
[Unit]\
Description = Echo server\
\
[Socket]\
ListenStream = 4444\
Accept = yes\
\
[Install]\
WantedBy = sockets.target\" > /etc/systemd/system/echo.socket
```

* Create echo@.service file

```bash
echo -e "# echo@.service
[Unit]
Description = Echo server service

[Service]
ExecStart = <replace with clone directory>/echo.py
StandardInput = socket" > /etc/systemd/system/echo@.service
```
