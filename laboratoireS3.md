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

Voici la "policy" qui vous a été attribuée ( déja créée par le prof ) :

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

* [AWS Official Doc - Upload file]([https://docs.aws.amazon.com/cli/v1/userguide/cli-services-s3-commands.html#using-s3-commands-managing-objects-copy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html))
* [Comment recupairer un objet](https://www.geeksforgeeks.org/get-object-in-aws-s3-using-ui-cli/)

* Après la vérification de des buckets j'ai uploader un fichier text test.txt

```bash
aws s3 ls s3://devopsteam05-i346 \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
2025-02-12 11:07:18          0 test.txt
2025-02-11 14:32:28          0 test_aws
2025-02-12 11:19:47          0 upladRepertoir
```

* ajout d'un fichier dans un bucket  

```bash
aws s3 cp C:\test.txt s3://devopsteam05-i346/ \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
upload: C:\test.txt to s3://devopsteam05-i346/test.txt
```

### Uploader un répertoire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Upload un repertoir](https://awscli.amazonaws.com/v2/documentation/api/2.0.34/reference/s3api/put-object.html#examples)

* Vérification de l'état du répertoir "upladRepertoir" qu'on met dans le répertoir "test_aws"

```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key upladRepertoir test_aws \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-11T12:48:31+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "binary/octet-stream",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* Nous avons utiliser la comande put-object pour créer un répertoir

```bash
aws s3 cp Amael s3://devopsteam05-i346/Amael \
--recursive \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
upload: Amael\Hugo.txt to s3://devopsteam05-i346/Amael/Hugo.txt
```

* autre possibiliter

```bash
aws s3 cp \
--recursive ./test_aws s3://devopsteam05-i346 \
--profile DEVOPSTEAM05
```

### Lister le contenu d'un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Upload un repertoir](https://awscli.amazonaws.com/v2/documentation/api/2.0.34/reference/s3api/put-object.html#examples)

* Vérification de l'état du répertoir "upladRepertoir" qu'on met dans le répertoir "test_aws"

```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key upladRepertoir test_aws \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-11T12:48:31+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "binary/octet-stream",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* pour lister ce qui a dans le repertoir j'ai utiliser la meme commande que pour verifier l'état du répertoir

```bash
aws s3 ls s3://devopsteam05-i346 \
--recursive \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
2025-02-25 13:40:41         13 Amael/Hugo.txt
2025-02-25 13:35:27         21 demo.txt
2025-02-12 11:07:18          0 test.txt
2025-02-11 14:32:28          0 test_aws
2025-02-12 12:25:43         21 upladRepertoir
```

### Synchroniser un répertoire local de sa machine avec un bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Syncroniser un repertoire ](https://docs.outscale.com/fr/userguide/Synchroniser-des-objets-dans-un-bucket.html)

* Vérification de l'état du répertoir "upladRepertoir" qu'on met dans le répertoir "test_aws"
  
```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key upladRepertoir test_aws \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-11T12:48:31+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "binary/octet-stream",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 sync Amael s3://devopsteam05-i346/Amael \
--profile DEVOPSTEAM05
```

* Cette comande ne marche pas car nous n'avons pas les droit donc il n'y a pas de retour. Mais 
```
[OUTPUT]
upload: Amael\Hugo.txt to s3://devopsteam05-i346/Amael/Hugo.txt
```


### Publier un fichier présent sur un bucket en générant un lien (url) temporaire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Publier un objet en URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)

* [Vérifier l'état du bucket avant votre commande]
* Après la vérification de des buckets j'ai uploader un fichier text test.txt

```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key test.txt C:\test.txt \
--profile DEVOPSTEAM05
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
aws s3 presign s3://devopsteam05-i346/Amael/Hugo.txt \
--expires-in 60 \
--region eu-central-1 \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
[https://devopsteam05-i346.s3.amazonaws.com/test.txt](https://devopsteam05-i346.s3.eu-central-1.amazonaws.com/Amael/Hugo.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA2KFJKL4ORBNOOB4J%2F20250225%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Date=20250225T124726Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Signature=1332b50915efc0badf3a7d8c1c1b4d2cf04a8ca7de882362228e74061a6d164e)
```

### Supprimer un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Delete object](https://awscli.amazonaws.com/v2/documentation/api/2.0.34/reference/s3api/delete-object.html)

* Verification de l'état du bucket avant l'execution de la commande

```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key test.txt C:\test.txt \
--profile DEVOPSTEAM05
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
aws s3 rm s3://devopsteam05-i346/demo.txt \
--profile DEVOPSTEAM05
```
Aucun output à la commande, donc une nouvelle commande pour verifier l'absence du fichiers à été entrée (elle avait un output qui est le suivant).
```
[OUTPUT]
delete: s3://devopsteam05-i346/demo.txt
```

### Vider un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Delete object](https://awscli.amazonaws.com/v2/documentation/api/2.0.34/reference/s3api/delete-object.html)

* [Vérifier l'état du bucket avant votre commande]


```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key test.txt C:\test.txt \
--profile DEVOPSTEAM05
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
aws s3 rm s3://devopsteam05-i346/Amael \
--recursive \
--profile DEVOPSTEAM05
```

Pas d'output dans la commande précédente, réalisation d'une commande de test qui est la suivante
```
[OUTPUT]
delete: s3://devopsteam05-i346/Amael/Hugo.txt

```

### Extraire uniquement les metadonnées d'un objet

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key test.txt C:\test.txt \
--profile DEVOPSTEAM05
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
aws s3api get-object-attributes \
--bucket devopsteam05-i346 \
--key Amael/Hugo.txt \
--object-attributes ObjectSize \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
{
    "LastModified": "2025-02-25T12:50:16+00:00",
    "ObjectSize": 15
}
```

### Vider le bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Vider Bucket](https://docs.aws.amazon.com/cli/latest/reference/s3api/delete-object.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object \
--bucket devopsteam05-i346 \
--key test_aws test_aws \
--profile DEVOPSTEAM05
```

```
[OUTPUT]
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 rm s3://devopsteam05-i346/ \
--recursive \
--profile DEVOPSTEAM05
```

* il n'y a pas de retour dans la console donc j'ai refait un êtat du bucket
```
delete: s3://devopsteam05-i346/upladRepertoir
delete: s3://devopsteam05-i346/Amael/Hugo.txt
delete: s3://devopsteam05-i346/test.txt
delete: s3://devopsteam05-i346/test_aws

```

---

## Questions d'analyse

Consigne : répondre en utilisant des sources officielles et en vous appuyant dessus pour répondre.

### Pourquoi est-il déconseillé de détruire un bucket S3 selon AWS ?

* [Sources AWS](https://docs.aws.amazon.com/fr_fr/AmazonS3/latest/userguide/delete-bucket.html)

Car il risque de detruir les fichiers à l'inteur du bucket à tout jamais et le nom du bucket ne pourras être rétuliser.

### Quelle est la différence entre un Bucket S3 et Glacier ?

* [Sources AWS]

[Votre réponse]

### Reprenez l'IAM "Policy" et expliquer ce que vous pouvez en déduire au niveau des droits qui vous sont alloués

Nous avons accés aux commandes comme Get-object, Delet-object et Put-object
