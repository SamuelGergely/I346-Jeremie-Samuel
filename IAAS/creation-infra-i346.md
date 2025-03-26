# Deploy infrastructure

## Installation et configuration du CLI

* [Installer le client git](https://git-scm.com/)
  * Git bash vous embarque de nombreuses commandes Linux utiles pour s'entrainer avec S3 (cat, grep, touch, ls)
* [Installation du CLI - v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Configuration du CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html#getting-started-quickstart-existing)
  * Les clés vous ont été partagées par oneDrive
* [Gestion des profiles](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-format-profile)
  
  * Vous devez créer un profile du nom de votre équipe et l'utiliser pour toute les futures commandes
  ```
  aws ec2 <la commande> --profile devopsteam04
  ```

## Schéma de l'infrastructure avec Eraser
![alt text](<Capture_d'ecran_2025-03-18_135348.jpg>)

## Afficher le subnet de l'équipe 4 une région sous forme de tableau
```bash
aws ec2 describe-vpcs \
--profile devopsteam04-i346 \
--region eu-central-1 \
--output table
```

```
[OUTPUT]
-----------------------------------------------------------
|                      DescribeVpcs                       |
+---------------------------------------------------------+
||                         Vpcs                          ||
|+----------------------+--------------------------------+|
||  CidrBlock           |  10.0.0.0/16                   ||
||  DhcpOptionsId       |  dopt-05854b009a610ac91        ||
||  InstanceTenancy     |  default                       ||
||  IsDefault           |  False                         ||
||  OwnerId             |  709024702237                  ||
||  State               |  available                     ||
||  VpcId               |  vpc-0a22d771f16ae549d         ||
|+----------------------+--------------------------------+|
|||               BlockPublicAccessStates               |||
||+------------------------------------------+----------+||
|||  InternetGatewayBlockMode                |  off     |||
||+------------------------------------------+----------+||
|||               CidrBlockAssociationSet               |||
||+----------------+------------------------------------+||
|||  AssociationId |  vpc-cidr-assoc-0fad6e9a11ccae331  |||
|||  CidrBlock     |  10.0.0.0/16                       |||
||+----------------+------------------------------------+||
||||                  CidrBlockState                   ||||
|||+-------------------+-------------------------------+|||
||||  State            |  associated                   ||||
|||+-------------------+-------------------------------+|||
|||                        Tags                         |||
||+----------------------+------------------------------+||
|||  Key                 |  Name                        |||
|||  Value               |  vpc-i346                    |||
||+----------------------+------------------------------+||
```

## Afficher tout les VPCs disponibles dans une région sous forme de tableau
* [Source](https://awscli.amazonaws.com/v2/documentation/api/2.1.21/reference/ec2/describe-subnets.html)
```bash
aws ec2 describe-subnets \
--profile devopsteam04-i346 \
--region eu-central-1 \
--subnet-ids subnet-02d0c07be4b48422c \
--output table
```

```
[OUTPUT]

------------------------------------------------------------------------------------------------------------
|                                              DescribeSubnets                                             |
+----------------------------------------------------------------------------------------------------------+
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.4.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-02d0c07be4b48422c  ||
||  SubnetId                    |  subnet-02d0c07be4b48422c                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.4.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
```

## Afficher tout les subnets présent sur le VPC
* [Source](https://awscli.amazonaws.com/v2/documentation/api/2.1.21/reference/ec2/describe-subnets.html)
```bash
aws ec2 describe-subnets \
--profile devopsteam04-i346 \
--region eu-central-1 \
--output table
```

```
[OUTPUT]

------------------------------------------------------------------------------------------------------------
|                                              DescribeSubnets                                             |
+----------------------------------------------------------------------------------------------------------+
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.10.0/28                                                           ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0c409522b892fc4bf  ||
||  SubnetId                    |  subnet-0c409522b892fc4bf                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+---------------------------+--------------------------------------------------------------------------+||
|||  Key                      |  Name                                                                    |||
|||  Value                    |  subnet-10.0.10.0/28                                                     |||
||+---------------------------+--------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.4.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-02d0c07be4b48422c  ||
||  SubnetId                    |  subnet-02d0c07be4b48422c                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.4.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.2.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-06924d9bed0d3f9fa  ||
||  SubnetId                    |  subnet-06924d9bed0d3f9fa                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.2.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.8.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-04000c6ac17aa87cd  ||
||  SubnetId                    |  subnet-04000c6ac17aa87cd                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.8.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  10                                                                     ||
||  CidrBlock                   |  10.0.0.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-007585998051b2c4a  ||
||  SubnetId                    |  subnet-007585998051b2c4a                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------------+-------------------------------------------------------------------+||
|||  Key                             |  Name                                                             |||
|||  Value                           |  public-subnet                                                    |||
||+----------------------------------+-------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.6.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0abac7e48b2a18a65  ||
||  SubnetId                    |  subnet-0abac7e48b2a18a65                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.6.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.1.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0fc3126df64eea2b9  ||
||  SubnetId                    |  subnet-0fc3126df64eea2b9                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.1.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.99.0/28                                                           ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0cfda26e6ed7eeeca  ||
||  SubnetId                    |  subnet-0cfda26e6ed7eeeca                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+---------------------------+--------------------------------------------------------------------------+||
|||  Key                      |  Name                                                                    |||
|||  Value                    |  subnet-10.0.99.0/28                                                     |||
||+---------------------------+--------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.5.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-092ced6aa04603165  ||
||  SubnetId                    |  subnet-092ced6aa04603165                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.5.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.3.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0aaee76144e27a3dd  ||
||  SubnetId                    |  subnet-0aaee76144e27a3dd                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.3.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.9.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0ab631f69a314e92d  ||
||  SubnetId                    |  subnet-0ab631f69a314e92d                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.9.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.7.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-01cfa9e1ea9fb3d90  ||
||  SubnetId                    |  subnet-01cfa9e1ea9fb3d90                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.7.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
```

## List Route Table sur un VPC
* [Source](https://awscli.amazonaws.com/v2/documentation/api/2.1.30/reference/ec2/describe-route-tables.html)
* [Query](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/dynamodb/query.html)
```bash
aws ec2 describe-route-tables \
--filters "Name=vpc-id,Values=MyVpc" \ 
--profile devopsteam04-i346 \ 
--region eu-central-1 \ 
--query "RouteTables[*].{RouteTableId:RouteTableId, VpcId:VpcId, Associations:Associations}" \ 
--output table
```

```
[OUTPUT]

-------------------------------------------------------------
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-0a9293aaf3c30b82c             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
||                      Associations                       ||
|+--------------------------+------------------------------+|
||  Main                    |  True                        ||
||  RouteTableAssociationId |  rtbassoc-02bc78e3a4b73050c  ||
||  RouteTableId            |  rtb-0a9293aaf3c30b82c       ||
|+--------------------------+------------------------------+|
|||                   AssociationState                    |||
||+--------------------+----------------------------------+||
|||  State             |  associated                      |||
||+--------------------+----------------------------------+||
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-069f0fe8e2ed1ff37             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
||                      Associations                       ||
|+--------------------------+------------------------------+|
||  Main                    |  False                       ||
||  RouteTableAssociationId |  rtbassoc-06c884888a865c8f0  ||
||  RouteTableId            |  rtb-069f0fe8e2ed1ff37       ||
||  SubnetId                |  subnet-007585998051b2c4a    ||
|+--------------------------+------------------------------+|
|||                   AssociationState                    |||
||+--------------------+----------------------------------+||
|||  State             |  associated                      |||
||+--------------------+----------------------------------+||
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-00b3f747f972f123a             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-01ebe5717e9104f85             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-0e48c9ae2d1e0e4b9             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-0b68177540d710b1a             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-07668590cdc381b07             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-09eea99d8ac647a5f             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
||                      Associations                       ||
|+--------------------------+------------------------------+|
||  Main                    |  False                       ||
||  RouteTableAssociationId |  rtbassoc-067eb31bcc2d1a3cc  ||
||  RouteTableId            |  rtb-09eea99d8ac647a5f       ||
||  SubnetId                |  subnet-092ced6aa04603165    ||
|+--------------------------+------------------------------+|
|||                   AssociationState                    |||
||+--------------------+----------------------------------+||
|||  State             |  associated                      |||
||+--------------------+----------------------------------+||
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-03d962d4967937170             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-0acd33fa1f46d6e21             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-0f49e7901c1b634f0             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-0a8386540207d7a99             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-005b030aec917782b             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
|                    DescribeRouteTables                    |
+----------------------+------------------------------------+
|  RouteTableId        |  rtb-07bf97cd343c65b4c             |
|  VpcId               |  vpc-0a22d771f16ae549d             |
+----------------------+------------------------------------+
||                      Associations                       ||
|+--------------------------+------------------------------+|
||  Main                    |  False                       ||
||  RouteTableAssociationId |  rtbassoc-0a41421456eb54417  ||
||  RouteTableId            |  rtb-07bf97cd343c65b4c       ||
||  SubnetId                |  subnet-0aaee76144e27a3dd    ||
|+--------------------------+------------------------------+|
|||                   AssociationState                    |||
||+--------------------+----------------------------------+||
|||  State             |  associated                      |||
||+--------------------+----------------------------------+||
```

## Create Route Table
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-route-table.html)
```bash
aws ec2 create-route-table \ 
--vpc-id vpc-0a22d771f16ae549d \
--region eu-central-1 \
--profile devopsteam04-i346 
```

```
[OUTPUT]

{
    "RouteTable": {
        "Associations": [],
        "PropagatingVgws": [],
        "RouteTableId": "rtb-0e9c1c8c5262297e0",
        "Routes": [
            {
                "DestinationCidrBlock": "10.0.0.0/16",
                "GatewayId": "local",
                "Origin": "CreateRouteTable",
                "State": "active"
            }
        ],
        "Tags": [],
        "VpcId": "vpc-0a22d771f16ae549d",
        "OwnerId": "709024702237"
    },
    "ClientToken": "bfe7fbb0-8a59-43ba-991e-387bb84c2f45"
}

```

## Name Route Table
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/mq/create-tags.html)
```bash
aws ec2 create-tags \
--resources rtb-0e9c1c8c5262297e0 \
--tags Key=Name,Value="private-rte-table-devopsteam04-i346" \
--profile devopsteam04-i346 \
--region eu-central-1
```

```
[OUTPUT]

None
```

## Delete Route Table
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/delete-route-table.html)
```bash
aws ec2 delete-route-table \
--route-table-id rtb-22574640 \
--profile devopsteam04-i346 \
--region eu-central-1
```

```
[OUTPUT]

None
```

## Associate Route table to Subnet
* [Source](https://awscli.amazonaws.com/v2/documentation/api/2.7.25/reference/ec2/associate-route-table.html)
```bash
aws ec2 associate-route-table \
--route-table-id rtb-0e9c1c8c5262297e0 \
--subnet-id subnet-02d0c07be4b48422c \
--profile devopsteam04-i346 \
--region eu-central-1
```

```
[Output]

{
    "AssociationId": "rtbassoc-00fba39d410526628",
    "AssociationState": {
        "State": "associated"
    }
}
```

## Create route
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-route.html)
```bash
aws ec2 create-route \
--route-table-id rtb-0e9c1c8c5262297e0 \
--destination-cidr-block 0.0.0.0/0 \
--network-interface-id eni-0e382f5c175b09ce2 \
--profile devopsteam04-i346 \
--region eu-central-1
```

```
[OUTPUT]

{
    "Return": true
}
```

# Deploy Instance

## Create and upload private key pairs
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-key-pair.html)
```bash
aws ec2 create-key-pair \
--key-name KEY-I346-SUB-DEVOPSTEAM04 \
--key-type rsa \
--key-format pem \
--tag-specifications 'ResourceType=key-pair,Tags=[{Key=Name,Value=KEY-I346-SUB-DEVOPSTEAM04}]' \
--region eu-central-1 \
--profile devopsteam04-i346 \
--output text > KEY-I346-SUB-DEVOPSTEAM04.pem
```

```
[OUTPUT]
None
```

## Create Subnet security group
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-security-group.html)
```bash
aws ec2 create-security-group \
--group-name secugrp-i346-devopsteam04 \
--description "secugrp-i346-devopsteam04" \
--vpc-id vpc-0a22d771f16ae549d \
--tag-specifications 'ResourceType=security-group,Tags=[{Key="Name",Value="SG-DEVOPSTEAM04-SUBNET"}]' \
--region eu-central-1 \
--profile devopsteam04-i346 \
--output table

```

```
[OUTPUT]
---------------------------------------------------------------------------------------------------
|                                       CreateSecurityGroup                                       |
+------------------+------------------------------------------------------------------------------+
|  GroupId         |                                                        |
|  SecurityGroupArn|  arn:aws:ec2:eu-central-1:709024702237:security-group/sg-0c14ecd95a601269b   |
+------------------+------------------------------------------------------------------------------+
||                                             Tags                                              ||
|+-----------------------+-----------------------------------------------------------------------+|
||  Key                  |  Name                                                                 ||
||  Value                |  SG-DEVOPSTEAM04-SUBNET                                               ||
|+-----------------------+-----------------------------------------------------------------------+|

```

## Authorize Security Group - Ingress
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/authorize-security-group-ingress.html)
```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-0c14ecd95a601269b \
--ip-permissions "IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges=[{CidrIp=10.0.0.0/28,Description=SSH-FROM-DMZ}]" \
--region eu-central-1 
--profile devopsteam04-i346 \
--output table
```

