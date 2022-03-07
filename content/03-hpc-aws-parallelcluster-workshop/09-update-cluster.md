+++
title = "h. Update your cluster"
date = 2022-03-01T10:46:30-04:00
weight = 100
tags = ["tutorial", "create", "ParallelCluster"]
+++

We have sucessfully built your cluster and ran your first MPI job.

Let's say you want to change your instance type to a different instance type in your compute fleet for example **c4.large** . In this lab, we will learn how to update your cluster with new instance type.


Go back to your AWS Cloud9 environment, and list the cluster name (if you don't remember it).

```bash
pcluster list-clusters
```

Edit your original config file and change `InstanceType: c4.large`

```bash
vi config
```

```bash
- Name: compute
  ComputeResources:
    - Name: c4large
      InstanceType: c4.large
```

You would need to stop the cluster (the compute fleet) using the following command:
```bash
pcluster update-compute-fleet --cluster-name hpc --status STOP_REQUESTED
```

Then run a **pcluster update-cluster** command
```bash
pcluster update-cluster --cluster-name hpc --cluster-configuration config
```

Start your cluster again after update process is completed.

```bash
pcluster update-compute-fleet --cluster-name hpc --status START_REQUESTED
```

You can now login to your cluster and run your helloworld job again. You can see that the cluster compute node has changed to c4.large.

```bash
[ec2-user@ip-172-31-39-157 ~]$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST 
compute*     up   infinite      8  idle~ compute-dy-c4large-[1-8] 
```

Now you have a better understanding on how AWS ParallelCluster operates. For more information, see the [Configuration](https://docs.aws.amazon.com/parallelcluster/latest/ug/cluster-configuration-file-v3.html) section of the *AWS ParallelCluster User Guide*.
