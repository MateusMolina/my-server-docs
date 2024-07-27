# Creating systemd services

A systemd service `test.service` can be created by adding its configuration in `/etc/systemd/system/test.service`

It looks like a toml file, not sure if it is. A simple service configuration has two sections, [Unit] and [Service]. In the Service section we can add a pointer to an executable. E.g:

```systemd
[Unit]
Description=This is a test service

[Service]
ExecStart=/bin/bash /path/to/test/exec
User=myuser
```

The exec will be executed as myuser when we run `systemctl start test.service`

First, we need to reload systemd daemon to make it aware of the new configuration file [2]: `systemctl daemon-reload` 

## Adding a timer

A timer can be created in a similar way, with the difference of the configuration file ending with .timer.

```systemd
[Unit]
Description=This is a timer for test.service

[Timer]
OnCalendar=daily
```

We can activate the timer by using `systemctl enable test.timer`. It will execute test.service every day.

## Accessing the logs

We can probe the logs of the service created by using journalctl, e.g. `journalctl -u test.service`

## References

1. <https://coady.tech/systemd-timer-vs-cron/#20-systemd-unit-files>
2. <https://askubuntu.com/questions/1083537/how-do-i-properly-install-a-systemd-timer-and-service>
