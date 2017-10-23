---
layout: post
title: "VMware Socal Usercon 2017"
published: true
tags: vmware
---

I had a chance to attend a local Vmware User in Anaheim last Friday, 10/13/2017. This is a free, one-day event organized by VMUG community. The day was packed with great topics covering Vmware's full stack. One thing I really like about it is that it's a small gathering and I got a chance to talk shop with other VMware architects and admins which to me was very insightful. 

#### Key Takeaways

Vmware is not just about VMs anymore. The keynote was about "Software Defined Data Center" and how committed VMware is to this stack. They cover end to end technologies to run every datacenter; from Compute (Vsphere), Networking (NSX), Storage (vSAN) with vRealize Automation to wrap all these core services. VMware is late to the game, but everything is now API Driven. vRA now also supports Terraform so you can build your entire SDDC cluster with Terraform. Exciting times. 




**Vmware Cloud on AWS (VMC)** - This product is currently on Tech Preview. Vsphere is now available on AWS Marketplace which allows you to extend your on-prem vmware cluster and `vmotion` to your vmware cluster in AWS. VMware is finally realizing the fact that cloud computing will just continue to ramp up and so they'll have to take a piece of that pie, of course. The product is still new (feels alpa/beta to me) but vmware reps are saying a Fortune 500 client is already using it. 
The AWS cluster is running on a Baremetal server in Amazon. It's not a nested setup (A esxivm on top of another vm)

  * You'll need a minimum of 4 servers in your cluster
  * Each server will have 144 cores, 40TB NVME disk and 2TB disk memory
  * VMware SDDC running on your AWS: vSAN, NSX, vSphere 
  * You'll have a single pane of glass to manage both your on-prem and aws cluster
  * It can be integrated with native AWS services 
  * Supports multiple datastore
  * VMC requires NSX to run on AWS but it does not require NSX on-prem 
  * AWS cluster is fully managed by VMware. They will take care of updates, maintenance. It is a real hands off approach
  * Very expensive: $50k per host/per year 

**VM Backup Best Practices**
  * Try using a lower retention for Backups 
  * Do not reboot vcenter while it's being backed up 
  * Run vcenter on the fastest disk 
  * Separate backup datastores for Windows and Linux servers due to snapshot handling 
  * Look at the compression level of your backups. Higher compression, the slower backups will run (higher cpu too) 
  * You can use Vsphere Tags for backups too. ie: setup a "No-backup", "No Encryption" etc tags

**DR Architecture Design** - This talk was the main reason why I attended this vmug, as part on my ongoing research for our BCDR project.

**Know what we are trying to protect.** 
  * What should we plan for?  Natural Disaster (ie Earthquakes etc), Power loss, Human Error ie: Oooops! 
  * How do we begin?
  * Create a Business Impact Analysis (BIA) - These are the questions we need to get answered
  * What is the monetary impact of a Data Center outage or failure? How much money are we going to lose? 
  * What is the most critical business process?
  * Identify application tiers? P1 - Immediate recovery, P2 - 1 to 2-day recovery, P3 - 3 to 5-day recovery, P4 - Best efforts recovery
  * Identify RPO and RTO  
  * RPO - How much data can we lose? RTO - How long can we be dark? 

**BC vs DR vs OR - Say what?!** 
  * BC - Business Continuity - Could lose a datacenter and all goes on as normal. This is your active/active setup
  * DR - Disaster Recovery - Recover from an outage to an alternative site. This is your active/passive setup 
  * OR - Operational Recovery - Smaller scope events. Hard disk failing, HBA failures etc 
  * Key Evaluation Criteria for BCDR
  * Reliability of Data Recovery
  * Speed of Data Recovery 

**Types of Learning** - There was another talk about types of Learning. It was presented by the VP of VMware training services but I still found his talk interesting. 
  * "On the Job" Training - This can be stressful and you'll have to rely on other "experts" to help you out. You'll have limited time to understand the tech and is prone to mistakes and development of less than ideal best practices
  * Digital Training Videos / e-learning - This is typically short and on the point and it may or may not include actual facts. Make sure you understand the source of info since the context and examples may not apply to your situation. This is usually perfect for "just in time training"
  * Instructor-Led Training - Forms a strong foundation of knowledge and understanding. It is interactive, and can provide an in-depth understanding of the technology. This is also the most expensive form of training. 

### Various Links 
* [Hands-on Labs](http://labs.hol.vmware.com)
* [Hands-on Labs Documentation](http://docs.hol.vmware.com)
* [Official VMware Doc Site](https://docs.vmware.com)
* [VMware Cloud Docs](http://blog.cloud.vmware.com)
* [VMware training sites](http://vmware.com/education)
* [Veeam POC guide](https://bp.veeam.expert/poc_guide/enhanced_evaluation_example.html)
* [Free Veeam Products](https://www.veeam.com/virtual-machine-backup-solution-free.html)