```
[OUTPUT]
---------------------------------------------------------------------------------------------------------------
|                                        AuthorizeSecurityGroupIngress                                        |
+------------------------------------------------------------+------------------------------------------------+
|  Return                                                    |  True                                          |
+------------------------------------------------------------+------------------------------------------------+
||                                            SecurityGroupRules                                             ||
|+----------------------+------------------------------------------------------------------------------------+|
||  CidrIpv4            |  10.0.0.0/28                                                                       ||
||  Description         |  SSH-FROM-DMZ                                                                      ||
||  FromPort            |  22                                                                                ||
||  GroupId             |  sg-0c14ecd95a601269b                                                              ||
||  GroupOwnerId        |  709024702237                                                                      ||
||  IpProtocol          |  tcp                                                                               ||
||  IsEgress            |  False                                                                             ||
||  SecurityGroupRuleArn|  arn:aws:ec2:eu-central-1:709024702237:security-group-rule/sgr-0a9dc27cb7bb85acb   ||
||  SecurityGroupRuleId |  sgr-0a9dc27cb7bb85acb                                                             ||
||  ToPort              |  22                                                                                ||
|+----------------------+------------------------------------------------------------------------------------+|
```

## Deploy instance EC2 Linux
* [Source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/run-instances.html)
```bash
aws ec2 run-instances \
--image-id ami-0584590e5f0e97daa \
--count 1 \
--instance-type t2.micro \
--key-name KEY-I346-SUB-DEVOPSTEAM04 \
--security-group-ids sg-0c14ecd95a601269b \
--subnet-id subnet-02d0c07be4b48422c \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=EC2-DEVOPSTEAM04-LIN-SRV}]' \
--region eu-central-1 \
--profile devopsteam04-i346 \
--output table
```

