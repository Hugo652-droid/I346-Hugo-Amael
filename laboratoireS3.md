# Laboratoire S3

## Installation et configuration du CLI

* [Installer le client git](https://git-scm.com/)
  * Git bash vous embarque de nombreuses commandes Linux utiles pour s'entrainer avec S3 (cat, grep, touch, ls)
* [Installation du CLI - v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Configuration du CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html#getting-started-quickstart-existing)
  * Les clés vous ont été partagées par oneDrive
  ```
  aws configure
  ```
  * Puis il faut entré les données selon les credentials
* [Gestion des profiles](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-format-profile)
  * Vous devez créer un profile du nom de votre équipe et l'utiliser pour toute les futures commandes
  * Pour cela nous avons changé directement dans le fichier ```User/.aws/credentials```

## IAM Policy

Voici la "policy" qui vous a été attribuée ( déja créer par le prof ) :

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
            ],
            "Resource": "arn:aws:s3:::devopsteam<XX>-i346/*" //XX -> devopsteam number
        }
    ]
}
```

## Exploiter un S3

Attention:
* Vous devez utiliser la v2 du CLI
* Le client offre soit la commande s3, soit s3api. En priorité vous devez essayer "s3".

### Créer un bucket

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* Le bucket existe-t-il ?

```bash
aws s3 ls --profile DEVOPSTEAM05 | grep "devopsteam*"
```

```
[OUTPUT]
2025-01-27 22:23:30 devopsteam01-i346
2025-01-27 22:28:03 devopsteam02-i346
2025-01-27 22:28:05 devopsteam03-i346
2025-01-27 22:28:06 devopsteam04-i346
2025-01-27 22:28:08 devopsteam05-i346
2025-01-27 22:28:09 devopsteam06-i346
2025-01-27 22:28:11 devopsteam07-i346
2025-01-27 22:28:13 devopsteam08-i346
2025-01-27 22:28:14 devopsteam09-i346
2025-01-27 22:28:16 devopsteam10-i346
2025-02-03 19:32:33 devopsteam99-i346
```

* Créer un bucket (via un compte admin)

```bash
aws s3 mb s3://devopsteam99-i346 --region eu-central-1 --profile s3-admin
```

```
[OUTPUT]
make_bucket: devopsteam99-i346
```


### Uploader un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Upload file](https://docs.aws.amazon.com/cli/v1/userguide/cli-services-s3-commands.html#using-s3-commands-managing-objects-copy)
* [Comment recupairer un objet](https://www.geeksforgeeks.org/get-object-in-aws-s3-using-ui-cli/)

* Après la vérification de des buckets j'ai uploader un fichier text test.txt

```bash
aws s3api get-object --bucket devopsteam05-i346 --key test.txt C:\test.txt --profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:38:04+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* ajout d'un fichier dans un bucket  

```bash
aws s3 cp C:\test.txt s3://devopsteam05-i346/ --profile DEVOPSTEAM05
```

```
[OUTPUT]
upload: C:\test.txt to s3://devopsteam05-i346/test.txt
```

### Uploader un répertoire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://docs.aws.amazon.com/fr_fr/cli/v1/userguide/cli_s3_code_examples.html)

* [Vérifier l'état du bucket avant votre commande]

```bash

```

```
[OUTPUT]

```

* J'utilise l'opption recurisve pour ajouter le dossier dans le bucket

```bash
 aws s3 cp --recursive C:\test_aws s3://devopsteam05-i346/ --profile DEVOPSTEAM05
```

```
[OUTPUT]
upload: C:\test_aws\test.txt to s3://devopsteam05-i346/test.txt
```

### Lister le contenu d'un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

### Synchroniser un répertoire local de sa machine avec un bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

### Publier un fichier présent sur un bucket en générant un lien (url) temporaire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Publier un objet en URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)

* [Vérifier l'état du bucket avant votre commande]
* Après la vérification de des buckets j'ai uploader un fichier text test.txt

```bash
aws s3api get-object --bucket devopsteam05-i346 --key test.txt C:\test.txt --profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:38:04+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
 aws s3 presign s3://devopsteam05-i346/test.txt --expires-in 604800 --profile DEVOPSTEAM05
```

```
[OUTPUT]
https://devopsteam05-i346.s3.amazonaws.com/test.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA2KFJKL4ORBNOOB4J%2F20250211%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250211T124526Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=cbe47509a7bdae703052cef3c6fff56cfd23a556e018b0a3609e52009083f822
```

### Supprimer un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Delete object](https://awscli.amazonaws.com/v2/documentation/api/2.0.34/reference/s3api/delete-object.html)

* Verification de l'état du bucket avant l'execution de la commande

```bash
aws s3api get-object --bucket devopsteam05-i346 --key test.txt C:\test.txt --profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:38:04+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3api delete-object --bucket devopsteam05-i346 --key test.txt --profile DEVOPSTEAM05
```
Aucun output à la commande, donc une nouvelle commande pour verifier l'absence du fichiers à été entrée (elle avait un output qui est le suivant).
```
[OUTPUT]
$ aws s3api get-object --bucket devopsteam05-i346 --key test.txt C:\test.txt --profile DEVOPSTEAM05

An error occurred (AccessDenied) when calling the GetObject operation: User: arn:aws:iam::709024702237:user/devopsteam05-i346 is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::devopsteam05-i346" because no identity-based policy allows the s3:ListBucket action
```

### Vider un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

### Extraire uniquement les metadonnées d'un objet

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

### Vider le bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

---

## Questions d'analyse

Consigne : répondre en utilisant des sources officielles et en vous appuyant dessus pour répondre.

### Pourquoi est-il déconseillé de détruire un bucket S3 selon AWS ?

* [Sources AWS]

[Votre réponse]

### Quelle est la différence entre un Bucket S3 et Glacier ?

* [Sources AWS]

[Votre réponse]

### Reprenez l'IAM "Policy" et expliquer ce que vous pouvez en déduire au niveau des droits qui vous sont alloués

Consigne : Reprenez la "policy" et documenter chaque ligne
