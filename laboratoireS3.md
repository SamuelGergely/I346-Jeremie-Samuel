# Laboratoire S3

## Installation et configuration du CLI

* [Installer le client git](https://git-scm.com/)
  * Git bash vous embarque de nombreuses commandes Linux utiles pour s'entrainer avec S3 (cat, grep, touch, ls)
* [Installation du CLI - v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Configuration du CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html#getting-started-quickstart-existing)
  * Les clés vous ont été partagées par oneDrive
* [Gestion des profiles](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-format-profile)
  * Vous devez créer un profile du nom de votre équipe et l'utiliser pour toute les futures commandes
  ```
  aws s3 <la commande> --profile devopsteam04
  ```

## IAM Policy

Voici la "policy" qui vous a été attribuée:

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
            "Resource": "arn:aws:s3:::devopsteam04-i346/*" //XX -> devopsteam number
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
aws s3 ls \
 --profile devopsteam99-i346 | grep "devopsteam*"
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
aws s3 mb s3://devopsteam99-i346 \
 --region eu-central-1 \
 --profile s3-admin
```

```
[OUTPUT]
make_bucket: devopsteam99-i346
```


### Uploader un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam04-i346 \
 --profile devopsteam04-i346
```

```
[OUTPUT]
An error occurred (AccessDenied) when calling the ListObjectsV2 operation: User:
 arn:aws:iam::709024702237:user/devopsteam04-i346 is not authorized to perform:
s3:ListBucket on resource: "arn:aws:s3:::devopsteam04-i346" because no identity-
based policy allows the s3:ListBucket action
// résultat normal, nous n'avons pas les autorisations pour lister l'intérieur d'un bucket
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3api put-object \
 --bucket devopsteam04-i346 \
 --key image_test.png \
 --body "C:/Users/pu22amq/Desktop/circuit_lampe_allume.png" \
 --profile devopsteam04-i346
```

```
[OUTPUT]
{
    "ETag": "\"5a400ef7bc943f344c8f427d2f91cd6d\"",
    "ChecksumCRC64NVME": "qbzWXcW1hmg=",
    "ChecksumType": "FULL_OBJECT",
    "ServerSideEncryption": "AES256"
}

```

### Uploader un répertoire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object \
 --bucket devopsteam04-i346 \
 --key image_test.png image_test.png \
 --profile devopsteam04-i346
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws ecr create-repository \
 --repository-name repo_test/test1 \
 --profile devopsteam04-i346 \ 
 --region eu-central-1
```

```
[OUTPUT]
An error occurred (AccessDeniedException) when calling the CreateRepository operation: User: arn:aws:iam::709024702237:user/devopsteam04-i346 is not aut
horized to perform: ecr:CreateRepository on resource: arn:aws:ecr:eu-central-1:709024702237:repository/repo_test/test1 because no identity-based policy
allows the ecr:CreateRepository action
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
aws s3api list-objects-v2 \
 --bucket devopsteam04-i346 \
 --prefix repo_test/test1 \
 --profile devopsteam04-i346
```

```
[OUTPUT]
An error occurred (AccessDenied) when calling the ListObjectsV2 operation: User: arn:aws:iam::709024702237:user/devopsteam04-i
346 is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::devopsteam04-i346" because no identity-based policy
 allows the s3:ListBucket action
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
aws s3 sync C:/Users/pu22amq/Desktop/image_proj_front s3://devopsteam04-i346/ \
 --profile devopsteam04-i346
```

```
[OUTPUT]
fatal error: An error occurred (AccessDenied) when calling the ListObjectsV2 operation: User: arn:aws:iam::709024702237:user/d
evopsteam04-i346 is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::devopsteam04-i346" because no identity
-based policy allows the s3:ListBucket action
```

### Publier un fichier présent sur un bucket en générant un lien (url) temporaire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object \
 --bucket devopsteam04-i346 \
 --key image_test.png image_test.png \
 --profile devopsteam04-i346
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T11:21:08+00:00",
    "ContentLength": 49781,
    "ETag": "\"5a400ef7bc943f344c8f427d2f91cd6d\"",
    "ChecksumCRC64NVME": "qbzWXcW1hmg=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "binary/octet-stream",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}

```

* [La commande à réaliser pour effecuter l'action demandée]

```bash (Pour une heure seulement par défault)
aws s3 presign s3://devopsteam04-i346/image_test.png \
 --profile devopsteam04-i346
```
```bash (Pour une semaine)
aws s3 presign s3://devopsteam04-i346/image_test.png \
 --profile devopsteam04-i346 \
 --expires-in 604800
```

```
[OUTPUT]
$ aws s3 presign s3://devopsteam04-i346/image_test.png --profile devopsteam04-i346
https://devopsteam04-i346.s3.amazonaws.com/image_test.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA2KFJKL4OTZDZNJM5%2F20250205%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250205T111539Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=8b279825f0e7eae69106b642dc25fd1108d7ba7ec9ecd4629adb2513111afe17

```

### Supprimer un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object \
 --bucket devopsteam04-i346 \
 --key image_test.png image_test.png \
 --profile devopsteam04-i346
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T11:21:08+00:00",
    "ContentLength": 49781,
    "ETag": "\"5a400ef7bc943f344c8f427d2f91cd6d\"",
    "ChecksumCRC64NVME": "qbzWXcW1hmg=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "binary/octet-stream",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 rm s3://devopsteam04-i346/image_test.png \
 --profile devopsteam04-i346
```

```
[OUTPUT]
delete: s3://devopsteam04-i346/image_test.png
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
aws s3 rm s3://devopsteam04-i346/repo_test/test1 \
 --recursive \
 --profile devopsteam04-i346
```

```
[OUTPUT]
fatal error: An error occurred (AccessDenied) when calling the ListObjectsV2 operation: User: arn:aws:iam::709024702237:user/d
evopsteam04-i346 is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::devopsteam04-i346" because no identity
-based policy allows the s3:ListBucket action
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
aws s3api head-object \
 --bucket devopsteam04-i346 \
 --key image_test.png \
 --profile devopsteam04-i346
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T11:21:08+00:00",
    "ContentLength": 49781,
    "ETag": "\"5a400ef7bc943f344c8f427d2f91cd6d\"",
    "ContentType": "binary/octet-stream",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
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
aws s3 rm s3://devopsteam04-i346/image_test.png \
 --profile devopsteam04-i346
```

```
[OUTPUT]
delete: s3://devopsteam04-i346/image_test.png
(impossible de supprimer automatiquement tout le contenu du bucket d'un seul coup, manque de l'autorisation ListObjectV2)
```

---

## Questions d'analyse

Consigne : répondre en utilisant des sources officielles et en vous appuyant dessus pour répondre.

### Pourquoi est-il déconseillé de détruire un bucket S3 selon AWS ?

* [Sources AWS]

[Votre réponse]

### Quelle est la différence entre un Bucket S3 et Glacier ?

* [What is Amazon Glacier?](https://www.techtarget.com/searchaws/definition/Glacier-Amazon-Glacier)

Glacier est plutôt une option prévue pour archiver des document dont le besoin d'accès est rare, mais probablement requis à un moment.
Alors que le bucket S3 est dynamique et rapide, Glacier serait incapable de stocker un stie web statique par exemple.

### Reprenez l'IAM "Policy" et expliquer ce que vous pouvez en déduire au niveau des droits qui vous sont alloués

Consigne : Reprenez la "policy" et documenter chaque ligne

```json
{
    "Version": "2012-10-17", // déclare la version
    "Statement": [ // liste de rêgles d'acces au bucket
        {
            "Effect": "Allow", // autorise l'utilisateur à effectuer le/les action(s) suivante(s)
            "Action": "s3:ListAllMyBuckets", // action(s) autorisée(s) (lister tout les buckets)
            "Resource": "arn:aws:s3:::*" // indique sur quelle(s) ressources les autorisations sont appliquées
        },
        {
            "Effect": "Allow", // autorise l'utilisateur à effectuer le/les action(s) suivante(s)
            "Action": [ // action(s) autorisée(s)
                "s3:PutObject", // action no 1 (ajouter un objet sur le bucket)
                "s3:GetObject", // action no 2 (obtenir un objet sur le bucket)
                "s3:DeleteObject" // action no 3 (supprimer un objet sur le bucket)
            ],
          // indique sur quelle(s) ressources les autorisations sont appliquées
            "Resource": "arn:aws:s3:::devopsteam<04>-i346/*" //XX -> devopsteam number
        }
    ]
}
```