```
[OUTPUT]
{
    "ReservationId": "r-0666e4120e12261d5",
    "OwnerId": "709024702237",
    "Groups": [],
    "Instances": [
        {
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "3605bcd9-7619-4acd-bfdd-c58a2af4a974",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2025-03-18T14:27:41+00:00",
                        "AttachmentId": "eni-attach-0e6b9c0308112e652",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupId": "sg-0c14ecd95a601269b",
                            "GroupName": "secugrp-i346-devopsteam04"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "0a:dc:13:ad:b7:95",
                    "NetworkInterfaceId": "eni-01d299b5b63bb036c",
                    "OwnerId": "709024702237",
                    "PrivateIpAddress": "10.0.4.13",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateIpAddress": "10.0.4.13"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-02d0c07be4b48422c",
                    "VpcId": "vpc-0a22d771f16ae549d",
                    "InterfaceType": "interface",
                    "Operator": {
                        "Managed": false
                    }
                }
            ],
            "RootDeviceName": "/dev/xvda",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupId": "sg-0c14ecd95a601269b",
                    "GroupName": "secugrp-i346-devopsteam04"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "EC2-DEVOPSTEAM04-LIN-SRV"
                }
            ],
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 1
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "optional",
                "HttpPutResponseHopLimit": 1,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            },
            "MaintenanceOptions": {
                "AutoRecovery": "default"
            },
            "CurrentInstanceBootMode": "legacy-bios",
            "Operator": {
                "Managed": false
            },
            "InstanceId": "i-094b7d04792679271",
            "ImageId": "ami-0584590e5f0e97daa",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "PrivateDnsName": "ip-10-0-4-13.eu-central-1.compute.internal",
            "PublicDnsName": "",
            "StateTransitionReason": "",
            "KeyName": "KEY-I346-SUB-DEVOPSTEAM04",
            "AmiLaunchIndex": 0,
            "ProductCodes": [],
            "InstanceType": "t2.micro",
            "LaunchTime": "2025-03-18T14:27:41+00:00",
            "Placement": {
                "GroupName": "",
                "Tenancy": "default",
                "AvailabilityZone": "eu-central-1c"
            },
            "Monitoring": {
                "State": "disabled"
            },
            "SubnetId": "subnet-02d0c07be4b48422c",
            "VpcId": "vpc-0a22d771f16ae549d",
            "PrivateIpAddress": "10.0.4.13"
        }
    ]
}

```

