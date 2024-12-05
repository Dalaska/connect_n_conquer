# Creating a Subnet at Home

**Goal**  
Set up a small "sub-network" in your home network so two Linux computers can talk to each other using their own special IP addresses.

**Requirements:**  
Two Linux computers on the same home network (through a home router).

## Steps

### On Machine A

1. **Find the Network Interface Name**  
   Use:
   ```bash
   ifconfig
   ```
   or
   ```bash
   ip link show
   ```
   Your network card might be called `eth0` or something like `enp0s3` or `wlp0s20f3`.

2. **Assign a New IP Address**  
   We'll choose 192.168.4.10 on the 192.168.4.0/24 network:
   ```bash
   sudo ip addr add 192.168.4.10/24 dev wlp0s20f3
   ```

3. **Verify that the New IP Address was Added**  
   ```bash
   ip addr show wlp0s20f3
   ```
   You should see something like this:
   ```
   inet 192.168.4.10/24 scope global ...
   ```
   It shows that 192.168.4.10/24 was assigned.

### On Machine B

1. **Test Connection to Machine A**  
   ```bash
   ping 192.168.4.10
   ```
   You'll get no response yet because Machine B isn't on that new subnet.

2. **Do the Same Steps on Machine B**  
   After adding the new IP address, run:
   ```bash
   ping 192.168.4.10
   ```
   You should get replies this time, something like this:
   ```
   PING 192.168.4.10 (192.168.4.10) 56(84) bytes of data.
   64 bytes from 192.168.4.10: icmp_seq=79 ttl=64 time=42.2 ms
   64 bytes from 192.168.4.10: icmp_seq=80 ttl=64 time=5.18 ms
   ```
