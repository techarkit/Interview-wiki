## What is FLogi?
FLOGI process, a device sends its first frame to the SAN switch. The SAN switch assigns an FCID to the device and the end device confirms to the switch that it received an FCID. The switch uses this FCID to identify the end device connected to it in the SAN network. FLOGI Process happens when a new device connects to SAN switch or fabric for the first time. The new devices send it the first frame to switch that contains information like WWPN and buffer to buffer credits (B2B credits).

## What is PLogi?
PLOGI Process has two steps, port initialization and registration in Name Server. During port initialization a host and switch exchange information like port type and port speed. SAN switch uses these information and negotiates with host. During negotiation SAN switch will come to know whether the end device is a server or a storage by referencing the port type.

## What does mean by Disk C3 Errors on Port error show?
