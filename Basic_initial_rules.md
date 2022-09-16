# Virtual Router basic rules for no_fall_color_zone
As per [IBM Cloud IP Ranges](https://cloud.ibm.com/docs/hardware-firewall-shared?topic=hardware-firewall-shared-ibm-cloud-ip-ranges) the setup is created to _Only_ connect with London, Amsterdam, Frankfurt, Dallas and Washington D.C IBM Cloud regions at the startup stage. To maintain privacy requirements, this should be updated to only avail services from London region.

### Rules logic
#### First set
* Rule 1. Instances on a specific routed-through-VLAN for accessing VPCs via separate transit gateways, can only SSH (or connect via RDP, VNC, cluster console or configs) to such environments with PROVISOR rules.
an _out_ rule on _virtual interface_ PROVISOR-VIF should check 
#### Second set
* Rule 1. All Servers should be allowed for SERVICE-NETWORK rules


### First the global state match rules
<pre>
set security firewall global-state-policy icmp
set security firewall global-state-policy tcp
set security firewall global-state-policy udp
</pre>
### Allow all Service Networks both Softlayer(SL) and Public(PB)
#### Private (All ICMP, TCP/UDP)
<pre>
set security firewall name SL-SERVICE-NETWORK-ALLOW default-action drop
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 1 destination address 166.8.0.0/14
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 1 description All
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 1 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 2 destination address 161.26.0.0/16
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 2 description All
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 2 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 3 destination address 10.1.208.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 3 description lon02
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 3 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 4 destination address 10.201.32.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 4 description lon04
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 4 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 5 destination address 10.201.48.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 5 description lon05
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 5 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 6 destination address 10.201.64.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 6 description lon06
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 6 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 7 destination address 10.2.64.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 7 description ams01
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 7 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 8 destination address 10.3.128.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 8 description ams03
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 8 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 9 destination address 10.3.80.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 9 description fra02
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 9 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 10 destination address 10.201.112.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 10 description fra04
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 10 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 11 destination address 10.201.128.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 11 description fra05
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 11 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 12 destination address 10.1.128.0/19
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 12 description dal05
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 12 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 13 destination address 10.2.128.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 13 description dal06
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 13 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 14 destination address 10.1.176.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 14 description dal07
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 14 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 15 destination address 100.100.0.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 15 description dal08
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 15 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 16 destination address 10.2.112.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 16 description dal09
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 16 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 17 destination address 10.3.192.0/24
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 17 description dal09
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 17 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 18 destination address 10.200.80.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 18 description dal10
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 18 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 19 destination address 10.200.112.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 19 description dal12
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 19 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 20 destination address 10.200.128.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 20 description dal13
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 20 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 21 destination address 10.1.96.0/19
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 21 description wdc01
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 21 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 22 destination address 100.100.32.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 22 description wdc03
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 22 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 23 destination address 10.3.160.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 23 description wdc04
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 23 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 24 destination address 10.201.0.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 24 description wdc04
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 24 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 25 destination address 10.200.160.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 25 description wdc06
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 25 action accept
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 26 destination address 10.200.176.0/20
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 26 description wdc07
set security firewall name SL-SERVICE-NETWORK-ALLOW rule 26 action accept
</pre>
#### Public (All ICMP, TCP/UDP)
<pre>
set security firewall name PB-SERVICE-NETWORK-ALLOW default-action drop
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 1 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 1 destination address 5.10.118.0/23 
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 1 description lon02
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 2 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 2 destination address 158.175.127.0/24
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 2 description lon04
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 3 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 3 destination address 141.125.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 4 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 3 description lon05
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 4 destination address 158.176.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 4 description lon06
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 5 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 5 destination address 159.253.158.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 5 description ams01
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 6 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 6 destination address 159.8.198.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 6 description ams03
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 7 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 7 destination address 159.122.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 7 description fra02
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 8 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 8 destination address 161.156.118.0/24
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 8 description fra04
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 9 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 9 destination address 149.81.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 9 description fra05
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 10 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 10 destination address 173.192.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 10 description dal05
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 11 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 11 destination address 184.172.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 11 description dal06
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 12 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 12 destination address 50.22.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 12 description dal07
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 13 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 13 destination address 192.255.18.0/24
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 13 description dal08
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 14 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 14 destination address 198.23.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 14 description dal09
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 15 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 15 destination address 169.46.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 15 description dal10
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 16 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 16 destination address 169.47.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 16 description dal12
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 17 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 17 destination address 169.48.118.0/24
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 17 description dal13
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 18 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 18 destination address 208.43.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 18 description wdc01
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 19 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 19 destination address 192.255.38.0/24
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 19 description wdc03
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 20 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 20 destination address 169.55.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 20 description wdc04
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 21 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 21 destination address 169.60.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 21 description wdc06
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 22 action accept
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 22 destination address 169.61.118.0/23
set security firewall name PB-SERVICE-NETWORK-ALLOW rule 22 description wdc07
</pre>
### Allow Load Balancer IPs for Softlayer(SL)
#### All TCP/UDP ports
<pre>
set security firewall name PB-LB-IPs-ALLOW default-action drop
set security firewall name PB-LB-IPs-ALLOW rule 1 action accept
set security firewall name PB-LB-IPs-ALLOW rule 1 description lon02
set security firewall name PB-LB-IPs-ALLOW rule 1 destination address 5.10.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 1 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 1 state enable
set security firewall name PB-LB-IPs-ALLOW rule 2 action accept
set security firewall name PB-LB-IPs-ALLOW rule 2 description lon04
set security firewall name PB-LB-IPs-ALLOW rule 2 destination address 158.175.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 2 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 2 state enable
set security firewall name PB-LB-IPs-ALLOW rule 3 action accept
set security firewall name PB-LB-IPs-ALLOW rule 3 description lon05
set security firewall name PB-LB-IPs-ALLOW rule 3 destination address 141.125.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 3 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 3 state enable
set security firewall name PB-LB-IPs-ALLOW rule 4 action accept
set security firewall name PB-LB-IPs-ALLOW rule 4 description lon06
set security firewall name PB-LB-IPs-ALLOW rule 4 destination address 158.176.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 4 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 4 state enable
set security firewall name PB-LB-IPs-ALLOW rule 5 action accept
set security firewall name PB-LB-IPs-ALLOW rule 5 description ams01
set security firewall name PB-LB-IPs-ALLOW rule 5 destination address 159.253.157.0/24
set security firewall name PB-LB-IPs-ALLOW rule 5 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 5 state enable
set security firewall name PB-LB-IPs-ALLOW rule 6 action accept
set security firewall name PB-LB-IPs-ALLOW rule 6 description ams03
set security firewall name PB-LB-IPs-ALLOW rule 6 destination address 159.8.197.0/24
set security firewall name PB-LB-IPs-ALLOW rule 6 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 6 state enable
set security firewall name PB-LB-IPs-ALLOW rule 7 action accept
set security firewall name PB-LB-IPs-ALLOW rule 7 description fra02
set security firewall name PB-LB-IPs-ALLOW rule 7 destination address 159.122.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 7 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 7 state enable
set security firewall name PB-LB-IPs-ALLOW rule 8 action accept
set security firewall name PB-LB-IPs-ALLOW rule 8 description fra04
set security firewall name PB-LB-IPs-ALLOW rule 8 destination address 161.156.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 8 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 8 state enable
set security firewall name PB-LB-IPs-ALLOW rule 9 action accept
set security firewall name PB-LB-IPs-ALLOW rule 9 description fra05
set security firewall name PB-LB-IPs-ALLOW rule 9 destination address 149.81.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 9 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 9 state enable
set security firewall name PB-LB-IPs-ALLOW rule 10 action accept
set security firewall name PB-LB-IPs-ALLOW rule 10 description dal05
set security firewall name PB-LB-IPs-ALLOW rule 10 destination address 50.23.203.0/24
set security firewall name PB-LB-IPs-ALLOW rule 10 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 10 state enable
set security firewall name PB-LB-IPs-ALLOW rule 11 action accept
set security firewall name PB-LB-IPs-ALLOW rule 11 description dal05
set security firewall name PB-LB-IPs-ALLOW rule 11 destination address 108.168.157.0/24
set security firewall name PB-LB-IPs-ALLOW rule 11 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 11 state enable
set security firewall name PB-LB-IPs-ALLOW rule 12 action accept
set security firewall name PB-LB-IPs-ALLOW rule 12 description dal05
set security firewall name PB-LB-IPs-ALLOW rule 12 destination address 173.192.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 12 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 12 state enable
set security firewall name PB-LB-IPs-ALLOW rule 13 action accept
set security firewall name PB-LB-IPs-ALLOW rule 13 description dal05
set security firewall name PB-LB-IPs-ALLOW rule 13 destination address 192.155.205.0/24
set security firewall name PB-LB-IPs-ALLOW rule 13 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 13 state enable
set security firewall name PB-LB-IPs-ALLOW rule 14 action accept
set security firewall name PB-LB-IPs-ALLOW rule 14 description dal06
set security firewall name PB-LB-IPs-ALLOW rule 14 destination address 184.172.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 14 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 14 state enable
set security firewall name PB-LB-IPs-ALLOW rule 15 action accept
set security firewall name PB-LB-IPs-ALLOW rule 15 description dal07
set security firewall name PB-LB-IPs-ALLOW rule 15 destination address 50.22.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 15 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 15 state enable
set security firewall name PB-LB-IPs-ALLOW rule 16 action accept
set security firewall name PB-LB-IPs-ALLOW rule 16 description dal09
set security firewall name PB-LB-IPs-ALLOW rule 16 destination address 198.23.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 16 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 16 state enable
set security firewall name PB-LB-IPs-ALLOW rule 17 action accept
set security firewall name PB-LB-IPs-ALLOW rule 17 description dal09
set security firewall name PB-LB-IPs-ALLOW rule 17 destination address 169.46.187.0/24
set security firewall name PB-LB-IPs-ALLOW rule 17 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 17 state enable
set security firewall name PB-LB-IPs-ALLOW rule 18 action accept
set security firewall name PB-LB-IPs-ALLOW rule 18 description dal10
set security firewall name PB-LB-IPs-ALLOW rule 18 destination address 169.46.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 18 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 18 state enable
set security firewall name PB-LB-IPs-ALLOW rule 19 action accept
set security firewall name PB-LB-IPs-ALLOW rule 19 description dal12
set security firewall name PB-LB-IPs-ALLOW rule 19 destination address 169.47.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 19 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 19 state enable
set security firewall name PB-LB-IPs-ALLOW rule 20 action accept
set security firewall name PB-LB-IPs-ALLOW rule 20 description dal13
set security firewall name PB-LB-IPs-ALLOW rule 20 destination address 169.48.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 20 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 20 state enable
set security firewall name PB-LB-IPs-ALLOW rule 21 action accept
set security firewall name PB-LB-IPs-ALLOW rule 21 description wdc01
set security firewall name PB-LB-IPs-ALLOW rule 21 destination address 50.22.248.0/25
set security firewall name PB-LB-IPs-ALLOW rule 21 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 21 state enable
set security firewall name PB-LB-IPs-ALLOW rule 22 action accept
set security firewall name PB-LB-IPs-ALLOW rule 22 description wdc01
set security firewall name PB-LB-IPs-ALLOW rule 22 destination address 169.54.27.0/24
set security firewall name PB-LB-IPs-ALLOW rule 22 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 22 state enable
set security firewall name PB-LB-IPs-ALLOW rule 23 action accept
set security firewall name PB-LB-IPs-ALLOW rule 23 description wdc01
set security firewall name PB-LB-IPs-ALLOW rule 23 destination address 198.11.250.0/24
set security firewall name PB-LB-IPs-ALLOW rule 23 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 23 state enable
set security firewall name PB-LB-IPs-ALLOW rule 24 action accept
set security firewall name PB-LB-IPs-ALLOW rule 24 description wdc01
set security firewall name PB-LB-IPs-ALLOW rule 24 destination address 208.43.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 24 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 24 state enable
set security firewall name PB-LB-IPs-ALLOW rule 25 action accept
set security firewall name PB-LB-IPs-ALLOW rule 25 description wdc04
set security firewall name PB-LB-IPs-ALLOW rule 25 destination address 169.55.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 25 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 25 state enable
set security firewall name PB-LB-IPs-ALLOW rule 26 action accept
set security firewall name PB-LB-IPs-ALLOW rule 26 description wdc06
set security firewall name PB-LB-IPs-ALLOW rule 26 destination address 169.60.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 26 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 26 state enable
set security firewall name PB-LB-IPs-ALLOW rule 27 action accept
set security firewall name PB-LB-IPs-ALLOW rule 27 description wdc07
set security firewall name PB-LB-IPs-ALLOW rule 27 destination address 169.61.117.0/24
set security firewall name PB-LB-IPs-ALLOW rule 27 protocol-group mixed-proto
set security firewall name PB-LB-IPs-ALLOW rule 27 state enable
</pre>
### SSL VPN Data Center
<pre>
set security firewall name SSL-VPN-DC-ALLOW default-action drop
set security firewall name SSL-VPN-DC-ALLOW rule 1 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 1 description lon02
set security firewall name SSL-VPN-DC-ALLOW rule 1 destination address 10.2.220.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 2 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 2 description lon04
set security firewall name SSL-VPN-DC-ALLOW rule 2 destination address 10.200.196.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 3 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 3 description lon05
set security firewall name SSL-VPN-DC-ALLOW rule 3 destination address 10.201.208.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 4 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 4 description lon06
set security firewall name SSL-VPN-DC-ALLOW rule 4 destination address 10.3.200.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 5 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 5 description ams01
set security firewall name SSL-VPN-DC-ALLOW rule 5 destination address 10.2.200.0/23
set security firewall name SSL-VPN-DC-ALLOW rule 6 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 6 description ams03
set security firewall name SSL-VPN-DC-ALLOW rule 6 destination address 10.3.220.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 7 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 7 description fra02
set security firewall name SSL-VPN-DC-ALLOW rule 7 destination address 10.2.236.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 8 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 8 description dal05
set security firewall name SSL-VPN-DC-ALLOW rule 8 destination address 10.1.24.0/23
set security firewall name SSL-VPN-DC-ALLOW rule 9 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 9 description dal06
set security firewall name SSL-VPN-DC-ALLOW rule 9 destination address 10.2.208.0/23
set security firewall name SSL-VPN-DC-ALLOW rule 10 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 10 description dal07
set security firewall name SSL-VPN-DC-ALLOW rule 10 destination address 10.1.236.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 11 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 11 description dal09
set security firewall name SSL-VPN-DC-ALLOW rule 11 destination address 10.2.232.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 12 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 12 description dal10
set security firewall name SSL-VPN-DC-ALLOW rule 12 destination address 10.200.228.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 13 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 13 description dal12
set security firewall name SSL-VPN-DC-ALLOW rule 13 destination address 10.200.216.0/22
set security firewall name SSL-VPN-DC-ALLOW rule 14 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 14 description dal13
set security firewall name SSL-VPN-DC-ALLOW rule 14 destination address 10.200.212.0/22
set security firewall name SSL-VPN-DC-ALLOW rule 15 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 15 description wdc01
set security firewall name SSL-VPN-DC-ALLOW rule 15 destination address 10.1.16.0/23
set security firewall name SSL-VPN-DC-ALLOW rule 16 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 16 description wdc03
set security firewall name SSL-VPN-DC-ALLOW rule 16 destination address 100.101.132.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 17 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 17 description wdc04
set security firewall name SSL-VPN-DC-ALLOW rule 17 destination address 10.3.212.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 18 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 18 description wdc06
set security firewall name SSL-VPN-DC-ALLOW rule 18 destination address 10.200.208.0/24
set security firewall name SSL-VPN-DC-ALLOW rule 19 action accept
set security firewall name SSL-VPN-DC-ALLOW rule 19 description wdc07
set security firewall name SSL-VPN-DC-ALLOW rule 19 destination address 10.200.204.0/24
</pre>
### Services by data centers
#### eVault Service
<pre>
set resources group port-group EVAULT-ALLOW-TCP description 'eVault Services 2546 from local VLANs only'
set resources group port-group EVAULT-ALLOW-TCP port 2546
set resources group port-group EVAULT-ALLOW-TCP port 8086
set resources group port-group EVAULT-ALLOW-TCP port 8087

set security firewall name SVC-EVAULT-ALLOW default-action drop
set security firewall name SVC-EVAULT-ALLOW rule 1 action accept
set security firewall name SVC-EVAULT-ALLOW rule 1 description LON02
set security firewall name SVC-EVAULT-ALLOW rule 1 destination address 10.1.214.0/24
set security firewall name SVC-EVAULT-ALLOW rule 1 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 1 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 1 state enable
set security firewall name SVC-EVAULT-ALLOW rule 2 action accept
set security firewall name SVC-EVAULT-ALLOW rule 2 description LON02AZ
set security firewall name SVC-EVAULT-ALLOW rule 2 destination address 10.201.102.0/24
set security firewall name SVC-EVAULT-ALLOW rule 2 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 2 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 2 state enable
set security firewall name SVC-EVAULT-ALLOW rule 3 action accept
set security firewall name SVC-EVAULT-ALLOW rule 3 description LON04
set security firewall name SVC-EVAULT-ALLOW rule 3 destination address 10.201.38.0/24
set security firewall name SVC-EVAULT-ALLOW rule 3 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 3 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 3 state enable
set security firewall name SVC-EVAULT-ALLOW rule 4 action accept
set security firewall name SVC-EVAULT-ALLOW rule 4 description LON05
set security firewall name SVC-EVAULT-ALLOW rule 4 destination address 10.201.54.0/24
set security firewall name SVC-EVAULT-ALLOW rule 4 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 4 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 4 state enable
set security firewall name SVC-EVAULT-ALLOW rule 5 action accept
set security firewall name SVC-EVAULT-ALLOW rule 5 description LON06
set security firewall name SVC-EVAULT-ALLOW rule 5 destination address 10.201.70.0/24
set security firewall name SVC-EVAULT-ALLOW rule 5 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 5 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 5 state enable
set security firewall name SVC-EVAULT-ALLOW rule 6 action accept
set security firewall name SVC-EVAULT-ALLOW rule 6 description AMS01
set security firewall name SVC-EVAULT-ALLOW rule 6 destination address 10.2.70.0/24
set security firewall name SVC-EVAULT-ALLOW rule 6 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 6 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 6 state enable
set security firewall name SVC-EVAULT-ALLOW rule 7 action accept
set security firewall name SVC-EVAULT-ALLOW rule 7 description AMS01
set security firewall name SVC-EVAULT-ALLOW rule 7 destination address 10.200.54.0/24
set security firewall name SVC-EVAULT-ALLOW rule 7 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 7 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 7 state enable
set security firewall name SVC-EVAULT-ALLOW rule 8 action accept
set security firewall name SVC-EVAULT-ALLOW rule 8 description AMS03
set security firewall name SVC-EVAULT-ALLOW rule 8 destination address 10.3.134.0/24
set security firewall name SVC-EVAULT-ALLOW rule 8 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 8 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 8 state enable
set security firewall name SVC-EVAULT-ALLOW rule 9 action accept
set security firewall name SVC-EVAULT-ALLOW rule 9 description FRA02
set security firewall name SVC-EVAULT-ALLOW rule 9 destination address 10.3.86.0/24
set security firewall name SVC-EVAULT-ALLOW rule 9 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 9 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 9 state enable
set security firewall name SVC-EVAULT-ALLOW rule 10 action accept
set security firewall name SVC-EVAULT-ALLOW rule 10 description FRA02AZ
set security firewall name SVC-EVAULT-ALLOW rule 10 destination address 10.201.150.0/24
set security firewall name SVC-EVAULT-ALLOW rule 10 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 10 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 10 state enable
set security firewall name SVC-EVAULT-ALLOW rule 11 action accept
set security firewall name SVC-EVAULT-ALLOW rule 11 description FRA04
set security firewall name SVC-EVAULT-ALLOW rule 11 destination address 10.201.118.0/24
set security firewall name SVC-EVAULT-ALLOW rule 11 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 11 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 11 state enable
set security firewall name SVC-EVAULT-ALLOW rule 12 action accept
set security firewall name SVC-EVAULT-ALLOW rule 12 description FRA05
set security firewall name SVC-EVAULT-ALLOW rule 12 destination address 10.201.134.0/24
set security firewall name SVC-EVAULT-ALLOW rule 12 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 12 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 12 state enable
set security firewall name SVC-EVAULT-ALLOW rule 13 action accept
set security firewall name SVC-EVAULT-ALLOW rule 13 description DAL05
set security firewall name SVC-EVAULT-ALLOW rule 13 destination address 10.1.146.0/24
set security firewall name SVC-EVAULT-ALLOW rule 13 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 13 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 13 state enable
set security firewall name SVC-EVAULT-ALLOW rule 14 action accept
set security firewall name SVC-EVAULT-ALLOW rule 14 description DAL06
set security firewall name SVC-EVAULT-ALLOW rule 14 destination address 10.2.134.0/24
set security firewall name SVC-EVAULT-ALLOW rule 14 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 14 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 14 state enable
set security firewall name SVC-EVAULT-ALLOW rule 15 action accept
set security firewall name SVC-EVAULT-ALLOW rule 15 description DAL08
set security firewall name SVC-EVAULT-ALLOW rule 15 destination address 100.100.6.0/24
set security firewall name SVC-EVAULT-ALLOW rule 15 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 15 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 15 state enable
set security firewall name SVC-EVAULT-ALLOW rule 16 action accept
set security firewall name SVC-EVAULT-ALLOW rule 16 description DAL09
set security firewall name SVC-EVAULT-ALLOW rule 16 destination address 10.2.118.0/24
set security firewall name SVC-EVAULT-ALLOW rule 16 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 16 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 16 state enable
set security firewall name SVC-EVAULT-ALLOW rule 17 action accept
set security firewall name SVC-EVAULT-ALLOW rule 17 description DAL09
set security firewall name SVC-EVAULT-ALLOW rule 17 destination address 10.2.126.0/24
set security firewall name SVC-EVAULT-ALLOW rule 17 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 17 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 17 state enable
set security firewall name SVC-EVAULT-ALLOW rule 18 action accept
set security firewall name SVC-EVAULT-ALLOW rule 18 description DAL10
set security firewall name SVC-EVAULT-ALLOW rule 18 destination address 10.200.86.0/24
set security firewall name SVC-EVAULT-ALLOW rule 18 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 18 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 18 state enable
set security firewall name SVC-EVAULT-ALLOW rule 19 action accept
set security firewall name SVC-EVAULT-ALLOW rule 19 description DAL12
set security firewall name SVC-EVAULT-ALLOW rule 19 destination address 10.200.118.0/24
set security firewall name SVC-EVAULT-ALLOW rule 19 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 19 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 19 state enable
set security firewall name SVC-EVAULT-ALLOW rule 20 action accept
set security firewall name SVC-EVAULT-ALLOW rule 20 description DAL13
set security firewall name SVC-EVAULT-ALLOW rule 20 destination address 10.200.134.0/24
set security firewall name SVC-EVAULT-ALLOW rule 20 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 20 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 20 state enable
set security firewall name SVC-EVAULT-ALLOW rule 21 action accept
set security firewall name SVC-EVAULT-ALLOW rule 21 description WDC01
set security firewall name SVC-EVAULT-ALLOW rule 21 destination address 10.1.114.0/24
set security firewall name SVC-EVAULT-ALLOW rule 21 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 21 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 21 state enable
set security firewall name SVC-EVAULT-ALLOW rule 22 action accept
set security firewall name SVC-EVAULT-ALLOW rule 22 description WDC03
set security firewall name SVC-EVAULT-ALLOW rule 22 destination address 100.100.38.0/24
set security firewall name SVC-EVAULT-ALLOW rule 22 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 22 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 22 state enable
set security firewall name SVC-EVAULT-ALLOW rule 23 action accept
set security firewall name SVC-EVAULT-ALLOW rule 23 description WDC04
set security firewall name SVC-EVAULT-ALLOW rule 23 destination address 10.3.166.0/24
set security firewall name SVC-EVAULT-ALLOW rule 23 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 23 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 23 state enable
set security firewall name SVC-EVAULT-ALLOW rule 24 action accept
set security firewall name SVC-EVAULT-ALLOW rule 24 description WDC04
set security firewall name SVC-EVAULT-ALLOW rule 24 destination address 10.201.6.0/24
set security firewall name SVC-EVAULT-ALLOW rule 24 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 24 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 24 state enable
set security firewall name SVC-EVAULT-ALLOW rule 25 action accept
set security firewall name SVC-EVAULT-ALLOW rule 25 description WDC06
set security firewall name SVC-EVAULT-ALLOW rule 25 destination address 10.200.166.0/24
set security firewall name SVC-EVAULT-ALLOW rule 25 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 25 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 25 state enable
set security firewall name SVC-EVAULT-ALLOW rule 26 action accept
set security firewall name SVC-EVAULT-ALLOW rule 26 description WDC07
set security firewall name SVC-EVAULT-ALLOW rule 26 destination address 10.200.182.0/24
set security firewall name SVC-EVAULT-ALLOW rule 26 destination port EVAULT-ALLOW-TCP
set security firewall name SVC-EVAULT-ALLOW rule 26 protocol tcp
set security firewall name SVC-EVAULT-ALLOW rule 26 state enable
</pre>
#### File & Block
<pre>set resources group port-group FILEBLK-ALLOW-MIXED description 'File and Block Services'
set resources group port-group FILEBLK-ALLOW-MIXED port 111
set resources group port-group FILEBLK-ALLOW-MIXED port 635
set resources group port-group FILEBLK-ALLOW-MIXED port 4045-4048
set resources group port-group FILEBLK-ALLOW-MIXED port 65200

set security firewall name SVC-FILEBLK-ALLOW default-action drop
set security firewall name SVC-FILEBLK-ALLOW rule 1 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 1 description LON02
set security firewall name SVC-FILEBLK-ALLOW rule 1 destination address 10.1.222.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 1 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 1 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 2 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 2 description LON02AZ
set security firewall name SVC-FILEBLK-ALLOW rule 2 destination address 10.201.110.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 2 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 2 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 3 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 3 description LON04
set security firewall name SVC-FILEBLK-ALLOW rule 3 destination address 10.201.46.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 3 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 3 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 4 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 4 description LON05
set security firewall name SVC-FILEBLK-ALLOW rule 4 destination address 10.201.62.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 4 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 4 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 5 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 5 description LON06
set security firewall name SVC-FILEBLK-ALLOW rule 5 destination address 10.201.78.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 5 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 5 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 6 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 6 description AMS01
set security firewall name SVC-FILEBLK-ALLOW rule 6 destination address 10.2.78.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 6 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 6 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 7 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 7 description AMS01
set security firewall name SVC-FILEBLK-ALLOW rule 7 destination address 10.200.62.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 7 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 7 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 8 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 8 description AMS03
set security firewall name SVC-FILEBLK-ALLOW rule 8 destination address 10.3.142.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 8 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 8 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 9 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 9 description FRA02
set security firewall name SVC-FILEBLK-ALLOW rule 9 destination address 10.3.94.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 9 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 9 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 10 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 10 description FRA02AZ
set security firewall name SVC-FILEBLK-ALLOW rule 10 destination address 10.201.158.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 10 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 10 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 11 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 11 description FRA04
set security firewall name SVC-FILEBLK-ALLOW rule 11 destination address 10.201.110.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 11 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 11 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 12 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 12 description FRA05
set security firewall name SVC-FILEBLK-ALLOW rule 12 destination address 10.201.142.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 12 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 12 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 13 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 13 description DAL05
set security firewall name SVC-FILEBLK-ALLOW rule 13 destination address 10.1.154.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 13 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 13 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 14 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 14 description DAL05
set security firewall name SVC-FILEBLK-ALLOW rule 14 destination address 10.1.159.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 14 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 14 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 15 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 15 description DAL06
set security firewall name SVC-FILEBLK-ALLOW rule 15 destination address 10.2.142.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 15 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 15 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 16 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 16 description DAL08
set security firewall name SVC-FILEBLK-ALLOW rule 16 destination address 100.100.14.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 16 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 16 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 17 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 17 description DAL10
set security firewall name SVC-FILEBLK-ALLOW rule 17 destination address 10.200.94.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 17 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 17 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 18 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 18 description DAL12
set security firewall name SVC-FILEBLK-ALLOW rule 18 destination address 10.200.126.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 18 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 18 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 19 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 19 description DAL13
set security firewall name SVC-FILEBLK-ALLOW rule 19 destination address 10.200.142.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 19 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 19 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 20 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 20 description WDC01
set security firewall name SVC-FILEBLK-ALLOW rule 20 destination address 10.1.122.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 20 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 20 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 21 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 21 description WDC01
set security firewall name SVC-FILEBLK-ALLOW rule 21 destination address 10.1.127.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 21 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 21 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 22 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 22 description WDC01
set security firewall name SVC-FILEBLK-ALLOW rule 22 destination address 10.1.104.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 22 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 22 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 23 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 23 description WDC03
set security firewall name SVC-FILEBLK-ALLOW rule 23 destination address 100.100.46.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 23 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 23 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 24 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 24 description WDC04
set security firewall name SVC-FILEBLK-ALLOW rule 24 destination address 10.201.14.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 24 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 24 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 25 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 25 description WDC04
set security firewall name SVC-FILEBLK-ALLOW rule 25 destination address 10.3.174.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 25 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 25 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 26 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 26 description WDC06
set security firewall name SVC-FILEBLK-ALLOW rule 26 destination address 10.200.174.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 26 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 26 state enable
set security firewall name SVC-FILEBLK-ALLOW rule 27 action accept
set security firewall name SVC-FILEBLK-ALLOW rule 27 description WDC07
set security firewall name SVC-FILEBLK-ALLOW rule 27 destination address 10.200.90.0/24
set security firewall name SVC-FILEBLK-ALLOW rule 27 protocol-group mixed-proto
set security firewall name SVC-FILEBLK-ALLOW rule 27 state enable
</pre>
#### Advance Monitoring (NimSoft) rule
<pre>
set security firewall name SVC-ADVMON-ALLOW default-action drop
set security firewall name SVC-ADVMON-ALLOW rule 1 action accept
set security firewall name SVC-ADVMON-ALLOW rule 1 description LON02
set security firewall name SVC-ADVMON-ALLOW rule 1 destination address 10.1.211.0/24
set security firewall name SVC-ADVMON-ALLOW rule 1 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 1 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 1 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 1 state enable
set security firewall name SVC-ADVMON-ALLOW rule 2 action accept
set security firewall name SVC-ADVMON-ALLOW rule 2 description LON02AZ
set security firewall name SVC-ADVMON-ALLOW rule 2 destination address 10.201.99.0/24
set security firewall name SVC-ADVMON-ALLOW rule 2 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 2 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 2 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 2 state enable
set security firewall name SVC-ADVMON-ALLOW rule 3 action accept
set security firewall name SVC-ADVMON-ALLOW rule 3 description LON04
set security firewall name SVC-ADVMON-ALLOW rule 3 destination address 10.201.35.0/24
set security firewall name SVC-ADVMON-ALLOW rule 3 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 3 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 3 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 3 state enable
set security firewall name SVC-ADVMON-ALLOW rule 4 action accept
set security firewall name SVC-ADVMON-ALLOW rule 4 description LON05
set security firewall name SVC-ADVMON-ALLOW rule 4 destination address 10.201.51.0/24
set security firewall name SVC-ADVMON-ALLOW rule 4 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 4 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 4 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 4 state enable
set security firewall name SVC-ADVMON-ALLOW rule 5 action accept
set security firewall name SVC-ADVMON-ALLOW rule 5 description LON06
set security firewall name SVC-ADVMON-ALLOW rule 5 destination address 10.201.67.0/24
set security firewall name SVC-ADVMON-ALLOW rule 5 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 5 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 5 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 5 state enable
set security firewall name SVC-ADVMON-ALLOW rule 6 action accept
set security firewall name SVC-ADVMON-ALLOW rule 6 description AMS01
set security firewall name SVC-ADVMON-ALLOW rule 6 destination address 10.2.67.0/24
set security firewall name SVC-ADVMON-ALLOW rule 6 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 6 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 6 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 6 state enable
set security firewall name SVC-ADVMON-ALLOW rule 7 action accept
set security firewall name SVC-ADVMON-ALLOW rule 7 description AMS03
set security firewall name SVC-ADVMON-ALLOW rule 7 destination address 10.3.131.0/24
set security firewall name SVC-ADVMON-ALLOW rule 7 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 7 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 7 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 7 state enable
set security firewall name SVC-ADVMON-ALLOW rule 8 action accept
set security firewall name SVC-ADVMON-ALLOW rule 8 description FRA02
set security firewall name SVC-ADVMON-ALLOW rule 8 destination address 10.3.83.0/24
set security firewall name SVC-ADVMON-ALLOW rule 8 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 8 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 8 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 8 state enable
set security firewall name SVC-ADVMON-ALLOW rule 9 action accept
set security firewall name SVC-ADVMON-ALLOW rule 9 description FRA02AZ
set security firewall name SVC-ADVMON-ALLOW rule 9 destination address 10.201.147.0/24
set security firewall name SVC-ADVMON-ALLOW rule 9 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 9 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 9 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 9 state enable
set security firewall name SVC-ADVMON-ALLOW rule 10 action accept
set security firewall name SVC-ADVMON-ALLOW rule 10 description FRA04
set security firewall name SVC-ADVMON-ALLOW rule 10 destination address 10.201.115.0/24
set security firewall name SVC-ADVMON-ALLOW rule 10 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 10 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 10 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 10 state enable
set security firewall name SVC-ADVMON-ALLOW rule 11 action accept
set security firewall name SVC-ADVMON-ALLOW rule 11 description FRA05
set security firewall name SVC-ADVMON-ALLOW rule 11 destination address 10.201.131.0/24
set security firewall name SVC-ADVMON-ALLOW rule 11 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 11 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 11 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 11 state enable
set security firewall name SVC-ADVMON-ALLOW rule 12 action accept
set security firewall name SVC-ADVMON-ALLOW rule 12 description DAL05
set security firewall name SVC-ADVMON-ALLOW rule 12 destination address 10.1.143/139.0/24
set security firewall name SVC-ADVMON-ALLOW rule 12 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 12 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 12 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 12 state enable
set security firewall name SVC-ADVMON-ALLOW rule 13 action accept
set security firewall name SVC-ADVMON-ALLOW rule 13 description DAL06
set security firewall name SVC-ADVMON-ALLOW rule 13 destination address 10.2.131.0/24
set security firewall name SVC-ADVMON-ALLOW rule 13 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 13 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 13 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 13 state enable
set security firewall name SVC-ADVMON-ALLOW rule 14 action accept
set security firewall name SVC-ADVMON-ALLOW rule 14 description DAL08
set security firewall name SVC-ADVMON-ALLOW rule 14 destination address 100.100.3.0/24
set security firewall name SVC-ADVMON-ALLOW rule 14 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 14 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 14 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 14 state enable
set security firewall name SVC-ADVMON-ALLOW rule 15 action accept
set security firewall name SVC-ADVMON-ALLOW rule 15 description DAL09
set security firewall name SVC-ADVMON-ALLOW rule 15 destination address 10.2.115.0/24
set security firewall name SVC-ADVMON-ALLOW rule 15 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 15 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 15 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 15 state enable
set security firewall name SVC-ADVMON-ALLOW rule 16 action accept
set security firewall name SVC-ADVMON-ALLOW rule 16 description DAL10
set security firewall name SVC-ADVMON-ALLOW rule 16 destination address 10.200.83.0/24
set security firewall name SVC-ADVMON-ALLOW rule 16 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 16 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 16 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 16 state enable
set security firewall name SVC-ADVMON-ALLOW rule 17 action accept
set security firewall name SVC-ADVMON-ALLOW rule 17 description DAL12
set security firewall name SVC-ADVMON-ALLOW rule 17 destination address 10.200.115.0/24
set security firewall name SVC-ADVMON-ALLOW rule 17 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 17 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 17 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 17 state enable
set security firewall name SVC-ADVMON-ALLOW rule 18 action accept
set security firewall name SVC-ADVMON-ALLOW rule 18 description DAL13
set security firewall name SVC-ADVMON-ALLOW rule 18 destination address 10.200.131.0/24
set security firewall name SVC-ADVMON-ALLOW rule 18 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 18 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 18 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 18 state enable
set security firewall name SVC-ADVMON-ALLOW rule 19 action accept
set security firewall name SVC-ADVMON-ALLOW rule 19 description WDC01
set security firewall name SVC-ADVMON-ALLOW rule 19 destination address 10.1.111.0/24
set security firewall name SVC-ADVMON-ALLOW rule 19 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 19 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 19 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 19 state enable
set security firewall name SVC-ADVMON-ALLOW rule 20 action accept
set security firewall name SVC-ADVMON-ALLOW rule 20 description WDC03
set security firewall name SVC-ADVMON-ALLOW rule 20 destination address 100.100.35.0/24
set security firewall name SVC-ADVMON-ALLOW rule 20 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 20 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 20 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 20 state enable
set security firewall name SVC-ADVMON-ALLOW rule 21 action accept
set security firewall name SVC-ADVMON-ALLOW rule 21 description WDC04
set security firewall name SVC-ADVMON-ALLOW rule 21 destination address 10.3.163.0/24
set security firewall name SVC-ADVMON-ALLOW rule 21 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 21 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 21 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 21 state enable
set security firewall name SVC-ADVMON-ALLOW rule 22 action accept
set security firewall name SVC-ADVMON-ALLOW rule 22 description WDC04
set security firewall name SVC-ADVMON-ALLOW rule 22 destination address 10.201.3.0/24
set security firewall name SVC-ADVMON-ALLOW rule 22 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 22 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 22 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 22 state enable
set security firewall name SVC-ADVMON-ALLOW rule 23 action accept
set security firewall name SVC-ADVMON-ALLOW rule 23 description WDC06
set security firewall name SVC-ADVMON-ALLOW rule 23 destination address 10.200.163.0/24
set security firewall name SVC-ADVMON-ALLOW rule 23 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 23 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 23 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 23 state enable
set security firewall name SVC-ADVMON-ALLOW rule 24 action accept
set security firewall name SVC-ADVMON-ALLOW rule 24 description WDC07
set security firewall name SVC-ADVMON-ALLOW rule 24 destination address 10.200.179.0/24
set security firewall name SVC-ADVMON-ALLOW rule 24 destination port 48000
set security firewall name SVC-ADVMON-ALLOW rule 24 protocol-group mixed-proto
set security firewall name SVC-ADVMON-ALLOW rule 24 source port 48000-48200
set security firewall name SVC-ADVMON-ALLOW rule 24 state enable
</pre>
