Day 01 — Lab Notes


# Day 01 — Mac-to-Windows 11 VM Network Connectivity Testing

## 1. Objective

The objective of this lab was to verify IP connectivity between my MacBook Pro, which serves as the primary workstation, and a Windows 11 virtual machine running in VMware Fusion.

The test used ICMP Echo Requests and Echo Replies through the `ping` utility.

## 2. Lab Environment

| Component | Details |
|---|---|
| Primary workstation | MacBook Pro (2017) |
| Host operating system | macOS Ventura |
| Virtualization platform | VMware Fusion |
| Target machine | Windows 11 virtual machine |
| Host IP address | `192.168.1.212` |
| VM IP address | `172.16.204.128` |
| VM network mode | NAT |
| Test utility | `ping` |

The Mac host and Windows virtual machine use different IP subnets. The Windows VM is connected through VMware Fusion's NAT network.

## 3. Methodology

The following procedure was used to test connectivity:

1. Identified the IP address assigned to the Windows 11 virtual machine.
2. Initiated a ping test from the macOS terminal to the VM's IP address.
3. Examined the responses returned by the target machine.
4. Investigated the Windows Firewall configuration when ICMP connectivity was initially unsuccessful.
5. Enabled the appropriate inbound ICMP Echo Request firewall rule and repeated the test.

## 4. Command Executed

The following command was executed on the MacBook Pro:

ping 172.16.204.128


The command sends ICMP Echo Requests to the Windows virtual machine and waits for replies.

## 5. Results and Observations

**Result: Successful ICMP connectivity test.**

The repeated test returned successful ICMP Echo Replies from the Windows 11 virtual machine.

Observed results included:

- The target VM responded to ICMP Echo Requests.
- The reported packet loss was 0% for the successful test.
- The observed response times were approximately 0.6 milliseconds.
- Enabling the appropriate inbound ICMP firewall rule on Windows resolved the initial connectivity issue.

These observations confirm that the Mac could reach the Windows VM using ICMP at the time of testing.

## 6. Technical Analysis

The successful ping test demonstrates that ICMP traffic could travel from the Mac host to the Windows 11 virtual machine and that the VM could return ICMP Echo Replies.

The initial failure highlighted the role of host-based firewall rules in network troubleshooting. A machine may be reachable through its network configuration while a firewall blocks specific types of traffic.

In this case, allowing inbound ICMP Echo Requests enabled the VM to respond to the connectivity test.

Because the Mac host and virtual machine use different subnets, the test also demonstrates connectivity across the host's physical network and the VMware NAT environment.

However, a successful ping test does not establish that every network service is accessible or that the system is secure.

## 7. Security Implications

ICMP can be useful for network diagnostics, connectivity monitoring, and troubleshooting.

However, allowing inbound ICMP traffic should be evaluated according to the environment's security requirements.

Security considerations include:

- Restricting firewall rules to the required traffic and scope where practical.
- Avoiding unnecessary exposure of systems to untrusted networks.
- Distinguishing basic network reachability from application-level availability.
- Reviewing firewall configuration when troubleshooting connectivity failures.

For this lab, the ICMP rule was enabled specifically to support testing within the personal virtualized environment.

## 8. Challenges and Troubleshooting

**Challenge:** The initial ping test did not receive replies from the Windows 11 virtual machine.

**Investigation:** The Windows Firewall configuration was examined.

**Resolution:** The appropriate inbound ICMP Echo Request rule was enabled, and the connectivity test was repeated.

**Outcome:** The VM returned successful ICMP Echo Replies.

This exercise reinforced the importance of testing network connectivity systematically rather than assuming that an unsuccessful ping automatically indicates a hardware or IP configuration failure.

## 9. Key Takeaways

- The `ping` utility is useful for testing basic IP connectivity.
- ICMP Echo Requests and Echo Replies help identify whether a target responds to network probes.
- Host-based firewall rules can prevent successful ping responses.
- VMware NAT environments introduce an additional networking layer to consider during troubleshooting.
- A successful ping does not prove that all ports and services are accessible.

## 10. Evidence

The supporting evidence for this lab is the successful ping output obtained from the macOS terminal.

**Evidence to attach:** `screenshots/day-01/mac-to-windows-ping.png`

The screenshot should show the command and successful replies. Any unrelated personal information should be cropped or redacted before publication.

## 11. Conclusion

This lab successfully verified ICMP connectivity between the MacBook Pro and the Windows 11 virtual machine after the relevant Windows Firewall rule was enabled.

The exercise provided practical experience with ICMP-based connectivity testing, firewall troubleshooting, and networking within a virtualized environment.

**Lab status:** Completed  
**Primary skill demonstrated:** Network connectivity troubleshooting  
**Next step:** Continue with the next networking exercise and document the observed results using the same reporting structure.
