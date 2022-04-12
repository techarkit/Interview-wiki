### Difference between IPSpace and Broadcast domain
### What is NBlade
### What is DBlade
### What is Cluster Seesion Manager
### What is Volume Database (RDB)
### Port error show Disk C3 errors
### What is Epslon
### What is Quorum
### How Data Read Request process in Netapp
### Explain NetApp Architecture
### What is Load sharing mirrors
### Explain Snapmirror Types
### Client is reporting CIFS shares slowness how will you resolve
### NFS client is reporting latency how will you resolve
### SAN Switch Director
### What is Flogi process?
FLOGI process, a device sends its first frame to the SAN switch. The SAN switch assigns an FCID to the device and the end device confirms to the switch that it received an FCID. The switch uses this FCID to identify the end device connected to it in the SAN network. FLOGI Process happens when a new device connects to SAN switch or fabric for the first time. The new devices send it the first frame to switch that contains information like WWPN and buffer to buffer credits (B2B credits).

## What is PLogi process?
PLOGI Process has two steps, port initialization and registration in Name Server. During port initialization a host and switch exchange information like port type and port speed. SAN switch uses these information and negotiates with host. During negotiation SAN switch will come to know whether the end device is a server or a storage by referencing the port type.
