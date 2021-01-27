# This repo replicate the issue on creating a AWS Batch compute environment 

The user account has the IAM policy at [this link](https://github.com/seqeralabs/nf-tower-aws/blob/master/forge/forge-policy.json).

#### Service Role 

* ARN: `arn:aws:iam::195996028523:role/TowerForge-4IgIbmOvmsK3HX6ts4MPEh-ServiceRole`
* Permissions: 
  - `AWSBatchServiceRole`


#### Spot fleet role

* ARN: `arn:aws:iam::195996028523:role/TowerForge-4IgIbmOvmsK3HX6ts4MPEh-FleetRole` 
* Permissions: 
  - `AmazonEC2SpotFleetTaggingRole`

#### Instance Role 

* ARN: `arn:aws:iam::195996028523:instance-profile/TowerForge-4IgIbmOvmsK3HX6ts4MPEh-InstanceRole`
* Permissions: 
  - `AmazonS3ReadOnlyAccess`
  - `AmazonEC2ContainerServiceforEC2Role`
  + Inline policies below
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "batch:DescribeJobQueues",
                "batch:CancelJob",
                "batch:SubmitJob",
                "batch:ListJobs",
                "batch:DescribeComputeEnvironments",
                "batch:TerminateJob",
                "batch:DescribeJobs",
                "batch:RegisterJobDefinition",
                "batch:DescribeJobDefinitions",
                "ecs:DescribeContainerInstances",
                "ecs:DescribeTasks",
                "ec2:DescribeInstances",
                "ec2:DescribeInstanceAttribute",
                "ec2:DescribeInstanceTypes",
                "ec2:DescribeInstanceStatus"
            ],
            "Resource": "*"
        }
    ]
}
```  
  
 ```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListObjectsInBucket",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::nextflow-ci"
            ]
        },
        {
            "Sid": "AllObjectActions",
            "Effect": "Allow",
            "Action": "s3:*Object",
            "Resource": [
                "arn:aws:s3:::nextflow-ci/*"
            ]
        }
    ]
}
 ```

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Action": [
            "ec2:AttachVolume",
            "ec2:DescribeVolumeStatus",
            "ec2:DescribeVolumes",
            "ec2:ModifyInstanceAttribute",
            "ec2:DescribeVolumeAttribute",
            "ec2:CreateVolume",
            "ec2:DeleteVolume",
            "ec2:CreateTags"
        ],
        "Resource": "*",
        "Effect": "Allow"
    }
}
```


### Execution 

To run the snipped run `./gradlew run`