## Deploy instance EC2 WIN
* [Source]()
```bash
aws ec2 run-instances \
--image-id ami-045114d716addc65d \
--instance-type t3.micro \
--key-name KEY-I346-SUB-DEVOPSTEAM04 \
--security-group-ids sg-0c14ecd95a601269b \
--subnet-id subnet-02d0c07be4b48422c \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=EC2-DEVOPSTEAM04-WIN-SRV}]' \
--count 1 \
--profile devopsteam04-i346 \
--region eu-central-1
```

```
[OUTPUT]

{
    "ReservationId": "r-0bf6acfcf308ffc13",
    "OwnerId": "709024702237",
    "Groups": [],
    "Instances": [
        {
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "2e091c8b-9c20-41c3-abdd-cd8be9f442ec",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2025-03-18T14:25:29+00:00",
                        "AttachmentId": "eni-attach-054539afc836d8415",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupId": "sg-0c14ecd95a601269b",
                            "GroupName": "secugrp-i346-devopsteam04"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "0a:e9:87:d7:ef:65",
                    "NetworkInterfaceId": "eni-00f16c354df7eee9b",
                    "OwnerId": "709024702237",
                    "PrivateIpAddress": "10.0.4.4",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateIpAddress": "10.0.4.4"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-02d0c07be4b48422c",
                    "VpcId": "vpc-0a22d771f16ae549d",
                    "InterfaceType": "interface",
                    "Operator": {
                        "Managed": false
                    }
                }
            ],
            "RootDeviceName": "/dev/sda1",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupId": "sg-0c14ecd95a601269b",
                    "GroupName": "secugrp-i346-devopsteam04"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "EC2-DEVOPSTEAM04-WIN-SRV"
                }
            ],
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 2
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "required",
                "HttpPutResponseHopLimit": 2,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "BootMode": "uefi",
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            },
            "MaintenanceOptions": {
                "AutoRecovery": "default"
            },
            "CurrentInstanceBootMode": "uefi",
            "Operator": {
                "Managed": false
            },
            "InstanceId": "i-0bf136248db6b25e8",
            "ImageId": "ami-045114d716addc65d",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "PrivateDnsName": "ip-10-0-4-4.eu-central-1.compute.internal",
            "PublicDnsName": "",
            "StateTransitionReason": "",
            "KeyName": "KEY-I346-SUB-DEVOPSTEAM04",
            "AmiLaunchIndex": 0,
            "ProductCodes": [],
            "InstanceType": "t3.micro",
            "LaunchTime": "2025-03-18T14:25:29+00:00",
            "Placement": {
                "GroupName": "",
                "Tenancy": "default",
                "AvailabilityZone": "eu-central-1c"
            },
            "Platform": "windows",
            "Monitoring": {
                "State": "disabled"
            },
            "SubnetId": "subnet-02d0c07be4b48422c",
            "VpcId": "vpc-0a22d771f16ae549d",
            "PrivateIpAddress": "10.0.4.4"
        }
    ]
}
```

