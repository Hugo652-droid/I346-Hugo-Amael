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


## Créer la table de routage

- [Documentation AWS Créer une table de routage] (https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route-table.html)

Créer la table de routage :
```
 aws ec2 create-route-table --vpc-id vpc-0a22d771f16ae549d --profile DEVOPSTEAM05 --region eu-central-1
```

Output du CLI:
```
{
    "RouteTable": {
        "Associations": [],
        "PropagatingVgws": [],
        "RouteTableId": "rtb-028cd789bcaf18038",
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
    "ClientToken": "575fae50-7c3b-44ca-b651-aa487d17c588"
}
```

Output de l'interface grafique :
![image](<Image/Capture d'ecrant IG AWS ec2 creat route table .png>)

- [Documentation AWS supprimer une table de routage] (https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-route-table.html)

Pour suprimmer la route table
```
aws ec2 delete-route-table \
	--route-table-id rtb-028cd789bcaf18038 \
	--profile DEVOPSTEAM05 \
	--region eu-central-1
```

Output du CLI:

Output de l'interface grafique :
![image](<Image/Capture_decrant_IG_AWS_ec2_delete_route_table .png>)