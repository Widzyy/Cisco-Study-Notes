### 🔹 1. **VLAN (Virtual Local Area Network)**

* Membagi jaringan fisik menjadi beberapa jaringan logis.
* Cocok untuk memisahkan traffic user, server, atau VoIP.
* Perintah dasar:

  ```bash
  switch(config)# vlan 10
  switch(config-vlan)# name HR
  switch(config)# interface fa0/1
  switch(config-if)# switchport mode access
  switch(config-if)# switchport access vlan 10
  ```

---

### 🔹 2. **Trunking (802.1Q)**

* Menghubungkan beberapa switch dengan membawa banyak VLAN lewat satu link.
* Perintah dasar:

  ```bash
  switch(config)# interface fa0/24
  switch(config-if)# switchport mode trunk
  switch(config-if)# switchport trunk allowed vlan 10,20,30
  ```

---

### 🔹 3. **Spanning Tree Protocol (STP)**

* Mencegah **looping** jaringan jika ada link redundant.
* Bisa dicoba:

  * **PVST+** (default)
  * **Rapid-PVST+** (lebih cepat konvergensinya)
* Perintah dasar:

  ```bash
  switch(config)# spanning-tree mode rapid-pvst
  switch(config)# spanning-tree vlan 10 priority 4096
  ```

---

### 🔹 4. **Port Security**

* Membatasi perangkat yang boleh terhubung ke port tertentu.
* Bagus untuk mencegah **MAC flooding** atau perangkat tidak sah.
* Contoh:

  ```bash
  switch(config)# interface fa0/2
  switch(config-if)# switchport mode access
  switch(config-if)# switchport port-security
  switch(config-if)# switchport port-security maximum 2
  switch(config-if)# switchport port-security violation restrict
  switch(config-if)# switchport port-security mac-address sticky
  ```

---

### 🔹 5. **Inter-VLAN Routing (SVI – Switch Virtual Interface)**

* Kalau switch **Layer 3**, bisa langsung melakukan routing antar VLAN.
* Contoh:

  ```bash
  switch(config)# interface vlan 10
  switch(config-if)# ip address 192.168.10.1 255.255.255.0
  switch(config-if)# no shutdown
  switch(config)# ip routing
  ```

---

### 🔹 6. **EtherChannel (Link Aggregation)**

* Menggabungkan beberapa port jadi satu channel untuk meningkatkan bandwidth & redundancy.
* Contoh:

  ```bash
  switch(config)# interface range fa0/1 - 2
  switch(config-if-range)# channel-group 1 mode active
  switch(config)# interface port-channel 1
  switch(config-if)# switchport mode trunk
  ```

---

### 🔹 7. **QoS (Quality of Service)**

* Mengatur prioritas traffic (misalnya untuk VoIP).
* Cocok buat lab real-time traffic.

---

### 🔹 8. **DHCP Snooping & Dynamic ARP Inspection (DAI)**

* **DHCP Snooping**: mencegah DHCP rogue server.
* **DAI**: mencegah ARP spoofing.

---