## Start/Stop/Terminate EC2
* [Source]()
```bash
#Start both :
aws ec2 start-instances \
--instance-ids i-094b7d04792679271 i-0bf136248db6b25e8 \
--profile devopsteam04-i346 \
--region eu-central-1


#Stop both:
aws ec2 stop-instances \
--instance-ids i-094b7d04792679271 i-0bf136248db6b25e8 \
--profile devopsteam04-i346 \
--region eu-central-1


#Terminate both :
aws ec2 terminate-instances \
--instance-ids i-094b7d04792679271 i-0bf136248db6b25e8 \
--profile devopsteam04-i346 \
--region eu-central-1

```

```
[OUTPUT]

Start :


Stop :
{
    "StoppingInstances": [
        {
            "InstanceId": "i-040fccbbbd58e5a36",
            "CurrentState": {
                "Code": 64,
                "Name": "stopping"
            },
            "PreviousState": {
                "Code": 16,
                "Name": "running"
            }
        }
    ]
}

Terminate :
{
    "TerminatingInstances": [
        {
            "InstanceId": "i-040fccbbbd58e5a36",
            "CurrentState": {
                "Code": 48,
                "Name": "terminated"
            },
            "PreviousState": {
                "Code": 80,
                "Name": "stopped"
            }
        }
    ]
}
```

