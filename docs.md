# Documentation 

## Pre-requisites

Make sure to configure the XPACK license and the plugin as described
in the [README](README.md#configuration).

## AWS Batch Pro executor

The `xpack-amzn` plugin implements an advanced version of the AWS Batch executor
for Nextflow, which supports the use of a shared file system instead of an S3 bucket
as the pipeline work directory.

## Using Amazon EFS

[Amazon EFS](https://aws.amazon.com/efs/) is a shared file-system based on the 
NFS protocol provided by AWS. 

To learn more about EFS and how to create an EFS instance, check out the [AWS documentation](https://docs.aws.amazon.com/efs/latest/ug/creating-using-create-fs.html).

Once you have created your desired EFS instances, you can make them accessible to your
pipeline with the `efsVolumes` option in your Nextflow configuration:

```groovy
aws.batch.efsVolumes.'efs-1234567890'.mountPath = '/mnt/efs'
```

In the above snippet, replace `efs-1234567890` with the ID of your EFS instance and
the path `/mnt/efs` with one of your choice. Repeat this configuration for each
EFS instance that you want to use in your pipeline.

You can then use an EFS instance as the work directory based on its mount path:

```groovy
workDir = '/mnt/efs'
```

Available options:

`aws.batch.efsVolumes.'<ID>'.mountPath`
: The host path to which the file system should be made available (default: none)

`aws.batch.efsVolumes.'<ID>'.rootPath`
: The file system directory that should be made available through the mount point (default: `/`) 

`aws.batch.efsVolumes.'<ID>'.readOnly`
: When `true` mounts the file system as read-only (default: `false`)

*Note: Replace `<ID>` with your EFS instance ID.*

## Using a POSIX-based shared file-system

With the `xpack-amzn` plugin, you can use any POSIX-based shared file-system with 
AWS Batch, such as [Amazon FSx](https://aws.amazon.com/fsx/), [Qumolo](https://qumulo.com/), [Weka](https://www.weka.io/), etc.

The provisioning and management of such file systems are your responsibility. Typically,
these file systems must be mounted in the launch template used to execute tasks.

As with EFS, you can then use the shared file system as the work directory based on its mount path:

```groovy
workDir = '/mnt/fsx'
```

You can also mount additional shared file systems into the task containers with the `aws.batch.volumes`
config option. See the [Nextflow documentation](https://nextflow.io/docs/latest/aws.html#volume-mounts)
for more details.
