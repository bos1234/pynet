# 1. Parse the CDP data (see link above) to obtain the following information: hostname, ip, model, vendor, and device_type

# (device_type will be either 'router', 'switch', or 'unknown').
# From this data create a dictionary of all the network devices.
# The network_devices dictionary should have the following format:
#
# network_devices = {
#      'SW1': { 'ip': '10.1.1.22', 'model': 'WS-C2950-24', 'vendor': 'cisco', 'device_type': 'switch' },
#      'R1': { 'ip': '10.1.1.1', 'model': '881', 'vendor': 'Cisco', 'device_type': 'router' },
#       ...
#      'R5': { 'ip': '10.1.1.1', 'model': '881', 'vendor': 'Cisco', 'device_type': 'router' },
#  }
#
# Note, this data structure is a dictionary that contains additional dictionaries.  The key to the outer dictionary is a hostname and the data corresponding to this key is another dictionary.  For example, for 'R1':
#
# >>> network_devices['R1']
# {'ip': '10.1.1.1', 'model': '881', 'vendor': 'Cisco', 'device_type': 'router'}
#
# You can access a given attribute in the inner dictionary as follows:
# >>> a_dict['R1']['ip']
# '10.1.1.1'
#
#
# If this is confusing, you might want to experiment with it in the Python shell:
#
# ##### Python Shell - experimenting with dictionary of dictionaries #####
#
# # Initialize network_devices to be a blank dictionary
# >>> network_devices = {}
#
# # Assign the key 'R1' to network_devices using a value of a blank dictionary (in other words, I am adding a key:value pair to network_devices where the key is 'R1' and the value is {} )
# >>> network_devices['R1'] = {}
#
# # Look at network_devices at this point
# >>> network_devices
# {'R1': {}}
#
# # Add the 'ip' and 'vendor' fields to the inner dictionary
# >>> network_devices['R1']['ip'] = '10.1.1.1'
# >>> network_devices['R1']['vendor'] = 'Cisco'
# >>> network_devices
# {'R1': {'ip': '10.1.1.1', 'vendor': 'Cisco'}}
#
# ##### Python Shell - experimenting end #####
#
#
# For the output to this exercise, print network_devices to standard output.
# Your output should look similar to the following (six network devices with their associated attributes).
# {'R1': {'device_type': 'Router',
#         'ip': '10.1.1.1',
#         'model': '881',
#         'vendor': 'Cisco'},
#  'R2': {'device_type': 'Router',
#         'ip': '10.1.1.2',
#         'model': '881',
#         'vendor': 'Cisco'},
#  'R3': {'device_type': 'Router',
#         'ip': '10.1.1.3',
#         'model': '881',
#         'vendor': 'Cisco'},
#  'R4': {'device_type': 'Router',
#         'ip': '10.1.1.4',
#         'model': '881',
#         'vendor': 'Cisco'},
#  'R5': {'device_type': 'Router',
#         'ip': '10.1.1.5',
#         'model': '881',
#         'vendor': 'Cisco'},
#  'SW1': {'device_type': 'Switch',
#          'ip': '10.1.1.22',
#          'model': 'WS-C2950-24',
#          'vendor': 'cisco'}}

import re
from pprint import pprint

sw1_show_cdp_neighbors = '''
SW1>show cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                                 S - Switch, H - Host, I - IGMP, r - Repeater, P - Phone
Device ID            Local Intrfce        Holdtme        Capability        Platform    Port ID
R1                    Fas 0/11              153            R S I           881          Fas 1
R2                    Fas 0/12              123            R S I           881          Fas 1
R3                    Fas 0/13              129            R S I           881          Fas 1
R4                    Fas 0/14              173            R S I           881          Fas 1
R5                    Fas 0/15              144            R S I           881          Fas 1
'''

