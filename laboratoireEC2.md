## Lister le VPC 
### Depuis le site web aws

VPC > Your VPCs > vpc-0a22d771f16ae549d

![image](https://github.com/user-attachments/assets/be4ccc05-0a4f-449c-a4db-3473511d1601)

### Depuis le CLI

- [Documentation AWS](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-vpcs.html)

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

Lister les subnets:
```
aws ec2 describe-subnets --region eu-central-1 --profile DEVOPSTEAM05 --output table
```
Output:
Tableau de tout les sous-réseaux

Lister UN sous-réseau en particulier:


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
![alt text](image/Capture%20d'ecrant%20IG%20AWS%20ec2%20creat%20route%20table%20.png)

- [Documentation AWS supprimer une table de routage] (https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-route-table.html)

Pour suprimmer la route table
```
aws ec2 delete-route-table \
	--route-table-id rtb-028cd789bcaf18038 \
	--profile DEVOPSTEAM05 \
	--region eu-central-1
```

Output du CLI:
``````

Output de l'interface grafique :
![alt text](image/Capture_decrant_IG_AWS_ec2_delete_route_table%20.png)