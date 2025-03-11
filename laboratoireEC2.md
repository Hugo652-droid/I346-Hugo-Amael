## Lister le VPC 
### Depuis le site web aws

VPC > Your VPCs > vpc-0a22d771f16ae549d

![image](https://github.com/user-attachments/assets/be4ccc05-0a4f-449c-a4db-3473511d1601)

### Depuis le CLI

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

## Lister les sous-réseaux

### Depuis le site web aws

Lister les subnets :

VPC > Your VPCs > vpc-0a22d771f16ae549d > Subnets

![image](https://github.com/user-attachments/assets/ee1f4c56-797d-46f0-bff0-d08fe89d7d18)

Lister UN subnet en particulier :

VPC > Your VPCs > vpc-0a22d771f16ae549d > Subnets > subnet-092ced6aa04603165 / subnet-10.0.5.0/28

![image](https://github.com/user-attachments/assets/7ec81e66-9ef2-417e-9b81-86e5ff0255c8)

### Depuis le CLI

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
$ aws ec2 describe-subnets \
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

### Associer la table

- [Documentation AWS - Associer la table de routage](https://docs.aws.amazon.com/cli/latest/reference/ec2/associate-route-table.html)

Associer depuis le CLI:

```
$ aws ec2 associate-route-table\
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
$ aws ec2 disassociate-route-table\
 --association-id rtb-09eea99d8ac647a5f\
 --region eu-central-1\
 --profile DEVOPSTEAM05\
 --output table
```

Output depuis le CLI

Pas de droits pour faire cette action, voici donc le message d'erreur
```
An error occurred (UnauthorizedOperation) when calling the DisassociateRouteTable operation: You are not authorized to perform this operation. User: arn:aws:iam::709024702237:user/devopsteam05-i346 is not authorized to perform: ec2:DisassociateRouteTable on resource: arn:aws:ec2:eu-central-1:709024702237:*/* because no identity-based policy allows the ec2:DisassociateRouteTable action. Encoded authorization failure message: _jcP-nx6SWAGhDmerAMc-shVPOmXQXwPPwJhtZOvvaQmGUuMzx-sQ2vdg_roUQNYPBsqGlnucOfF_KkddpNAlwEIP4XTgh1KVmdPVDlXH4mz-zHVeJihSJD7tGJxu60-TMs87KcSfNLpPVY8G7uvpoTDiEQC6dt1niiOKHf3CVR830U2768OEABP5Z7lF9dp-ore7iVTSSOrgCgf1nZgdM89nExnfUY_5Hw1zhyiYmMTNOe6AhMCBwUo1Ka6_rvwxXfYZ2E75B2NKdlZeh2NXvcroJgDNfBux--uig9W1Djjp9oh5JlqrhB2I9Q03CY6d2HA97ERYH79-SYNcKlMeuS3Q4QK5KcqdNF-fM0L8-W26d9DEKVMkKSlDlFKTJSwY1GFeoVeduxoksD8wTQ2eA80hBE8DPL0hMpO5BX_ujebpfnyQClz2BGwLWbrHYBjCNUcGduNSXOhrKOlXxBY8eFXrJwypea-Rx-BLCXhG_SdW448HJQLsDUN2GRvE4bPmCfOfaiio_5L1Kc
```

### Créer des routes

- [Documentation AWS - Créer des routes](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)


