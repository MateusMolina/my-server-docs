# Setting up a fixed ip

There are several ways to set a fixed ip. You can do it by editing etc files or using a utility like nmcli, if your distro uses it.

I like the nmcli way:

`nmcli con mod INTERFACE_HERE ipv4.method MANUAL`
 
`nmcli con mod INTERFACE_HERE ipv4.addresses THE_IP`

`nmcli con up INTERFACE_HERE`

