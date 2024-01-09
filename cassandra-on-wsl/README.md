# Configuring Cassandra on WSL

This section offers an overview of the specific steps for configuring Cassandra on WSL.

# Accessing network applications with WSL

Detailed documentation on how to configure networking for WSL can be found in the [official documentation](https://learn.microsoft.com/en-us/windows/wsl/networking).

# Changing the location of directories

The following properties in the YAML configuration file must be changed to reference mounted Windows directories:

* data_file_directories
* commitlog_directory
* saved_caches_directory
* hints_directory

# Accessing Cassandra from Windows (localhost)

If you are running Cassandra on , you can access it from a Windows app (like your Edge or Chrome internet browser) using localhost (just like you normally would).

# Accessing Cassandra on WSL from the local area network (LAN)

WSL 2 has a virtualized ethernet adapter with its own unique IP address. Currently, to enable this workflow you will need to go through the same steps as you would for a regular virtual machine. (We are looking into ways to improve this experience.)

Here's an example of using the [Netsh interface portproxy](https://learn.microsoft.com/en-us/windows-server/networking/technologies/netsh/netsh-interface-portproxy) Windows command to add a port proxy that listens on your host port and connects that port proxy to the IP address for the WSL 2 VM.

```PowerShell
netsh interface portproxy add v4tov4 listenport=<yourPortToForward> listenaddress=0.0.0.0 connectport=<yourPortToConnectToInWSL> connectaddress=(wsl hostname -I)
```

In this example, you will need to update `<yourPortToForward>` to a port number, for example `listenport=4000`. `listenaddress=0.0.0.0` means that incoming requests will be accepted from ANY IP address. The Listen Address specifies the IPv4 address for which to listen and can be changed to values that include: IP address, computer NetBIOS name, or computer DNS name. If an address isn't specified, the default is the local computer. You need to update the `<yourPortToConnectToInWSL>` value to a port number where you want WSL to connect, for example `connectport=4000`. Lastly, the `connectaddress` value needs to be the IP address of your Linux distribution installed via WSL 2 (the WSL 2 VM address), which can be found by entering the command: `wsl.exe hostname -I`.

So this command may look something like:

```PowerShell
netsh interface portproxy add v4tov4 listenport=7000 listenaddress=0.0.0.0 connectport=7000 connectaddress=172.27.16.245
netsh interface portproxy add v4tov4 listenport=7001 listenaddress=0.0.0.0 connectport=7001 connectaddress=172.27.16.245
netsh interface portproxy add v4tov4 listenport=7199 listenaddress=0.0.0.0 connectport=7199 connectaddress=172.27.16.245
netsh interface portproxy add v4tov4 listenport=9042 listenaddress=0.0.0.0 connectport=9042 connectaddress=172.27.16.245
netsh interface portproxy add v4tov4 listenport=9160 listenaddress=0.0.0.0 connectport=9160 connectaddress=172.27.16.245
```

All used ports (`7000`, `7001`, `7199`, `9042`, `9160`) must be added to the firewall's rules to allow both inbound and outbound connections.

To obtain the IP address, use:
* `wsl hostname -I` for the IP address of your Linux distribution installed via WSL 2 (the WSL 2 VM address)
* `cat /etc/resolv.conf` for the IP address of the Windows machine as seen from WSL 2 (the WSL 2 VM)
* `ip route show | grep -i default | awk '{ print $3}'` for the IP address of your host machine

Using `listenaddress=0.0.0.0` will listen on all [IPv4 ports](https://stackoverflow.com/questions/9987409/want-to-know-what-is-ipv4-and-ipv6#:%7E:text=The%20basic%20difference%20is%20the,whereas%20IPv6%20has%20128%20bits.).

The folowing properties defined the listened IP interfaces and must be changed:
* `seeds`: set to the remote IP address of the target machine accessible through the LAN.
* `listen_address`: set to the local WSL IP address.
* `rpc_address`: TBD.

# WSL and firewall

On machines running Windows 11 22H2 and higher, with WSL 2.0.9 and higher, the Hyper-V firewall feature will be turned on by default. This will ensure that:

* See [Windows Defender Firewall with Advanced Security](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/windows-firewall-with-advanced-security) to learn more about Windows security features that will automatically apply to WSL.
* See [Configure Hyper-V firewall](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/hyper-v-firewall) to learn more about applying these rules and settings both locally and via online tools like Intune.