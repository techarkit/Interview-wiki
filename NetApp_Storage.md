# NetApp Interview Questions and Answers
_______________________________________________________

### What is a Node?
A single NetApp controller in a high-availability (HA) pair.

### What is a Cluster?
One or more nodes that are interconnected and managed as a single system.

### What is Cluster interconnect?
A dedicated high-speed, low-latency, private network used for communication and replication between nodes in the same cluster.

### What is Data network?
The network used by clients to access data.

### What is a Management network?
The network used for administration of the cluster, SVM, and nodes.

### What is a HA interconnect?
The dedicated interconnect between two nodes in one HA pair.

### What is HA pair?
Two nodes configured in a pair for HA.

### What is Physical port?
A physical port such as e0e or e0f or a logical port such as a virtual LAN (VLAN) or an interface group (ifgrp).

### What is Virtual port?
  −  Ifgrp. A collection of physical ports combined to create one logical port used for link aggregation.
  −  VLAN. A VLAN subdivides a physical network into distinct broadcast domains. As a result, traffic is completely isolated between VLANs unless a router (layer 3) is used to connect the networks. In ONTAP, VLANs subdivide a physical port into several separate virtual ports, allowing for one of the key components of our secure multitenant messaging―isolation of data.
  
### What is Logical interface (LIF)?
A LIF is an IP address or a worldwide port name (WWPN) that is associated with a port. It is associated with attributes such as failover groups, failover rules, and firewall rules. A LIF communicates over the network through the port (physical or virtual) to which it is currently bound.

### Difference between IPSpace and Broadcast domain
An IPspace defines a distinct IP address space within the cluster and is a way to allocate a separate network space to provide secure administration and routing for SVMs.
A broadcast domain groups ports that belong in the same Layer 2 network and sets the MTU for the broadcast domain ports. Broadcast domains are assigned to an IPspace. An IP space can contain one or more broadcast domains.

### What is NBlade?
N-blade means Network blade which handles the networking, NFS and CIFS requests and then translates to SpinNP requests as inputs to Cluster session manager

### What is DBlade?
D-blade means Data blade, which contains the WAFL file systems then handles the SpinNP requests and them communicate disks and tape devices using FC.

### What is SCSI-Blade?
The SCSI-blade handles the networking, FC, FCoE and iSCSI requests and then translates to SpinNP requests as inputs to CSM.

### What is Cluster Seesion Manager?
Cluster Session Manager (CSM) is a communication channels to exchange information between nodes in a cluster.

### What is Volume Location Database?
VLDB contains Index of each aggregate ownership information and containing volume information. That is the reason we can easily move volumes from one aggregate to another aggregate. The system needs to keep track of where each volume is located, and it's the VLDB that does that.

### What is Epsilon?
Epsilon is assigned to a single node in the cluster. It gives an extra fractional voting weight, which is a deciding factor when the connectivity between two equal portions of a large cluster fails. The group of nodes containing epsilon maintains quorum. It is needed to avoid “Split Brain” situation, when both halves of the cluster could end up having two separate read/write copies of replicated databases. Epsilon is automatically assigned to the first node when the cluster is created. In case of a node failure, the epsilon is automatically reassigned to a healthy node.

### What is Quorum
Quorum is a precondition for a fully-functioning cluster. When a cluster is in quorum, a simple majority of nodes are healthy and can communicate with each other. When quorum is lost, the cluster loses the ability to accomplish normal cluster operations. Only one collection of nodes can have quorum at any one time because all of the nodes collectively share a single view of the data. Therefore, if two non-communicating nodes are permitted to modify the data in divergent ways, it is no longer possible to reconcile the data into a single data view. Each node in the cluster participates in a voting protocol that elects one node master; each remaining node is a secondary. The master node is responsible for synchronizing information across the cluster. When quorum is formed, it is maintained by continual voting; if the master node goes offline, a new master is elected by the nodes that remain online.


### What is Load sharing mirrors
A load-sharing mirror reduces the network traffic to a FlexVol volume by providing additional read-only access to clients. You can create and manage load-sharing mirrors to distribute read-only traffic away from a FlexVol volume. Load-sharing mirrors do not support Infinite Volumes.

### What is a NameSpace?
A NAS namespace is a logical grouping of volumes joined together at junction points to create a single file system hierarchy. A client with sufficient permissions can access files in the namespace without specifying the location of the files in storage. Junctioned volumes can reside anywhere in the cluster.