sw1_show_cdp_neighbors_detail = '''
SW1> show cdp neighbors detail
--------------------------
Device ID: R1
Entry address(es):
   IP address: 10.1.1.1
Platform: Cisco 881, Capabilities: Router Switch IGMP
Interface: FastEthernet0/11, Port ID (outgoing port): FastEthernet1
Holdtime: 153 sec
Version :
Cisco IOS Software, C880 Software (C880DATA-UNIVERSALK9-M), Version 15.0(1)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Fri 29-Oct-10 00:02 by prod_rel_team
advertisement version: 2
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
Management address(es):
--------------------------
Device ID: R2
Entry address(es):
   IP address: 10.1.1.2
Platform: Cisco 881, Capabilities: Router Switch IGMP
Interface: FastEthernet0/12, Port ID (outgoing port): FastEthernet1
Holdtime: 123 sec
Version :
Cisco IOS Software, C880 Software (C880DATA-UNIVERSALK9-M), Version 15.0(1)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Fri 29-Oct-10 00:02 by prod_rel_team
advertisement version: 2
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
Management address(es):
--------------------------
Device ID: R3
Entry address(es):
   IP address: 10.1.1.3
Platform: Cisco 881, Capabilities: Router Switch IGMP
Interface: FastEthernet0/13, Port ID (outgoing port): FastEthernet1
Holdtime: 129 sec
Version :
Cisco IOS Software, C880 Software (C880DATA-UNIVERSALK9-M), Version 15.0(1)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Fri 29-Oct-10 00:02 by prod_rel_team
advertisement version: 2
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
Management address(es):
--------------------------
Device ID: R4
Entry address(es):
   IP address: 10.1.1.4
Platform: Cisco 881, Capabilities: Router Switch IGMP
Interface: FastEthernet0/14, Port ID (outgoing port): FastEthernet1
Holdtime: 173 sec
Version :
Cisco IOS Software, C880 Software (C880DATA-UNIVERSALK9-M), Version 15.0(1)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Fri 29-Oct-10 00:02 by prod_rel_team
advertisement version: 2
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
Management address(es):
--------------------------
Device ID: R5
Entry address(es):
   IP address: 10.1.1.5
Platform: Cisco 881, Capabilities: Router Switch IGMP
Interface: FastEthernet0/15, Port ID (outgoing port): FastEthernet1
Holdtime: 144 sec
Version :
Cisco IOS Software, C880 Software (C880DATA-UNIVERSALK9-M), Version 15.0(1)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Fri 29-Oct-10 00:02 by prod_rel_team
advertisement version: 2
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
Management address(es):
'''

r1_show_cdp_neighbors = '''
R1>show cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater
Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
SW1              Fas 1              150          S I      WS-C2950- Fas 0/11
'''

r1_show_cdp_neighbors_detail = '''
R1>show cdp neighbors detail
-------------------------
Device ID: SW1
Entry address(es):
  IP address: 10.1.1.22
Platform: cisco WS-C2950-24,  Capabilities: Switch IGMP
Interface: FastEthernet1,  Port ID (outgoing port): FastEthernet0/11
Holdtime : 145 sec
Version :
Cisco Internetwork Operating System Software
IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(22)EA8a, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2006 by cisco Systems, Inc.
Compiled Fri 28-Jul-06 15:16 by weiliu
advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF0000000000000019E845CE80FF0000
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
'''

r2_show_cdp_neighbors = '''
R2>show cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater
Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
SW1              Fas 1              150          S I      WS-C2950- Fas 0/12
'''

r2_show_cdp_neighbors_detail = '''
R2>show cdp neighbors detail
-------------------------
Device ID: SW1
Entry address(es):
  IP address: 10.1.1.22
Platform: cisco WS-C2950-24,  Capabilities: Switch IGMP
Interface: FastEthernet1,  Port ID (outgoing port): FastEthernet0/12
Holdtime : 145 sec
Version :
Cisco Internetwork Operating System Software
IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(22)EA8a, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2006 by cisco Systems, Inc.
Compiled Fri 28-Jul-06 15:16 by weiliu
advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF0000000000000019E845CE80FF0000
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
'''

r3_show_cdp_neighbors = '''
R3>show cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater
Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
SW1              Fas 1              150          S I      WS-C2950- Fas 0/13
'''

