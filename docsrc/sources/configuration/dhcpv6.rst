.. code-block:: json

    { "dhcpv6": {} }


.. list-table::
   :widths: 25 50 25
   :header-rows: 1

   * - Attribute
     - Description
     - Default
   * - `enable`
     - This option allows to enable or disable DHCPv6
     - true
   * - `ia-na`
     - This option allows to enable or disable DHCPv6 IA_NA
     - true
   * - `ia-pd`
     - This option allows to enable or disable DHCPv6 IA_PD
     - true
   * - `rapid-commit`
     - DHCPv6 rapid commit (2-way handshake)
     - true
   * - `timeout`
     - DHCPv6 timeout in seconds
     - 5
   * - `retry`
     - DHCPv6 retry
     - 10
   * - `access-line`
     - Add access-line attributes like Agent-Remote/Circuit-Id
     - true