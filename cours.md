# Git remote

## SSH
SSH (Secure Shell) est un protocole réseau sécurisé qui permet de se connecter à un ordinateur distant via un réseau non sécurisé. Il chiffre les communications entre le client et le serveur, garantissant confidentialité et intégrité.

### Cas d'utilisation
- Accéder à distance à un serveur pour exécuter des commandes.
- Transférer des fichiers de manière sécurisée entre machines.
- Gérer des systèmes à distance, comme des serveurs web ou des bases de données.
- Configurer des connexions sécurisées pour des applications comme Git.


## Installation

Si pas installé :
```bash
  brew install openssh
```
Pour vérifier l'installation : (`-V` permet d'afficher la version de SSH)
```bash
  ssh -V
```

## SSH Key
SSH utilise un système de cryptographie asymétrique basé sur deux clés :

- La clé privée : elle reste secrète et stockée en local sur ton ordinateur.

- La clé publique : elle peut être partagée librement, et est installée sur le serveur distant.

Les deux clés sont liées mathématiquement : ce qui est chiffré avec l’une ne peut être déchiffré qu’avec l’autre.

### Générer une clé SSH

Pour ça, on va utiliser la commande : `ssh-keygen`

Exemple : `ssh-keygen -t ed25519 -C "nto@wedigital.garden" -f ~/.ssh/id_wizards`
- `-t ed25519` : spécifie le type de clé à générer (ed25519 est un algorithme moderne et sécurisé). Autre algorithme utilisé : `-t rsa`
- `-C "nto@wedigital.garden"` : ajoute un commentaire à la clé (souvent utilisé pour indiquer l'adresse e-mail de l'utilisateur).
- `-f ~/.ssh/id_wizards` : permet de spécifier le nom et l'emplacement du fichier de la clé privée. Si ce paramètre n'est pas spécifié, la clé sera enregistrée par défaut dans `~/.ssh/id_rsa` (pour RSA) ou `~/.ssh/id_ed25519` (pour Ed25519).

Lors de la création de la clé, tu vas pouvoir choisir de protéger ta clé privée par une phrase de passe. C'est une bonne pratique de sécurité, mais cela signifie que tu devras entrer cette phrase de passe chaque fois que tu utiliseras la clé.

### Ajouter la clé SSH à l'agent SSH

L'agent SSH est un programme qui stocke les clés privées utilisées pour l'authentification. Il permet de ne pas avoir à entrer la phrase de passe à chaque fois que tu te connectes à un serveur.

- Démarrer l'agent SSH
```bash
    eval $(ssh-agent -s)
```

- Ouvrir la configuration de l'agent SSH
```bash
    open ~/.ssh/config
```

- Si le fichier n'existe pas, crée-le avec la commande :
```bash
    touch ~/.ssh/config
```

- Ajouter la clé SSH à l'agent
```Text
    Host github.com
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/[nom_de_la_clé, ex : id_ed25519]
```

- Ajouter la clé SSH à l'agent
```bash
    ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```