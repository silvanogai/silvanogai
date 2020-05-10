---
layout: post
comments: true
author: Silvano Gai & Diego Crupnicoff
title:  NVMe standards and applications
excerpt: Silvano Gai interviews Diego Crupnicoff, a well-known NVMe expert.
description: An interview with Diego Crupnicoff
---

*In this podcast, I interview [Diego Crupnicoff](https://pensando.io/about/#bio-11), a well known Storage and RDMA expert, and ask him to explain the NVMe standards and applications.*

<iframe title="NVMe Overview - A discussion with Diego Crupnicoff" style="border: none;" scrolling="no" data-name="pb-iframe-player" src="https://www.podbean.com/media/player/hzzf9-dbca3c?from=yiiadmin&download=1&version=1&skin=1&btn-skin=107&auto=0&share=1&fonts=Helvetica&download=1&rtl=0&pbad=1" width="100%" height="122"></iframe>

*You can find the official NVMe website at* [https://nvmexpress.org/](https://nvmexpress.org/).

*Diego also provided this additional explanation.*

---

During the past decade, solid state drives (SSDs) started to become economically viable. They provide superior performance compared to rotating media hard disks. To fully exploit SSD capabilities, a new Non-Volatile Memory express (NVMe) standard was created as a more modern alternative to the established SCSI and ATA models.

NVMe was released in 2011 as an open logical device interface specification for accessing nonvolatile storage media attached via PCIe. NVMe has been designed to take advantage of the low latency and high internal parallelism of flash-based storage devices. As a result, NVMe reduces I/O overhead and brings various performance improvements relative to previous logical-device interfaces, including multiple, long command queues and reduced latency.

In order to efficiently leverage the advantages of the NVMe model with network attached storage, a remote flavor of NVMe named NVMe over Fabrics (NVMe-oF) was specified in 2016. NVMe-oF defines extensions to NVMe that allow remote storage access over RDMA, Fibre Channel and TCP.


![NVMe protocol stack](/assets/images/nvme-1.png)

NVMe-oF can be natively exposed to the storage client as shown in the figure below. This approach, entails the deployment of new storage management techniques (represented by the Remote Storage Management component shown in the figure below) that affect the way storage services are offered to the host. This is because under this scheme, host management infrastructure (e.g. OS stack, host admins, provisioning agents),  must deal with the explicitly remote aspects of storage such as remote access permissions, mounting of specific remote volumes, and so on.

In some cases, exposing the remote nature of storage to the client could present some challenges, notably in virtualized environments where a cloud tenant manages a guest OS image, which assumes the presence of local disks. One common solution is for the hypervisor to virtualize the remote storage and emulate a local disk toward the virtual machine as shown in the figure. This emulation abstracts the paradigm change from the perspective of the guest OS.

![NVMe over Fabric](/assets/images/nvme-2.png)

However, hypervisor-based storage virtualization is not a suitable solution in all cases. For example, in bare-metal environments, tenant-controlled OS images run on the actual physical machines with no hypervisor to create the emulation. Also, when implemented at the hypervisor, NVMe emulation consumes precious CPU cycles that could be otherwise devoted to billable workloads.

In view of above, and realizing that the particulars of storage disaggregation are actually a characteristic of the underlying infrastructure, a hardware NVMEe virtualization model is becoming more common. This approach, as shown in the figure below, presents to the physical server the illusion of a local hard disk. The underlying implementation virtualizes access across the network using standard or proprietary remote storage protocols. One typical approach is to emulate a local NVMe disk and use NVMe-oF to access the remote storage.

![NVMe Emulation](/assets/images/nvme-3.png)

The Pensando DSC product line, leveraging its high performance programmable dataplane, natively supports both of the above remote storage models.

---

My book has a full Chapter on NVMe (Chapter 6) written by Diego. Don't Forget that Pearson/Addison-Wesley has a special offer on my latest book. To save 35% on the book or eBook go to [the informit website](https://www.informit.com/store/building-a-future-proof-cloud-infrastructure-a-unified-9780136624097?utm_source=pensando&utm_medium=website&utm_campaign=bookad) and use code FUTUREPROOF during checkout to apply the discount.

Offer expires December 31, 2020

![Book Cover](/assets/images/book-cover.jpg)

You can read [an independent review of the book here.](https://www.linkedin.com/posts/activity-6642125779486539776-FJAj/)

The book was also listed in [The Top 10 Best Cloud Storage Books You Need to Read in 2020.](https://solutionsreview.com/data-storage/the-top-10-best-cloud-storage-books-you-need-to-read-in-2020/)
