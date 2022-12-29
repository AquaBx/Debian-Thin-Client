# Création d’un client léger sur un PC

## Étape 1 : Installation de Debian

C’est plutôt simple, il suffit d’installer Debian sur une clé avec Rufus, de booter dessus et puis zou

## Étape 2 : Paramétrage de Debian

On se connecte au compte créé, puis on lance un terminal et on lance

```bash
su
apt update && apt upgrade
```

Pour mettre tout à jour
Ensuite on va activer le démarrage automatique

![page1_1](https://user-images.githubusercontent.com/35542432/174541781-4852df38-b753-40e8-b242-70bb67445489.jpg)
![page2_1](https://user-images.githubusercontent.com/35542432/174541838-26d305b4-08cb-4606-89e8-a88cb30acf61.jpg)

Déverrouiller et mettez debian en tant qu’administrateur

Puis ajouter un nouvel utilisateur : Invité

Mettez-lui un mot de passe provisoire

Puis cliquez sur connexion automatique

Ouvrez un terminal et entrez : 

```bash
su
passwd –d invite
chgrp adm /usr/share/applications/
sudo usermod -a -G adm debian
chmod 751 /usr/share/applications/
```

On enlève le mot de passe de l’invité, puis on change le groupe d’appartenance des applications aux adm, on ajoute debian au groupe adm, puis on enlève les permissions de lecture des applications aux utilisateurs

## Étape 3 : Configuration du rdp

Il va tout d’abord devoir télécharger quelques fichiers
  
Mettre les fichiers dans le /home/<<nom d’utilisateur>>

Faire un clic droit sur le dossier puis ouvrir un terminal, et lancer les commandes :

```bash
su
chmod +x rdp_script
nano rdp_script
```

Puis modifier les lignes rds, lbi et domain en fonction des paramètres du serveur

⚠️ : si le domaine n'est pas rempli les erreurs dans les logs seront les mêmes que pour un mauvais identifiant 

Enfin lancez :

```bash
mv rdp.desktop /usr/share/xsessions/
mv rdp_script /usr/bin/
```

Maintenant tout est bon, il faut maintenant changer d’utilisateur.

Ensuite allez sur l’écran de connexion et vérifier que rdp est bien sélectionner puis se connecter

 ![page3_3](https://user-images.githubusercontent.com/35542432/174541890-9f0cd284-0f35-4c72-a565-2dc5cc2c85e6.jpg)

Le programme devrait se lancer normalement

Au prochain redémarrage l’ordinateur devrait garder ces paramètres pour acquis et se connecter automatiquement sur RDP

## Étape 4 : comment relancer le compte admin

C’est très simple, cliquer sur changer d’utilisateur et connecter vous sur votre compte

Bon, le script rdp se lance tout seul, ne surtout pas le fermer sinon vous vous déconnectez 🙂

Pour modifier les paramètres après installation

```bash
su
nano /usr/bin/rdp_script
```

## Étape 5 : comment lire les logs

sur la session debian

ouvrir un terminal puis lancer

```bash
su
cat /home/invite/rdp_script.log
```
ou
```bash
su
cat /home/debian/rdp_script.log
```
cela donnera un fichier de cette forme

```
[2022-12-29 10:36:39] Entrée du script
[10:36:45:500] [30566:30567] [WARN][com.freerdp.core.nla] - SPNEGO received NTSTATUS: STATUS_LOGON_FAILURE [0xC000006D] from server
[10:36:45:500] [30566:30567] [ERROR][com.freerdp.core] - nla_recv_pdu:freerdp_set_last_error_ex ERRCONNECT_LOGON_FAILURE [0x00020014]
[10:36:45:500] [30566:30567] [ERROR][com.freerdp.core.rdp] - rdp_recv_callback: CONNECTION_STATE_NLA - nla_recv_pdu() fail
[10:36:45:500] [30566:30567] [ERROR][com.freerdp.core.transport] - transport_check_fds: transport->ReceiveCallback() - -1
[2022-12-29 10:37:05] Sortie du script

[2022-12-29 10:38:04] Entrée du script
[10:38:11:178] [30684:30685] [WARN][com.freerdp.core.nla] - SPNEGO received NTSTATUS: STATUS_LOGON_FAILURE [0xC000006D] from server
[10:38:11:178] [30684:30685] [ERROR][com.freerdp.core] - nla_recv_pdu:freerdp_set_last_error_ex ERRCONNECT_LOGON_FAILURE [0x00020014]
[10:38:11:178] [30684:30685] [ERROR][com.freerdp.core.rdp] - rdp_recv_callback: CONNECTION_STATE_NLA - nla_recv_pdu() fail
[10:38:11:178] [30684:30685] [ERROR][com.freerdp.core.transport] - transport_check_fds: transport->ReceiveCallback() - -1
[2022-12-29 10:40:34] Sortie du script

[2022-12-29 10:46:45] Entrée du script
[10:58:57:688] [33427:33428] [ERROR][com.freerdp.core] - rdp_set_error_info:freerdp_set_last_error_ex ERRINFO_RPC_INITIATED_DISCONNECT_BY_USER [0x0001000B]
[10:58:58:019] [33427:33804] [ERROR][com.freerdp.channels.smartcard.client] - SCardGetStatusChangeW failed with error SCARD_E_CANCELLED [-2146435070]
[10:58:58:019] [33427:33804] [WARN][com.freerdp.channels.smartcard.client] - IRP failure: SCardGetStatusChangeW (0x000900A4), status: SCARD_E_CANCELLED (0x80100002)
[10:58:58:019] [33427:33491] [ERROR][com.freerdp.channels.rdpdr.client] - pVirtualChannelWriteEx failed with CHANNEL_RC_BAD_CHANNEL_HANDLE [00000007]
[2022-12-29 11:13:32] Entrée du script
[11:13:36:051] [34835:34836] [ERROR][com.freerdp.core] - freerdp_tcp_is_hostname_resolvable:freerdp_set_last_error_ex ERRCONNECT_DNS_NAME_NOT_FOUND [0x00020005]
[2022-12-29 11:13:37] Sortie du script

[2022-12-29 11:14:48] Entrée du script
[11:14:52:370] [34932:34933] [WARN][com.freerdp.core.nla] - SPNEGO received NTSTATUS: STATUS_LOGON_FAILURE [0xC000006D] from server
[11:14:52:370] [34932:34933] [ERROR][com.freerdp.core] - nla_recv_pdu:freerdp_set_last_error_ex ERRCONNECT_LOGON_FAILURE [0x00020014]
[11:14:52:370] [34932:34933] [ERROR][com.freerdp.core.rdp] - rdp_recv_callback: CONNECTION_STATE_NLA - nla_recv_pdu() fail
[11:14:52:371] [34932:34933] [ERROR][com.freerdp.core.transport] - transport_check_fds: transport->ReceiveCallback() - -1
[2022-12-29 11:14:53] Sortie du script

[2022-12-29 11:15:20] Entrée du script
[11:15:32:697] [35016:35017] [ERROR][com.freerdp.core] - rdp_set_error_info:freerdp_set_last_error_ex ERRINFO_CB_CONNECTION_ERROR_INVALID_SETTINGS [0x00010410]
[11:15:32:717] [35016:35017] [ERROR][com.freerdp.core] - rdp_set_error_info:freerdp_set_last_error_ex ERRINFO_CB_CONNECTION_ERROR_INVALID_SETTINGS [0x00010410]
[11:15:32:717] [35016:35017] [ERROR][com.freerdp.core] - rdp_set_error_info: TODO: Trying to set error code ERRINFO_CB_CONNECTION_ERROR_INVALID_SETTINGS, but ERRINFO_CB_CONNECTION_ERROR_INVALID_SETTINGS already set!
[2022-12-29 11:15:33] Sortie du script
```

⚠️ : si le domaine n'est pas rempli les erreurs dans les logs seront les mêmes que pour un mauvais identifiant 


dans ce fichier, les ouvertures du script, ce qui correspond à l'ouverture de la session invité est horodaté, ainsi que sa fermeture.


code erreur les plus communs:

| Code Erreur       | Description                                                  |
| :---------------- |:-------------------------------------------------------------|
| LOGIN_FAILURE     | mauvais identifiants ou mauvais domaine                      |
| ERRINFO_CB_CONNECTION_ERROR_INVALID_SETTINGS    | mauvais lbi                    |
| ERRCONNECT_DNS_NAME_NOT_FOUND                   | mauvaise adresse rds           |
| Veuillez rentrer un mot de passe | l'utilisateur n'a pas rentré de mot de passe  |
| Veuillez rentrer un identifiant  | l'utilisateur n'a pas rentré d'identifiant    |
