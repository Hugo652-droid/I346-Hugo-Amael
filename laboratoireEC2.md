## Affichage des élements réseaux
### Lister le VPC
Depuis le site web aws

VPC > Your VPCs > vpc-0a22d771f16ae549d

![image](https://github.com/user-attachments/assets/be4ccc05-0a4f-449c-a4db-3473511d1601)

Depuis le CLI

- [Documentation AWS - Describe VPCs](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-vpcs.html)

Lister les VPC, ec2: Logiciel de virtualisation, region: eu-central-1 et output (sortie sous forme de tableau)
```
aws ec2 describe-vpcs\
  --region eu-central-1\
  --profile DEVOPSTEAM05\
  --output table
```
Outupt:
```
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

### Lister les sous-réseaux

Depuis le site web aws

Lister les subnets :

VPC > Your VPCs > vpc-0a22d771f16ae549d > Subnets

![image](https://github.com/user-attachments/assets/ee1f4c56-797d-46f0-bff0-d08fe89d7d18)

Lister UN subnet en particulier :

VPC > Your VPCs > vpc-0a22d771f16ae549d > Subnets > subnet-092ced6aa04603165 / subnet-10.0.5.0/28

![image](https://github.com/user-attachments/assets/7ec81e66-9ef2-417e-9b81-86e5ff0255c8)

Depuis le CLI

- [AWS Documentation - Describe subnets](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-subnets.html)

Lister les subnets:
```
aws ec2 describe-subnets\
 --region eu-central-1\
 --profile DEVOPSTEAM05 --output table
```
Output:
```
Tableau de tout les sous-réseaux
```

Lister UN subnet en particulier:
```
aws ec2 describe-subnets \
--filters "Name=subnet-id,Values=subnet-092ced6aa04603165" \
--region eu-central-1 \
--profile DEVOPSTEAM05 \
--output table
```

Output:
```
------------------------------------------------------------------------------------------------------------
|                                              DescribeSubnets                                             |
+----------------------------------------------------------------------------------------------------------+
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

```

### Supprimer un subnet

- [Documentation AWS - Supprimer un subnet](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-subnet.html)

Dans le CLI:
```
aws ec2 delete-subnet --subnet-id subnet-092ced6aa04603165
```

Nous n'avons pas pu faire cette action car nous n'avons pas peu faire la commande

## Gestion de la table de routage

### Créer la table de routage

- [Documentation AWS - Créer une table de routage](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route-table.html)

Créer la table de routage depuis le CLI :
```
 aws ec2 create-route-table\
 --vpc-id vpc-0a22d771f16ae549d\
 --profile DEVOPSTEAM05\
 --region eu-central-1\
--output table
```

Output du CLI:
```
-------------------------------------------------------------------------
|                           CreateRouteTable                            |
+------------------+----------------------------------------------------+
|  ClientToken     |  e2ba74b0-0456-4a6f-8f9e-c89704afd0ad              |
+------------------+----------------------------------------------------+
||                             RouteTable                              ||
|+---------------+--------------------------+--------------------------+|
||    OwnerId    |      RouteTableId        |          VpcId           ||
|+---------------+--------------------------+--------------------------+|
||  709024702237 |  rtb-09eea99d8ac647a5f   |  vpc-0a22d771f16ae549d   ||
|+---------------+--------------------------+--------------------------+|
|||                              Routes                               |||
||+-----------------------+------------+--------------------+---------+||
||| DestinationCidrBlock  | GatewayId  |      Origin        |  State  |||
||+-----------------------+------------+--------------------+---------+||
|||  10.0.0.0/16          |  local     |  CreateRouteTable  |  active |||
||+-----------------------+------------+--------------------+---------+||

```

Output de l'interface grafique :

![image](<Image/Capture d'ecrant IG AWS ec2 creat route table .png>)

### Supprimer la table de routage

- [Documentation AWS - supprimer une table de routage](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-route-table.html)

Suprimmer la route table depuis le CLI:
```
aws ec2 delete-route-table \
	--route-table-id rtb-028cd789bcaf18038 \
	--profile DEVOPSTEAM05 \
	--region eu-central-1
```

Output du CLI:

Aucun output

Output de l'interface grafique :

![image](<Image/Capture_decrant_IG_AWS_ec2_delete_route_table .png>)

### Afficher la table de routage

- [Documentation AWS - afficher une table de routage](https://awscli.amazonaws.com/v2/documentation/api/2.0.33/reference/ec2/describe-route-tables.html)

Afficher une table de routage :
```
aws ec2 describe-route-tables \
    --profile DEVOPSTEAM05 \
    --region eu-central-1 \
    --route-table-ids rtb-09eea99d8ac647a5f \
    --output table
```

Output du CLI :
```
---------------------------------------------------------------
|                     DescribeRouteTables                     |
+-------------------------------------------------------------+
||                        RouteTables                        ||
|+----------------------+------------------------------------+|
||  OwnerId             |  709024702237                      ||
||  RouteTableId        |  rtb-09eea99d8ac647a5f             ||
||  VpcId               |  vpc-0a22d771f16ae549d             ||
|+----------------------+------------------------------------+|
|||                      Associations                       |||
||+--------------------------+------------------------------+||
|||  Main                    |  False                       |||
|||  RouteTableAssociationId |  rtbassoc-067eb31bcc2d1a3cc  |||
|||  RouteTableId            |  rtb-09eea99d8ac647a5f       |||
|||  SubnetId                |  subnet-092ced6aa04603165    |||
||+--------------------------+------------------------------+||
||||                   AssociationState                    ||||
|||+--------------------+----------------------------------+|||
||||  State             |  associated                      ||||
|||+--------------------+----------------------------------+|||
|||                         Routes                          |||
||+------------------------------+--------------------------+||
|||  DestinationCidrBlock        |  10.0.0.0/16             |||
|||  GatewayId                   |  local                   |||
|||  Origin                      |  CreateRouteTable        |||
|||  State                       |  active                  |||
||+------------------------------+--------------------------+||
```

### Créer le tag d'un composant
- [Documentation AWS - Créer un tag](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-tags.html)

Créer le tag de la route table :

```
aws ec2 create-tags\
     --resources rtb-09eea99d8ac647a5f\
     --tags Key=Name,Value=private-rte-table-devopsteam05\
     --profile DEVOPSTEAM05\
     --region eu-central-1
```
Output depuis le CLI :

Pas d'ouput

Output depuis l'interface graphique :
![image](https://github.com/user-attachments/assets/0ac58ae4-dd97-4bde-8625-fa6aa1770b22)


### Associer la table

- [Documentation AWS - Associer la table de routage](https://docs.aws.amazon.com/cli/latest/reference/ec2/associate-route-table.html)

Associer depuis le CLI:

```
aws ec2 associate-route-table\
 --route-table-id rtb-09eea99d8ac647a5f\
 --subnet-id subnet-092ced6aa04603165\
 --region eu-central-1\
 --profile DEVOPSTEAM05\
--output table
```

Output depuis CLI:

```
-------------------------------------------------
|              AssociateRouteTable              |
+----------------+------------------------------+
|  AssociationId |  rtbassoc-067eb31bcc2d1a3cc  |
+----------------+------------------------------+
||              AssociationState               ||
|+----------------+----------------------------+|
||  State         |  associated                ||
|+----------------+----------------------------+|

```

Output depuis l'interface graphique :

![image](https://github.com/user-attachments/assets/49c474f9-b322-473b-99d5-160226c3753f)

### Dissocier la table

- [Documentation AWS - Dissocier la table de routage](https://docs.aws.amazon.com/cli/latest/reference/ec2/disassociate-route-table.html)

Dissocier depuis le CLI
```
aws ec2 disassociate-route-table\
 --association-id rtb-09eea99d8ac647a5f\
 --region eu-central-1\
 --profile DEVOPSTEAM05\
 --output table
```

Output depuis le CLI

Pas de droits pour faire cette action

### Créer des routes

- [Documentation AWS - Créer des routes](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

Créer depuis le CLI

```
aws ec2 create-route \
    --route-table-id rtb-09eea99d8ac647a5f \
    --destination-cidr-block 0.0.0.0/0 \
    --instance-id i-09d3919ca6d27ab6b \
    --region eu-central-1 \
    --profile DEVOPSTEAM05\
    --output table
```

Output depuis le CLI

```
--------------------
|    CreateRoute   |
+---------+--------+
|  Return |  True  |
+---------+--------+
```

### Supprimer une routes

- [Documentation AWS - supprimer une route ](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-route.html#examples)

Créer depuis le CLI:

```
aws ec2 delete-route\
 --route-table-id rtb-22574640\
 --destination-cidr-block 0.0.0.0/0\
 --region eu-central-1\
 --profile DEVOPSTEAM05
```

Output depuis le CLI

Pas de droits pour faire cette action

## Gestion des instances

### Créer une instance

- [Documentation AWS - Créer une instance](https://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html)

Créer depuis le CLI (LIN)
```
aws ec2 run-instances \
    --image-id ami-0584590e5f0e97daa \
    --instance-type t2.micro \
    --key-name KEY-I346-SUB-DEVOPSTEAM05 \
    --subnet-id subnet-092ced6aa04603165 \
    --security-group-ids sg-0ae65e1e8f9697e4a \
    --private-ip-address 10.0.5.10 \
    --region eu-central-1 \
    --profile DEVOPSTEAM05 \
    --output table
```

Output :

```
-----------------------------------------------------------------------------
|                               RunInstances                                |
+-------------------------------+-------------------------------------------+
|  OwnerId                      |  709024702237                             |
|  ReservationId                |  r-0986257ab3881bbe7                      |
+-------------------------------+-------------------------------------------+
||                                Instances                                ||
|+--------------------------+----------------------------------------------+|
||  AmiLaunchIndex          |  0                                           ||
||  Architecture            |  x86_64                                      ||
||  ClientToken             |  ca195c05-8f7d-450f-a4b0-d47757317624        ||
||  CurrentInstanceBootMode |  legacy-bios                                 ||
||  EbsOptimized            |  False                                       ||
||  EnaSupport              |  True                                        ||
||  Hypervisor              |  xen                                         ||
||  ImageId                 |  ami-0584590e5f0e97daa                       ||
||  InstanceId              |  i-0100024ec0080e056                         ||
||  InstanceType            |  t2.micro                                    ||
||  KeyName                 |  KEY-I346-SUB-DEVOPSTEAM05                   ||
||  LaunchTime              |  2025-03-18T14:33:02+00:00                   ||
||  PrivateDnsName          |  ip-10-0-5-10.eu-central-1.compute.internal  ||
||  PrivateIpAddress        |  10.0.5.10                                   ||
||  PublicDnsName           |                                              ||
||  RootDeviceName          |  /dev/xvda                                   ||
||  RootDeviceType          |  ebs                                         ||
||  SourceDestCheck         |  True                                        ||
||  StateTransitionReason   |                                              ||
||  SubnetId                |  subnet-092ced6aa04603165                    ||
||  VirtualizationType      |  hvm                                         ||
||  VpcId                   |  vpc-0a22d771f16ae549d                       ||
|+--------------------------+----------------------------------------------+|
|||                   CapacityReservationSpecification                    |||
||+---------------------------------------------------------+-------------+||
|||  CapacityReservationPreference                          |  open       |||
||+---------------------------------------------------------+-------------+||
|||                              CpuOptions                               |||
||+-------------------------------------------------------+---------------+||
|||  CoreCount                                            |  1            |||
|||  ThreadsPerCore                                       |  1            |||
||+-------------------------------------------------------+---------------+||
|||                            EnclaveOptions                             |||
||+--------------------------------------+--------------------------------+||
|||  Enabled                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                          MaintenanceOptions                           |||
||+-----------------------------------------+-----------------------------+||
|||  AutoRecovery                           |  default                    |||
||+-----------------------------------------+-----------------------------+||
|||                            MetadataOptions                            |||
||+-------------------------------------------------+---------------------+||
|||  HttpEndpoint                                   |  enabled            |||
|||  HttpProtocolIpv6                               |  disabled           |||
|||  HttpPutResponseHopLimit                        |  1                  |||
|||  HttpTokens                                     |  optional           |||
|||  InstanceMetadataTags                           |  disabled           |||
|||  State                                          |  pending            |||
||+-------------------------------------------------+---------------------+||
|||                              Monitoring                               |||
||+-----------------------------+-----------------------------------------+||
|||  State                      |  disabled                               |||
||+-----------------------------+-----------------------------------------+||
|||                           NetworkInterfaces                           |||
||+------------------------------+----------------------------------------+||
|||  Description                 |                                        |||
|||  InterfaceType               |  interface                             |||
|||  MacAddress                  |  0a:40:a8:8d:d5:9b                     |||
|||  NetworkInterfaceId          |  eni-05882bcfd22aecbe1                 |||
|||  OwnerId                     |  709024702237                          |||
|||  PrivateIpAddress            |  10.0.5.10                             |||
|||  SourceDestCheck             |  True                                  |||
|||  Status                      |  in-use                                |||
|||  SubnetId                    |  subnet-092ced6aa04603165              |||
|||  VpcId                       |  vpc-0a22d771f16ae549d                 |||
||+------------------------------+----------------------------------------+||
||||                             Attachment                              ||||
|||+----------------------------+----------------------------------------+|||
||||  AttachTime                |  2025-03-18T14:33:02+00:00             ||||
||||  AttachmentId              |  eni-attach-06a534ea00202d9f6          ||||
||||  DeleteOnTermination       |  True                                  ||||
||||  DeviceIndex               |  0                                     ||||
||||  NetworkCardIndex          |  0                                     ||||
||||  Status                    |  attaching                             ||||
|||+----------------------------+----------------------------------------+|||
||||                               Groups                                ||||
|||+-----------------------+---------------------------------------------+|||
||||  GroupId              |  sg-0ae65e1e8f9697e4a                       ||||
||||  GroupName            |  sg private subnet05                        ||||
|||+-----------------------+---------------------------------------------+|||
||||                              Operator                               ||||
|||+-------------------------------------+-------------------------------+|||
||||  Managed                            |  False                        ||||
|||+-------------------------------------+-------------------------------+|||
||||                         PrivateIpAddresses                          ||||
|||+-----------------------------------------+---------------------------+|||
||||  Primary                                |  True                     ||||
||||  PrivateIpAddress                       |  10.0.5.10                ||||
|||+-----------------------------------------+---------------------------+|||
|||                               Operator                                |||
||+--------------------------------------+--------------------------------+||
|||  Managed                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                               Placement                               |||
||+-------------------------------------+---------------------------------+||
|||  AvailabilityZone                   |  eu-central-1c                  |||
|||  GroupName                          |                                 |||
|||  Tenancy                            |  default                        |||
||+-------------------------------------+---------------------------------+||
|||                         PrivateDnsNameOptions                         |||
||+------------------------------------------------------+----------------+||
|||  EnableResourceNameDnsAAAARecord                     |  False         |||
|||  EnableResourceNameDnsARecord                        |  False         |||
|||  HostnameType                                        |  ip-name       |||
||+------------------------------------------------------+----------------+||
|||                            SecurityGroups                             |||
||+------------------------+----------------------------------------------+||
|||  GroupId               |  sg-0ae65e1e8f9697e4a                        |||
|||  GroupName             |  sg private subnet05                         |||
||+------------------------+----------------------------------------------+||
|||                                 State                                 |||
||+-----------------------------+-----------------------------------------+||
|||  Code                       |  0                                      |||
|||  Name                       |  pending                                |||
||+-----------------------------+-----------------------------------------+||
|||                              StateReason                              |||
||+----------------------------------+------------------------------------+||
|||  Code                            |  pending                           |||
|||  Message                         |  pending                           |||
||+----------------------------------+------------------------------------+||
```

Créer depuis le CLI (WIN)
```
aws ec2 run-instances \
    --image-id ami-045114d716addc65d \
    --instance-type t3.micro \
    --key-name KEY-I346-SUB-DEVOPSTEAM05 \
    --subnet-id subnet-092ced6aa04603165 \
    --security-group-ids sg-0ae65e1e8f9697e4a \
    --private-ip-address 10.0.5.11 \
    --region eu-central-1 \
    --profile DEVOPSTEAM05 \
    --output table
```

Output :
```
-----------------------------------------------------------------------------
|                               RunInstances                                |
+-------------------------------+-------------------------------------------+
|  OwnerId                      |  709024702237                             |
|  ReservationId                |  r-0f9762bfe23f4b6fb                      |
+-------------------------------+-------------------------------------------+
||                                Instances                                ||
|+--------------------------+----------------------------------------------+|
||  AmiLaunchIndex          |  0                                           ||
||  Architecture            |  x86_64                                      ||
||  BootMode                |  uefi                                        ||
||  ClientToken             |  99d1aa9f-ac11-4dc9-84e0-70fab4812041        ||
||  CurrentInstanceBootMode |  uefi                                        ||
||  EbsOptimized            |  False                                       ||
||  EnaSupport              |  True                                        ||
||  Hypervisor              |  xen                                         ||
||  ImageId                 |  ami-045114d716addc65d                       ||
||  InstanceId              |  i-005ef53567c5833dd                         ||
||  InstanceType            |  t3.micro                                    ||
||  KeyName                 |  KEY-I346-SUB-DEVOPSTEAM05                   ||
||  LaunchTime              |  2025-03-18T14:43:41+00:00                   ||
||  Platform                |  windows                                     ||
||  PrivateDnsName          |  ip-10-0-5-11.eu-central-1.compute.internal  ||
||  PrivateIpAddress        |  10.0.5.11                                   ||
||  PublicDnsName           |                                              ||
||  RootDeviceName          |  /dev/sda1                                   ||
||  RootDeviceType          |  ebs                                         ||
||  SourceDestCheck         |  True                                        ||
||  StateTransitionReason   |                                              ||
||  SubnetId                |  subnet-092ced6aa04603165                    ||
||  VirtualizationType      |  hvm                                         ||
||  VpcId                   |  vpc-0a22d771f16ae549d                       ||
|+--------------------------+----------------------------------------------+|
|||                   CapacityReservationSpecification                    |||
||+---------------------------------------------------------+-------------+||
|||  CapacityReservationPreference                          |  open       |||
||+---------------------------------------------------------+-------------+||
|||                              CpuOptions                               |||
||+-------------------------------------------------------+---------------+||
|||  CoreCount                                            |  1            |||
|||  ThreadsPerCore                                       |  2            |||
||+-------------------------------------------------------+---------------+||
|||                            EnclaveOptions                             |||
||+--------------------------------------+--------------------------------+||
|||  Enabled                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                          MaintenanceOptions                           |||
||+-----------------------------------------+-----------------------------+||
|||  AutoRecovery                           |  default                    |||
||+-----------------------------------------+-----------------------------+||
|||                            MetadataOptions                            |||
||+-------------------------------------------------+---------------------+||
|||  HttpEndpoint                                   |  enabled            |||
|||  HttpProtocolIpv6                               |  disabled           |||
|||  HttpPutResponseHopLimit                        |  2                  |||
|||  HttpTokens                                     |  required           |||
|||  InstanceMetadataTags                           |  disabled           |||
|||  State                                          |  pending            |||
||+-------------------------------------------------+---------------------+||
|||                              Monitoring                               |||
||+-----------------------------+-----------------------------------------+||
|||  State                      |  disabled                               |||
||+-----------------------------+-----------------------------------------+||
|||                           NetworkInterfaces                           |||
||+------------------------------+----------------------------------------+||
|||  Description                 |                                        |||
|||  InterfaceType               |  interface                             |||
|||  MacAddress                  |  0a:ac:19:8e:be:81                     |||
|||  NetworkInterfaceId          |  eni-018f143e6a3af428b                 |||
|||  OwnerId                     |  709024702237                          |||
|||  PrivateIpAddress            |  10.0.5.11                             |||
|||  SourceDestCheck             |  True                                  |||
|||  Status                      |  in-use                                |||
|||  SubnetId                    |  subnet-092ced6aa04603165              |||
|||  VpcId                       |  vpc-0a22d771f16ae549d                 |||
||+------------------------------+----------------------------------------+||
||||                             Attachment                              ||||
|||+----------------------------+----------------------------------------+|||
||||  AttachTime                |  2025-03-18T14:43:41+00:00             ||||
||||  AttachmentId              |  eni-attach-0abe45eead32976d9          ||||
||||  DeleteOnTermination       |  True                                  ||||
||||  DeviceIndex               |  0                                     ||||
||||  NetworkCardIndex          |  0                                     ||||
||||  Status                    |  attaching                             ||||
|||+----------------------------+----------------------------------------+|||
||||                               Groups                                ||||
|||+-----------------------+---------------------------------------------+|||
||||  GroupId              |  sg-0ae65e1e8f9697e4a                       ||||
||||  GroupName            |  sg private subnet05                        ||||
|||+-----------------------+---------------------------------------------+|||
||||                              Operator                               ||||
|||+-------------------------------------+-------------------------------+|||
||||  Managed                            |  False                        ||||
|||+-------------------------------------+-------------------------------+|||
||||                         PrivateIpAddresses                          ||||
|||+-----------------------------------------+---------------------------+|||
||||  Primary                                |  True                     ||||
||||  PrivateIpAddress                       |  10.0.5.11                ||||
|||+-----------------------------------------+---------------------------+|||
|||                               Operator                                |||
||+--------------------------------------+--------------------------------+||
|||  Managed                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                               Placement                               |||
||+-------------------------------------+---------------------------------+||
|||  AvailabilityZone                   |  eu-central-1c                  |||
|||  GroupName                          |                                 |||
|||  Tenancy                            |  default                        |||
||+-------------------------------------+---------------------------------+||
|||                         PrivateDnsNameOptions                         |||
||+------------------------------------------------------+----------------+||
|||  EnableResourceNameDnsAAAARecord                     |  False         |||
|||  EnableResourceNameDnsARecord                        |  False         |||
|||  HostnameType                                        |  ip-name       |||
||+------------------------------------------------------+----------------+||
|||                            SecurityGroups                             |||
||+------------------------+----------------------------------------------+||
|||  GroupId               |  sg-0ae65e1e8f9697e4a                        |||
|||  GroupName             |  sg private subnet05                         |||
||+------------------------+----------------------------------------------+||
|||                                 State                                 |||
||+-----------------------------+-----------------------------------------+||
|||  Code                       |  0                                      |||
|||  Name                       |  pending                                |||
||+-----------------------------+-----------------------------------------+||
|||                              StateReason                              |||
||+----------------------------------+------------------------------------+||
|||  Code                            |  pending                           |||
|||  Message                         |  pending                           |||
||+----------------------------------+------------------------------------+||
```
### Démarer une instance

Dans le CLI :
```
aws ec2 start-instances \
  --instance-ids i-005ef53567c5833dd \
  --profile DEVOPSTEAM05\
  --region eu-central-1
```

Output :
```
{
    "StartingInstances": [
        {
            "InstanceId": "i-005ef53567c5833dd",
            "CurrentState": {
                "Code": 0,
                "Name": "pending"
            },
            "PreviousState": {
                "Code": 80,
                "Name": "stopped"
            }
        }
    ]
}

```


### Arrêter une instance

- [Documentation AWS - Arrêter l'instance ](https://docs.aws.amazon.com/cli/latest/reference/ec2/stop-instances.html)

Arrêter depuis le CLI

```
aws ec2 stop-instances\
 --instance-ids i-005ef53567c5833dd
```

Output :
```
{
    "StoppingInstances": [
        {
            "InstanceId": "i-0ae1c1cf339881b06",
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
```

### Supprimer une instance

- [Documentation AWS - Arrêter l'instance ](https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html#examples)

Supprimer depuis le CLI

```
aws ec2 terminate-instances\
 --instance-ids i-1234567890abcdef0
```

Output :
```
{
    "TerminatingInstances": [
        {
            "InstanceId": "i-0ae1c1cf339881b06",
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

### Se connecter à une instance

- [Documentation AWS - Se connecter à une instance ](https://docs.aws.amazon.com/fr_fr/AWSEC2/latest/UserGuide/connect-using-eice.html)

Se connecter depuis le CLI

```
aws ec2-instance-connect open-tunnel \
    --instance-id i-0123456789example \
    --local-port 22
```

### Créer une "clé privée"

- [Documentation AWS - Créer une clé privée](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-key-pairs.html#examples)

Créer depuis le CLI

```
aws ec2 create-key-pair \
    --key-name KEY-I346-SUB-DEVOPSTEAM05 \
    --key-type rsa \
    --key-format pem \
    --profile DEVOPSTEAM05\
    --region eu-central-1\
    --output text > KEY-I346-SUB-DEVOPSTEAM05.pem
```

Output depuis le CLI

```
{
    "KeyPairId": "key-010ea06f85485f342",
    "KeyName": "cli-lin-subnet05",
    "KeyFingerprint": "b0:96:25:91:77:25:f7:7d:62:45:a8:5b:d9:c7:7b:fb:d6:19:74:2d",
    "KeyMaterial": "***"
}


```

Output depuis l'interface graphique

Pas de droit pour executer cette action

### Lister les "clé privées"

Lister depuis le CLI

[Documentation AWS - Lister les clés privées](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-key-pairs.html#examples)

```
aws ec2 describe-key-pairs \
    --profile DEVOPSTEAM05\
    --region eu-central-1\
    --output table
```

Output depuis le CLI

```
-------------------------------------------------------------------------------------
|                                 DescribeKeyPairs                                  |
+-----------------------------------------------------------------------------------+
||                                    KeyPairs                                     ||
|+---------------------+-----------------------------------------------------------+|
||  CreateTime         |  2025-01-06T11:11:00.356000+00:00                         ||
||  KeyFingerprint     |  mt8E8FXEMjnzRimOS1yAByqPel8LjzS3z9invTYnsZ0=             ||
||  KeyName            |  KEY_LIN3_DMZ_ADMIN                                       ||
||  KeyPairId          |  key-0825c3d7672314580                                    ||
||  KeyType            |  ed25519                                                  ||
|+---------------------+-----------------------------------------------------------+|
||                                    KeyPairs                                     ||
|+----------------+----------------------------------------------------------------+|
||  CreateTime    |  2025-03-12T11:11:49.197000+00:00                              ||
||  KeyFingerprint|  b0:96:25:91:77:25:f7:7d:62:45:a8:5b:d9:c7:7b:fb:d6:19:74:2d   ||
||  KeyName       |  cli-lin-subnet05                                              ||
||  KeyPairId     |  key-010ea06f85485f342                                         ||
||  KeyType       |  rsa                                                           ||
|+----------------+----------------------------------------------------------------+|
||                                    KeyPairs                                     ||
|+----------------+----------------------------------------------------------------+|
||  CreateTime    |  2025-03-12T08:54:33.080000+00:00                              ||
||  KeyFingerprint|  2f:5d:b3:bd:91:79:57:39:c9:2e:db:95:7c:9f:df:56:aa:c2:17:78   ||
||  KeyName       |  KEY-I346-SUB-DEVOPSTEAM99                                     ||
||  KeyPairId     |  key-081406c49f522c35f                                         ||
||  KeyType       |  rsa                                                           ||
|+----------------+----------------------------------------------------------------+|
|||                                     Tags                                      |||
||+-----------------+-------------------------------------------------------------+||
|||  Key            |  Name                                                       |||
|||  Value          |  KEY-I346-SUB-DEVOPSTEAM99                                  |||
||+-----------------+-------------------------------------------------------------+||
||                                    KeyPairs                                     ||
|+----------------+----------------------------------------------------------------+|
||  CreateTime    |  2025-03-12T10:10:37.188000+00:00                              ||
||  KeyFingerprint|  f1:0c:01:30:21:57:f9:7f:eb:90:fa:4a:86:c7:c9:5f:bd:cd:98:8d   ||
||  KeyName       |  test                                                          ||
||  KeyPairId     |  key-0e2e524e32e94bc19                                         ||
||  KeyType       |  rsa                                                           ||
|+----------------+----------------------------------------------------------------+|

```

### Supprimer une "clé privée"

- [Documenation AWS - Supprimer une clé privée](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-key-pair.html#examples)

Supprimer depuis le CLI

```
aws ec2 delete-key-pair \
    --key-name KEY-I346-SUB-DEVOPSTEAM05\
     --profile DEVOPSTEAM05\
     --region eu-central-1
```

Output depuis le CLI

Pas de droits pour exécuter cette action

## Gestion des groupes de sécurité

### Créer un groupe de sécurité

- [Documentation AWS - Créer un groupe de sécurité](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-security-group.html#examples)

Créer depuis le CLI

```
aws ec2 create-security-group\
 --group-name "sg private subnet05"\
 --description "Security groupe for the Subnet05"\
 --vpc-id vpc-0a22d771f16ae549d\
 --profile DEVOPSTEAM05\
 --region eu-central-1\
 --output table
```

Output depuis le CLI

```
---------------------------------------------------------------------------------------------------
|                                       CreateSecurityGroup                                       |
+------------------+------------------------------------------------------------------------------+
|  GroupId         |  sg-0ae65e1e8f9697e4a                                                        |
|  SecurityGroupArn|  arn:aws:ec2:eu-central-1:709024702237:security-group/sg-0ae65e1e8f9697e4a   |
+------------------+------------------------------------------------------------------------------+
```

Output depuis le site Web

![image](https://github.com/user-attachments/assets/fd624824-a0cb-4d2a-8b79-4c4ddc7f51ef)

### Supprimer un groupe de sécurité

- [Documentation AWS - Supprimer un groupe de sécurité](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-security-group.html#examples)

Supprimer depuis le CLI

```
aws ec2 delete-security-group\
--group-name "sg private subnet05"\
--profile DEVOPSTEAM05\
--region eu-central-1
```

Output depuis le CLI 

Pas de droits pour faire cette action

## Autorisier un group de securité 

- [Documentation AWS - Créer un groupe de sécurité](https://docs.aws.amazon.com/cli/latest/reference/ec2/authorize-security-group-ingress.html)

### Pour linux

Dans le CLI :
```
aws ec2 authorize-security-group-ingress \
    --group-id sg-0ae65e1e8f9697e4a \
    --ip-permissions "IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges=[{CidrIp=10.0.0.0/28,Description=SSH-FROM-DMZ}]" \
    --region eu-central-1 \
    --profile DEVOPSTEAM05\
    --output table
```

Output :
```
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
||  GroupId             |  sg-0ae65e1e8f9697e4a                                                              ||
||  GroupOwnerId        |  709024702237                                                                      ||
||  IpProtocol          |  tcp                                                                               ||
||  IsEgress            |  False                                                                             ||
||  SecurityGroupRuleArn|  arn:aws:ec2:eu-central-1:709024702237:security-group-rule/sgr-06292a071aff7a886   ||
||  SecurityGroupRuleId |  sgr-06292a071aff7a886                                                             ||
||  ToPort              |  22                                                                                ||
|+----------------------+------------------------------------------------------------------------------------+|
```

### Pour Windows

Dans le CLI :
```
aws ec2 authorize-security-group-ingress \
    --group-id sg-0ae65e1e8f9697e4a \
    --ip-permissions "IpProtocol=tcp,FromPort=3389,ToPort=3389,IpRanges=[{CidrIp=10.0.0.0/28,Description=RDP-FROM-DMZ}]" \
    --region eu-central-1 \
    --profile DEVOPSTEAM05\
    --output table
```

Output :
```
---------------------------------------------------------------------------------------------------------------
|                                        AuthorizeSecurityGroupIngress                                        |
+------------------------------------------------------------+------------------------------------------------+
|  Return                                                    |  True                                          |
+------------------------------------------------------------+------------------------------------------------+
||                                            SecurityGroupRules                                             ||
|+----------------------+------------------------------------------------------------------------------------+|
||  CidrIpv4            |  10.0.0.0/28                                                                       ||
||  Description         |  RDP-FROM-DMZ                                                                      ||
||  FromPort            |  3389                                                                              ||
||  GroupId             |  sg-0ae65e1e8f9697e4a                                                              ||
||  GroupOwnerId        |  709024702237                                                                      ||
||  IpProtocol          |  tcp                                                                               ||
||  IsEgress            |  False                                                                             ||
||  SecurityGroupRuleArn|  arn:aws:ec2:eu-central-1:709024702237:security-group-rule/sgr-01a664c41e3b0d266   ||
||  SecurityGroupRuleId |  sgr-01a664c41e3b0d266                                                             ||
||  ToPort              |  3389                                                                              ||
|+----------------------+------------------------------------------------------------------------------------+|
```

## Connection aux instances

- [Documentation du cours](https://github.com/CPNV-CFC-I346-CLOUD/DEVOPSTEAM99-LABO-SOLUTION/blob/main/EC2/accesses.md)

- [Documentation AWS]()

### se connecter à la DMZ

depuis le CLI

```
 ssh devopsteam05@52.59.181.213 -i KEY-I346-DMZ-DEVOPSTEAM05.pem
```

output (demande si l'on veut s'y connecter que à la première connection, logout à l'aide du mot clé "exit")
```
Linux ip-10-0-0-10 6.1.0-31-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.128-1 (2025-02-07) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Mar 19 11:28:14 2025 from 193.5.240.9
devopsteam05@ip-10-0-0-10:~$ exit
logout
Connection to 52.59.181.213 closed.

```

### Création des tounels

depuis le CLI

```
ssh devopsteam05@52.59.181.213 \
    -i KEY-I346-DMZ-DEVOPSTEAM05.pem \
    -L 23:10.0.5.10:22 \
    -L 3399:10.0.5.11:3389
```

output (demande si l'on veut s'y connecter que à la première connection, logout à l'aide du mot clé "exit")
```
Linux ip-10-0-0-10 6.1.0-31-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.128-1 (2025-02-07) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Mar 19 11:30:52 2025 from 193.5.240.9
devopsteam05@ip-10-0-0-10:~$ ssh admin@localhost   -p 23   -i KEY-I346-SUB-DEVOPSTEAM05.pem
Warning: Identity file KEY-I346-SUB-DEVOPSTEAM05.pem not accessible: No such file or directory.
ssh: connect to host localhost port 23: Connection refused
devopsteam05@ip-10-0-0-10:~$
```

### se connecter à la machine linux

depuis le CLI

```
ssh admin@localhost\
   -p 23\
   -i KEY-I346-SUB-DEVOPSTEAM05.pem
```

output (demande si l'on veut s'y connecter que à la première connection, logout à l'aide du mot clé "exit")
```
Linux ip-10-0-5-10 6.1.0-23-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.99-1 (2024-07-15) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
admin@ip-10-0-5-10:~$
```

### Test de connection à google

depuis le CLI

```
ping 8.8.8.8
```

output (demande si l'on veut s'y connecter que à la première connection, logout à l'aide du mot clé "exit")
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=57 time=2.40 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=57 time=2.28 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=57 time=1.77 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=57 time=2.05 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=57 time=1.85 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=57 time=1.68 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=57 time=1.43 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=57 time=2.97 ms
```

### Se connecter à la machine windows

depuis le CLI (obtention du mdp)

```
$ aws ec2 get-password-data\
  --instance-id  i-005ef53567c5833dd\
  --priv-launch-key KEY-I346-SUB-DEVOPSTEAM05.pem\
  --region eu-central-1\
  --profile DEVOPSTEAM05

```

output
```
{
    "InstanceId": "i-005ef53567c5833dd",
    "Timestamp": "2025-03-18T14:52:00+00:00",
    "PasswordData": "***"
}

```

connexion (machine: localhost:3399, utilisateur: administrator)

![image](https://github.com/user-attachments/assets/8e392994-0279-4b8f-87f0-ad1dfed209a3)


