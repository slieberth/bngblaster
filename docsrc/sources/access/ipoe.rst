.. _ipoe:

IPoE
----

The BNG Blaster can emulate IP over Ethernet (IPoE)
subscribers with static and dynamic address assignment
supporting 1:1 and N:1 VLAN mode.

Static Addresses
~~~~~~~~~~~~~~~~

Static addresses mean that the IP address and gateway are assigned
statically as shown in the example below.

.. code-block:: json

    {
        "interfaces": {
            "access": [
            {
                "interface": "eth1",
                "type": "ipoe",
                "vlan-mode": "1:1",
                "outer-vlan-min": 128,
                "outer-vlan-max": 4000,
                "address": "200.0.0.1",
                "address-iter": "0.0.0.4",
                "gateway": "200.0.0.2",
                "gateway-iter": "0.0.0.4",
            }
        ]
        }
    }

DHCPv4/v6
~~~~~~~~~

The most common case for IPoE is using DHCPv4/v6 as shown below.

.. code-block:: json

    {
        "interfaces": {
            "access": [
            {
                "interface": "eth1",
                "type": "ipoe",
                "outer-vlan": 7,
                "vlan-mode": "N:1"
            }
        ]
        },
        "dhcp": {
            "enable": true,
        },
        "dhcpv6": {
            "enable": true
        },
        "access-line": {
            "agent-remote-id": "DEU.RTBRICK.{session-global}",
            "agent-circuit-id": "0.0.0.0/0.0.0.0 eth 0:{session-global}"
        }
    }

IPoE
^^^^^
.. include:: ../configuration/ipoe.rst

DHCP
^^^^
.. include:: ../configuration/dhcp.rst 

DHCPv6
^^^^^^
.. include:: ../configuration/dhcpv6.rst

IPoE Commands
~~~~~~~~~~~~~

The :ref:`command <api>` ``session-info session-id <id>`` provides
detailed information for IPoE sessions.

``$ sudo bngblaster-cli run.sock session-info session-id 1 | jq .``

.. code-block:: json

    {
        "status": "ok",
        "code": 200,
        "session-information": {
            "type": "ipoe",
            "session-id": 1,
            "session-state": "Established",
            "interface": "eth1",
            "outer-vlan": 8,
            "inner-vlan": 1,
            "mac": "02:00:00:00:00:01",
            "agent-circuit-id": "0.0.0.0/0.0.0.0 eth 0:1",
            "agent-remote-id": "DEU.RTBRICK.1",
            "ipv4-address": "1.1.1.3",
            "ipv4-netmask": "255.255.255.255",
            "ipv4-gateway": "1.1.1.1",
            "ipv4-dns1": "10.0.0.3",
            "ipv4-dns2": "10.0.0.4",
            "ipv6-prefix": "fc66:1337:2222::3/128",
            "ipv6-delegated-prefix": "fc66:1337:3333:2::/64",
            "dhcp-state": "Bound",
            "dhcp-server": "1.1.1.1",
            "dhcp-lease-time": 300,
            "dhcp-lease-expire": 299,
            "dhcp-lease-expire-t1": 149,
            "dhcp-lease-expire-t2": 261,
            "dhcp-tx": 2,
            "dhcp-rx": 2,
            "dhcp-tx-discover": 1,
            "dhcp-rx-offer": 1,
            "dhcp-tx-request": 1,
            "dhcp-rx-ack": 1,
            "dhcp-rx-nak": 0,
            "dhcp-tx-release": 0,
            "dhcpv6-state": "Bound",
            "dhcpv6-lease-time": 14400,
            "dhcpv6-lease-expire": 14399,
            "dhcpv6-lease-expire-t1": 899,
            "dhcpv6-lease-expire-t2": 1439,
            "dhcpv6-tx": 1,
            "dhcpv6-rx": 1,
            "dhcpv6-tx-solicit": 1,
            "dhcpv6-rx-advertise": 0,
            "dhcpv6-tx-request": 0,
            "dhcpv6-rx-reply": 1,
            "dhcpv6-tx-renew": 0,
            "dhcpv6-tx-release": 0,
            "dhcpv6-dns1": "fc66::3",
            "dhcpv6-dns2": "fc66::4",
            "tx-packets": 6,
            "rx-packets": 6,
            "rx-fragmented-packets": 0,
            "session-traffic": {
                "total-flows": 6,
                "verified-flows": 0,
                "downstream-ipv4-flow-id": 2,
                "downstream-ipv4-tx-packets": 13,
                "downstream-ipv4-rx-packets": 13,
                "downstream-ipv4-rx-first-seq": 1,
                "downstream-ipv4-loss": 0,
                "downstream-ipv4-wrong-session": 0,
                "upstream-ipv4-flow-id": 1,
                "upstream-ipv4-tx-packets": 13,
                "upstream-ipv4-rx-packets": 13,
                "upstream-ipv4-rx-first-seq": 1,
                "upstream-ipv4-loss": 0,
                "upstream-ipv4-wrong-session": 0,
                "downstream-ipv6-flow-id": 4,
                "downstream-ipv6-tx-packets": 13,
                "downstream-ipv6-rx-packets": 13,
                "downstream-ipv6-rx-first-seq": 1,
                "downstream-ipv6-loss": 0,
                "downstream-ipv6-wrong-session": 0,
                "upstream-ipv6-flow-id": 3,
                "upstream-ipv6-tx-packets": 13,
                "upstream-ipv6-rx-packets": 13,
                "upstream-ipv6-rx-first-seq": 1,
                "upstream-ipv6-loss": 0,
                "upstream-ipv6-wrong-session": 0,
                "downstream-ipv6pd-flow-id": 6,
                "downstream-ipv6pd-tx-packets": 13,
                "downstream-ipv6pd-rx-packets": 13,
                "downstream-ipv6pd-rx-first-seq": 1,
                "downstream-ipv6pd-loss": 0,
                "downstream-ipv6pd-wrong-session": 0,
                "upstream-ipv6pd-flow-id": 5,
                "upstream-ipv6pd-tx-packets": 13,
                "upstream-ipv6pd-rx-packets": 13,
                "upstream-ipv6pd-rx-first-seq": 1,
                "upstream-ipv6pd-loss": 0,
                "upstream-ipv6pd-wrong-session": 0
            }
        }
    }
