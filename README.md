# TP 8 : Présentation de Ansible
[Ansible](https://www.ansible.com/) permet d’automatiser la configuration et le déploiement d’applications sur des machines. L'avantage est qu'on peut ainsi dupliquer facilement et automatiquement une configuration sur autant de postes qu'on le souhaite ; ceci permet également, en cas de problème sur un poste, de redéployer automatiquement sa configuration initiale.

:warning: Ansible n'est disponible *que* sous Linux !

# Configuration / Architecture
L'idée est donc de piloter la configuration et le déploiement d'applications sur des machines, appelées *nodes* dans le jargon d'Ansible, depuis un "noeud superviseur" ou *node manager*.

Vous aurez par conséquent besoin (a minima) de deux machines, **configurées pour communiquer entre elles**. Vous pouvez bien entendu pour cela réutiliser les deux machines *Serveur* et *Client* du TP "Réseau".

:bulb: Si votre système d'exploitation hôte est un Linux, vous pouvez *a priori* vous en servir comme *node manager*, et vous n'avez donc besoin que d'une seule VM (le *node*). 

### Procédure de secours
Si toutefois vous ne disposiez que d'une seule machine, ou que vous ayez eu des problèmes à faire communiquer vos VMs, le plus simple pour démarrer rapidement ce TP est de :

 1. cloner une machine en état de fonctionnement
 2. configurer une interface réseau sur chaque machine en mode **Pont** (ce qui permettra aux machines de se voir, d'aller sur Internet, et même d'être vues depuis la machine hôte).

:bulb: Par ailleurs, vous aurez besoin d'effectuer un certain nombre de copier-coller ; **une connexion ssh sur vos VMs est donc indispensable**. Pour rappel, Windows 10 intègre désormais un client ssh natif, et vous pouvez aussi utiliser *[cmder](http://cmder.net/)*. De plus, aucune configuration particulière (en particulier, une redirection de port) n'est nécessaire si vos machines sont en mode *Pont* (puisque la machine hôte les "voit", vous pouvez vous y connecter directement en saisissant `ssh AdresseIP`).

### TP de synthèse
:bangbang: Ce TP fait appel à de nombreuses notions vues dans les TP précédents (réseau, gestion des utilisateurs, gestion des paquets...) ; il constitue ainsi en quelques sortes un TP de synthèse au cours duquel vous pourrez évaluer vos connaissances en administration système, et l'équipe pédagogique **votre autonomie**.

# Enoncé
OpenClassRooms propose depuis peu un [cours complet](https://openclassrooms.com/fr/courses/2035796-utilisez-ansible-pour-automatiser-vos-taches-de-configuration) et bien fait sur Ansible, organisé en trois parties. **Votre objectif pour ce TP est de réaliser les deux premières parties** (jusqu'au cours "Assemblez les opérations avec les playbooks pour automatiser le déploiement" inclus). Il s'agit d'un cours complètement guidé, il suffit principalement de suivre (**et comprendre !!!**) ce qui vous est demandé.

:information_source: Les quiz ne sont pas à réaliser dans le cadre du TP. Vous êtes évidemment très fortement encouragés à y répondre pour parfaire votre connaissance d'Ansible !

## Différences avec le cours OpenClassRooms

 - Adresses IP : les IP de vos machines ne correspondent pas nécessairement à celles utilisées dans le cours ; l'idéal aurait été de créer un réseau NAT, mais j'ai rencontré plusieurs problèmes (notamment de DNS) lorsque j'ai désactivé le DHCP de VirtualBox pour forcer les IP du cours. **Vous pouvez sans problème utiliser les IP configurées dans le TP "Réseau" ou celles proposées par le mode "Pont"**, il faudra juste penser à faire les changements dans les fichiers de configuration d'Ansible quand ce sera nécessaire
 - **Vous n'utiliserez qu'un seul *node*** sur lequel vous installerez tous les logiciels demandés
 - Dans le cours, les *nodes* tournent sous *CentOS* et non sous Ubuntu, ce qui conduit à un certain nombre de différences qui deviendront claires au fur et à mesure de la lecture :
   - l'auteur part du principe que vous disposez d'un compte *root* sur les nodes ; or, comme vous le savez, le compte *root* est désactivé par défaut sous Ubuntu. On peut tout à fait utiliser Ansible sans compte *root* (si l'on est *sudoer*), mais ceci nécessite de modifier des fichiers de configuration et risque d'induire de mauvaises manipulations dans le TP ; **vous pouvez donc commencer par activer le compte root sur le *node*** 
   - il n'existe pas de groupe *wheel*, **utilisez le groupe *sudo* à la place**
   - il est à moment donné question de Python 2, mais cette version est obsolète et n'est plus installée par défaut depuis Ubuntu 20.04. **Utilisez à la place la version de Python 3 disponible sur vos machines**
   - **le gestionnaire de paquets sous Ubuntu est *apt*** et non *yum*
   - les scripts de configuration proposés doivent être en conséquence légèrement modifiés pour tourner sous Ubuntu. **J'ai mis plusieurs scripts "corrigés" à disposition sur ce GitHub**.

:warning: Le cours comporte un certain nombre de coquilles (dans les commandes à taper, dans les captures d'écran montrant le résultat d'une commande, etc.) mais qui sont très faciles à corriger. **Encore une fois, ce TP doit vous permettre de vous auto-évaluer !**

> Written with [StackEdit](https://stackedit.io/).