### What is consistensy point? How its differ from Snapshot?
A Consistency point triggered Whenever the filesystem reaches a point where it watns to update the physical data on the disks, with whatever has accumulatted in cache (And was journaled in NVRAM). 
A Snapshot is create wherever the snap-schedule is configured to trigger it or any other operations (SnapManger, SnapDrive, Snapmirror, Snapvault, Administrator) creates a new snapshot. creating a snapshot also triggers a consistency point, because the snapshot is always a consistent image of the file system as this point in time.

### Explain Snapmirror Types
The SnapMirror Async mode replicates Snapshot copies from a source volume or qtree to a destination. It will support to replicate more than 800Kms Long. volume or qtree. Incremental updates are based on a schedule or are performed manually using the snapmirror update command. Async mode works with both volume SnapMirror and qtree SnapMirror.

SnapMirror Sync mode replicates writes from a source volume to a destination volume at the same time it is written to the source volume. SnapMirror Sync is used in environments that have zero tolerance for data loss. it will note support more then 300Kms long.

SnapMirror Semi-Sync provides a middle-ground solution that keeps the source and destination systems more closely synchronized than Async mode, but with less impact on performance.

### Explain how De-Duplication works?
In the context of disk storage, De-duplication refers to any algorithm that searches for duplicate data objects (for example, blocks, chunks, files) and discards those duplicates. When duplicate data is detected, it is not retained, but instead a “data pointer” is modified so that the storage system references an exact copy of the data object already stored on disk. This De-duplication feature works well with datasets that have lots of duplicated date (for example, full backups).

### Diff between XDP & DP snapmirror relationship?

SnapMirror extended data protection (XDP)
XDP, SnapVault and version independent SnapMirror uses LRE (Logical Replication Engine)
LRE (suited for archival type of scenario) = Tracks the data "logically" and is based on the file-system structure.
Replication is faster than DP

SnapMirror data protection (DP)
"DP" are block-based and uses BRE (Block Replication Engine)
BRE (suited for disaster type of scenario) = Tracks each "block" and is unaware of file-system structure.
Replication is little slower then XDP (since it tracks each block change and replicate the same to destination)

### what is portset?

### What is initiator group?
### How to solve CIFS unaccessible issue?
### How to solve NFS unaccessible issue?
### What is infinite volume?
### What is flexgroup volume?
### How to convert DP to XDP snapmirror relationship?
- Snapmirror quiesce  -source-path svm:volA -destination-path svm:volb
- snapmirror break -source-path svm:volA -destination-path svm:volb
- snapshot autodelete modify -vserver VSERVER1 -volume VOLUME1 -enabled false
- snapmirror delete -source-path svm:volA -destination-path svm:volb
- snapmirror create -source-path svm:volA -destination-path svm:volb -type XDP -policy MirrorAllSnapshots

### Types of Logical interfaces (LIFs)?
- Node Management LIF
- Cluster Management LIF
- Data LIF
- Cluster LIf
- InterCluster LIF

### What a cluster replication ring?
A replication ring is a set of identical processes running on all nodes in the cluster. The basis of clustering is the replicated database (RDB). An instance of the RDB is maintained on each node in a cluster. There are a number of processes that use the RDB to ensure consistent data across the cluster

### Can we move volumes between different Vservers?
The Answer is we can rehost the volume from one SVM to another SVM using volume rehost command.

Several conditions must be met before you can rehost a volume from one SVM to another:
- The volume must be online.
- Protocols: SAN or NAS. For the NAS protocol, the volume must be unmounted.
- If the volume is in a SnapMirror relationship, then the relationship must be either deleted or broken prior to volume rehost. You can resynchronize the SnapMirror relationship after the volume rehost operation.

### How do you setup the cluster?
To setup the cluster first you need to connect internal network connections and VLANs in place. 
You can run cluster setup from Command line (Connect to  as well as from GUI once initial cluster is create from CLI.

### What happens when 4 disks fails in RAID-TEC?
RAID-TEC is supported on all disk types and all platforms, including AFF. Aggregates that contain larger disks have a higher possibility of concurrent disk failures. RAID-TEC helps to mitigate this risk by providing triple-parity protection so that your data can survive up to three simultaneous disk failures. RAID-TEC is the default RAID policy for capacity HDD aggregates with disks that are 6 TB or larger. If 4 disks failed RAID-TEC will go into degraded mode (we may not able to recover the data).

### Why we need to do portset?
### What is the maximum capacity of the volume in cluster mode ?
### Client is reporting CIFS shares slowness how will you resolve
### NFS client is reporting latency how will you resolve
### How Data Read Request processes in Netapp?
### Explain NetApp Architecture
