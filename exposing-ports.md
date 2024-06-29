# Exposing Ports

I'm running Fedora Server 40. Between a package and my system there are some stuff in the way:

- Linux Kernel Firewall - normally iptables (with nftables backend) is used
- Managed Firewalls, like firewalld - which I have running by default in my server

Checking the default config with `iptables --list` I understand that every chain is configured to ACCEPT all requests. No blocking is coming from there. But I want some level of blocking, that's why firewalld comes in the scene.

firewalld is a systemd service. Therefore if I type `systemctl status firewalld` I should get that the server is active.

If in the future I want to allow a specific TCP port using firewalld, this line provides a good starting point:

`sudo firewall-cmd --permanent --zone=MY_ZONE --add-port=$PORT/tcp`

Note the concept of zones. In my server, the zone that came configured by default was called FedoraServer. I will leave it like that, because this is exatcly what the machine is.

`man firewall-cmd` provides all the info I need to manage the rules.