r3_show_cdp_neighbors_detail = '''
R3>show cdp neighbors detail
-------------------------
Device ID: SW1
Entry address(es):
  IP address: 10.1.1.22
Platform: cisco WS-C2950-24,  Capabilities: Switch IGMP
Interface: FastEthernet1,  Port ID (outgoing port): FastEthernet0/13
Holdtime : 145 sec
Version :
Cisco Internetwork Operating System Software
IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(22)EA8a, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2006 by cisco Systems, Inc.
Compiled Fri 28-Jul-06 15:16 by weiliu
advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF0000000000000019E845CE80FF0000
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
'''

r4_show_cdp_neighbors = '''
R4>show cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater
Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
SW1              Fas 1              150          S I      WS-C2950- Fas 0/14
'''

r4_show_cdp_neighbors_detail = '''
R4>show cdp neighbors detail
-------------------------
Device ID: SW1
Entry address(es):
  IP address: 10.1.1.22
Platform: cisco WS-C2950-24,  Capabilities: Switch IGMP
Interface: FastEthernet1,  Port ID (outgoing port): FastEthernet0/14
Holdtime : 145 sec
Version :
Cisco Internetwork Operating System Software
IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(22)EA8a, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2006 by cisco Systems, Inc.
Compiled Fri 28-Jul-06 15:16 by weiliu
advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF0000000000000019E845CE80FF0000
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
'''

r5_show_cdp_neighbors = '''
R5>show cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater
Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
SW1              Fas 1              150          S I      WS-C2950- Fas 0/15
'''

r5_show_cdp_neighbors_detail = '''
R5>show cdp neighbors detail
-------------------------
Device ID: SW1
Entry address(es):
  IP address: 10.1.1.22
Platform: cisco WS-C2950-24,  Capabilities: Switch IGMP
Interface: FastEthernet1,  Port ID (outgoing port): FastEthernet0/15
Holdtime : 145 sec
Version :
Cisco Internetwork Operating System Software
IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(22)EA8a, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2006 by cisco Systems, Inc.
Compiled Fri 28-Jul-06 15:16 by weiliu
advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF0000000000000019E845CE80FF0000
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
'''

network_devices = {}
list_of_show_cdp_neighbors = [sw1_show_cdp_neighbors_detail, r1_show_cdp_neighbors_detail,
                              r2_show_cdp_neighbors_detail, r3_show_cdp_neighbors_detail,
                              r4_show_cdp_neighbors_detail, r5_show_cdp_neighbors_detail]

# populate the dictionary with the hostnames
for element in list_of_show_cdp_neighbors:
    cdp_list = element.splitlines()

    for i, cdp in enumerate(cdp_list):
        match_hostname = re.search(r"Device ID:\s(.+)$", cdp)

        if (match_hostname):
            test = network_devices.get(match_hostname.group(1), 'False')
            if (test=='False'):
                network_devices[match_hostname.group(1)] = {}

# populate the dictionary with the other elements like ip address and device model
    for cdp in (cdp_list):
        match_hostname = re.search(r"Device ID:\s(.+)$", cdp)
        match_ip = re.search(r"\s+IP address:\s(.+)$", cdp)
        match_model = re.search(r"Platform: [A-Za-z]+\s(.+), (.+)$", cdp)
        match_vendor = re.search(r"Platform: (\w+)\s", cdp)
        match_device_type = re.search(r"Capabilities: (.+)", cdp)



        if (match_hostname):
            hostname = match_hostname.group(1)
        if (match_ip):
            network_devices[hostname]['ip'] = match_ip.group(1)
        if (match_model):
            network_devices[hostname]['model'] = match_model.group(1)
        if (match_vendor):
            network_devices[hostname]['vendor'] = match_vendor.group(1)
        if (match_device_type):
            if 'Router' in match_device_type.group(1):
                network_devices[hostname]['device_type'] = 'Router'
            elif 'Switch' in match_device_type.group(1):
                network_devices[hostname]['device_type'] = 'Switch'
            else:
                etwork_devices[hostname]['device_type'] = 'Uknown'

pprint(network_devices)
