# Comment installer NVIDIA NemoClaw : Guide étape par étape

NemoClaw est une pile open-source de NVIDIA conçue pour exécuter les agents d'IA OpenClaw en toute sécurité en ajoutant des contrôles de confidentialité, un bac à sable (sandboxing) et des barrières de sécurité.

Suivez ces étapes simples pour configurer et exécuter votre agent d'IA sécurisé.

## Prérequis

Avant de commencer, assurez-vous que votre système répond aux exigences suivantes :

* **Système d'exploitation :** Linux (Ubuntu 22.04+ recommandé). macOS et Windows (via WSL2) sont pris en charge mais à titre expérimental.
* **Matériel :** Au moins 8 Go de RAM (16 Go fortement recommandés) et environ 40 Go d'espace disque disponible.
* **Clé API :** Une clé API NVIDIA (vous pouvez en obtenir une gratuitement sur `build.nvidia.com`).

## Étape 1 : Préparer votre système

NemoClaw nécessite l'installation de Docker et de Node.js (version 20 ou 22) pour fonctionner correctement.

### 1. Vérifier Docker :

Assurez-vous que Docker est installé et que vous avez les bonnes autorisations sans avoir à utiliser `sudo` à chaque fois :

```bash
docker ps
```

(Si vous obtenez une erreur d'autorisation refusée "permission denied", exécutez `sudo usermod -aG docker $USER`, puis déconnectez-vous et reconnectez-vous).

### 2. Installer Node.js :

Exécutez les commandes suivantes pour installer Node.js (version 22) :

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Vérifiez l'installation en exécutant `node --version`.

## Étape 2 : Installer NemoClaw

NVIDIA fournit un script d'installation simple qui s'occupe des tâches complexes.

Exécutez la commande suivante dans votre terminal :

```bash
curl -fsSL https://nvidia.com/nemoclaw.sh | bash
```

Remarque : Selon la configuration de votre système, vous devrez peut-être l'exécuter avec `sudo bash` si vous rencontrez des erreurs d'autorisation.

## Étape 3 : Configurer votre agent (Onboarding)

Une fois l'installation terminée, vous devez configurer votre bac à sable (sandbox) et les paramètres d'inférence.

Exécutez l'assistant de configuration :

```bash
nemoclaw onboard
```

Lors de ce processus interactif :

* Donnez un nom à votre assistant (par exemple, `my-assistant`).
* Entrez votre clé API NVIDIA lorsque vous y êtes invité.
* Acceptez les configurations par défaut pour les politiques de sécurité et la configuration du bac à sable.

Remarque : Le script va télécharger l'image du bac à sable (environ 2,4 Go). Cela peut prendre quelques minutes.

## Étape 4 : Se connecter et discuter !

Votre environnement sécurisé est maintenant prêt. Il est temps de vous connecter à votre agent isolé.

### 1. Se connecter au bac à sable :

Remplacez `my-assistant` par le nom que vous avez choisi à l'Étape 3.

```bash
nemoclaw my-assistant connect
```

### 2. Lancer l'interface de discussion :

Une fois à l'intérieur du bac à sable isolé, lancez l'interface utilisateur textuelle (TUI) d'OpenClaw :

```bash
openclaw tui
```

Félicitations ! Vous pouvez maintenant taper des messages en toute sécurité et interagir avec votre agent d'IA isolé.

## Conseils de dépannage

* **Erreurs de manque de mémoire (OOM) :** Si l'installation plante sur une machine avec 8 Go de RAM, essayez d'ajouter de l'espace d'échange (swap space) à votre système.
* **Utilisateurs de WSL2 :** Si vous utilisez le sous-système Windows pour Linux et que vous rencontrez des problèmes avec le transfert de GPU (GPU passthrough) pendant `nemoclaw onboard`, vous devrez peut-être démarrer la passerelle OpenShell manuellement sans l'indicateur `--gpu`.
