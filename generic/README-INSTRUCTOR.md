# Instructor notes
========================================

## Before you start

See ../README.md for instructions on using the cluster management scripts.

### a) Deploy cluster(s)

1. Get the repo and switch to the 'generic' directory

    ```
git clone https://github.com/seanorama/masterclass
cd masterclass/generic
    ```

2. Set these variables, updating the values as appropriate:

   ```sh
export AWS_DEFAULT_REGION=eu-west-1  ## region to deploy in
export lab_prefix=test         ## template for naming the cloudformation stacks
export lab_first=100                 ## number to start at in naming
export lab_count=1                   ## number of clusters to create

export cfn_parameters='
[
  {"ParameterKey":"KeyName","ParameterValue":"secloud"},
  {"ParameterKey":"SubnetId","ParameterValue":"subnet-7e49641b"},
  {"ParameterKey":"SecurityGroups","ParameterValue":"sg-f915bc9d"},
  {"ParameterKey":"AmbariServices","ParameterValue":"HDFS MAPREDUCE2 PIG YARN ZOOKEEPER HIVE SPARK"},
  {"ParameterKey":"AdditionalInstanceCount","ParameterValue":"0"},
  {"ParameterKey":"PostCommand","ParameterValue":"curl -sSL https://raw.githubusercontent.com/seanorama/masterclass/master/generic/setup.sh | bash"},
  {"ParameterKey":"InstanceType","ParameterValue":"m4.xlarge"},
  {"ParameterKey":"BootDiskSize","ParameterValue":"80"}
]
'
   ```

3. Create the cluster(s): `../bin/clusters-create.sh`

4. List cluster host(s): `../bin/clusters-report.sh`

5. Terminate cluster(s): `../bin/clusters-terminate.sh`

## REMEMBER to terminate the clusters immediately after the class is over, or be prepared to pay $$$!

Further, you should verify deletion of the CloudFormations & EC2 instances from the AWS Console.

## Issues: See ../README.md

## Advanced usage

1. Only deploy the infrastructure by setting PostCommand to /bin/true