## Test SSH DMZ Access
```bash
ssh devopsteam04@52.59.181.213 \
-i KEY-I346-DMZ-DEVOPSTEAM04.pem
```

```
[OUTPUT]

The authenticity of host '52.59.181.213 (52.59.181.213)' can't be established.
ED25519 key fingerprint is SHA256:WuBrwzur3OxFeol6sLW9avIhbS/ET8W1TIIjeUMKFVE.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '52.59.181.213' (ED25519) to the list of known hosts.
Linux ip-10-0-0-10 6.1.0-31-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.128-1 (2025-02-07) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Mar 18 17:56:12 2025 from 188.155.68.9
devopsteam04@ip-10-0-0-10:~$ exit
logout
Connection to 52.59.181.213 closed.
```

## Test SSH DMZ avec Tunnel Access
```bash
ssh devopsteam04@52.59.181.213 -i KEY-I346-DMZ-DEVOPSTEAM04.pem -L 23:10.0.4.13:22 -L 3399:10.0.4.4:3389
```

```
[OUTPUT]

Linux ip-10-0-0-10 6.1.0-31-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.128-1 (2025-02-07) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Mar 19 11:28:01 2025 from 193.5.240.9
```

## Test EC2 LIN access - INBOUND
* [Source]()
```bash
ssh admin@localhost -p 23 -i KEY-I346-SUB-DEVOPSTEAM04.pem
```

```
[OUTPUT]

 ssh admin@localhost -p 23 -i KEY-I346-SUB-DEVOPSTEAM04.pem
Linux ip-10-0-4-13 6.1.0-23-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.99-1 (2024-07-15) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
```

## Test EC2 WIN access - INBOUND
* [Source]()
```bash
# Récupérer le mot de passe
aws ec2 get-password-data \
--instance-id  i-0bf136248db6b25e8 \
--priv-launch-key KEY-I346-SUB-DEVOPSTEAM04.pem \
--region eu-central-1 \
--profile devopsteam04-i346
```

```
[OUTPUT]
{
    "InstanceId": "i-0bf136248db6b25e8",
    "Timestamp": "2025-03-18T14:33:07+00:00",
    "PasswordData": "C7q8vNv?(1woYH&264JsYgx)P8(1I50H"
}
```

```RDP
#Computer
localhost:3399

#User
administrator
```

## Test EC2 LIN access - OUTBOUND
* [Source]()
```bash
# Ping Google
admin@ip-10-0-4-13:~$ ping 8.8.8.8
```

```
[OUTPUT]

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=57 time=1.74 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=57 time=1.61 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=57 time=1.65 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=57 time=1.46 ms
```

## Test EC2 WIN access - OUTBOUND
* [Source]()
```bash
ping 8.8.8.8
```

```
[OUTPUT]

Pinging 8.8.8.8 with 32 bytes of data:
Reply from 8.8.8.8: bytes=32 time=2ms TTL=57
Reply from 8.8.8.8: bytes=32 time=2ms TTL=57
Reply from 8.8.8.8: bytes=32 time=1ms TTL=57
Reply from 8.8.8.8: bytes=32 time=2ms TTL=57

Ping statistics for 8.8.8.8:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 2ms, Average = 1ms
```

## Clean Subnet/Key/Instance/Security Group
* [Source]()
```bash
 
```

```
[OUTPUT]
```