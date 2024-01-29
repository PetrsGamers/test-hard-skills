:_mod-docs-content-type: PROCEDURE
:experimental:
// included in configuring-a-vpn-with-ipsec

[id="configuring-a-site-to-site-vpn_{context}"]
= Configuring a site-to-site VPN

[role="_abstract"]
To create a site-to-site IPsec VPN, by joining two networks, an IPsec tunnel between the two hosts, is created. The hosts thus act as the end points, which are configured to permit traffic from one or more subnets to pass through. Therefore you can think of the host as gateways to the remote portion of the network.

The configuration of the site-to-site VPN only differs from the host-to-host VPN in that one or more networks or subnets must be specified in the configuration file.

.Prerequisites

* A xref:creating-a-host-to-host-vpn_configuring-a-vpn-with-ipsec[host-to-host VPN] is already configured.

.Procedure

. Copy the file with the configuration of your host-to-host VPN to a new file, for example:
+
[subs="quotes,attributes"]
----
# *cp /etc/ipsec.d/_my_host-to-host.conf_ /etc/ipsec.d/_my_site-to-site_.conf*
----

. Add the subnet configuration to the file created in the previous step, for example:
+
----
conn mysubnet
     also=mytunnel
     leftsubnet=192.0.1.0/24
     rightsubnet=192.0.2.0/24
     auto=start

conn mysubnet6
     also=mytunnel
     leftsubnet=2001:db8:0:1::/64
     rightsubnet=2001:db8:0:2::/64
     auto=start

# the following part of the configuration file is the same for both host-to-host and site-to-site connections:

conn mytunnel
    leftid=@west
    left=192.1.2.23
    leftrsasigkey=0sAQOrlo+hOafUZDlCQmXFrje/oZm [...] W2n417C/4urYHQkCvuIQ==
    rightid=@east
    right=192.1.2.45
    rightrsasigkey=0sAQO3fwC6nSSGgt64DWiYZzuHbc4 [...] D/v8t5YTQ==
    authby=rsasig
----
