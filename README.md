<span class="badge-opencollective"><a href="https://github.com/ZarTek-Creole/DONATE" title="Donate to this project"><img src="https://img.shields.io/badge/open%20collective-donate-yellow.svg" alt="Open Collective donate button" /></a></span>
[![CC BY 4.0][cc-by-shield]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

# IRCServices
> introduction: 
> 
> Le Package IRC Services créé une interface en TCL et la connexion d'un Service à un IRCD (comme anope).
>
> Ce package fournit des [Commandes](#commandes) de bas niveau pour gérer le protocole IRC Serveur/service pour une communication multidiffusion immédiate et interactive.
> 
> Merci d'etre indulgent et repport bugs, idées, etc sur 

* [Creer un ticket](github.com/ZarTek-Creole/TCL-PKG-IRCServices/issues/new)
* [Site web: IRCServices](github.com/ZarTek-Creole/TCL-PKG-IRCServices)

# Informations sur la documentation
> Les informations entre < texte > sont obligatoires et ceux entre [texte] sont facultatives.


# Table des matières
- [IRCServices](#ircservices)
- [Informations sur la documentation](#informations-sur-la-documentation)
- [Table des matières](#table-des-matières)
- [Prérequis](#prérequis)
- [Téléchargement](#téléchargement)
  - [Avec git (conseillé):](#avec-git-conseillé)
  - [Avec wget :](#avec-wget-)
- [Installation](#installation)
  - [avec setup.tcl (systeme) :](#avec-setuptcl-systeme-)
  - [avec auto_path (userdir):](#avec-auto_path-userdir)
- [Utilisation](#utilisation)
  - [Exemple](#exemple)
- [Les commandes IRCServices](#les-commandes-ircservices)
  - [::IRCServices::**connection**](#ircservicesconnection)
  - [::IRCServices::**listnetworks**](#ircserviceslistnetworks)
  - [::IRCServices::**config** ?clé? ?valeur?](#ircservicesconfig-clé-valeur)
  - [Les commandes de réseau](#les-commandes-de-réseau)
    - [net **eventbind** ?event? ?script?](#net-eventbind-event-script)
      - [Liste des events](#liste-des-events)
    - [net **eventget** <event> <script>](#net-eventget-event-script)
    - [net **eventexists** event script](#net-eventexists-event-script)
    - [net **connect** <Server_HostName> <[+]Server_Port> <Server_Password> [Server_Protocol] [Server_Name] [Server_ID]](#net-connect-server_hostname-server_port-server_password-server_protocol-server_name-server_id)
      - [Server_HostName](#server_hostname)
      - [Server_Port](#server_port)
      - [Server_Password](#server_password)
      - [Server_Name](#server_name)
      - [Server_Protocol (new/old)](#server_protocol-newold)
    - [net **config** [key] [value]](#net-config-key-value)
      - [key](#key)
      - [value](#value)
    - [net **log** level message](#net-log-level-message)
    - [net **logname**](#net-logname)
    - [net **connected**](#net-connected)
    - [net **sockname**](#net-sockname)
    - [net **peername**](#net-peername)
    - [net **socket**](#net-socket)
    - [net **user** username localhostname localdomainname userinfo](#net-user-username-localhostname-localdomainname-userinfo)
    - [net **nick** nick](#net-nick-nick)
    - [net **ping** target](#net-ping-target)
    - [net **serverping**](#net-serverping)
    - [net **join** channel ?key?](#net-join-channel-key)
    - [net **part** channel ?message?](#net-part-channel-message)
    - [net **quit** ?message?](#net-quit-message)
    - [net **privmsg** target message](#net-privmsg-target-message)
    - [net **notice** target message](#net-notice-target-message)
    - [net **ctcp** target message](#net-ctcp-target-message)
    - [net **kick** channel target ?message?](#net-kick-channel-target-message)
    - [net **mode** target args](#net-mode-target-args)
    - [net **topic** channel message](#net-topic-channel-message)
    - [net **invite** channel target](#net-invite-channel-target)
    - [net **send** text](#net-send-text)
    - [net **destroy**](#net-destroy)
  - [Callback Commands](#callback-commands)
    - [**who** ?address?](#who-address)
    - [**action**](#action)
    - [**target**](#target)
    - [**additional**](#additional)
    - [**header**](#header)
    - [**msg**](#msg)

# Prérequis
* tcllib (logger)

# Téléchargement
## Avec git (conseillé):

`git clone  https://github.com/ZarTek-Creole/TCL-PKG-IRCServices.git /path/to/install`

## Avec wget :

```bash
wget https://github.com/ZarTek-Creole/TCL-PKG-IRCServices/archive/refs/heads/main.zip -O /path/to/install/TCL-PKG-IRCServices.zip
unzip -x TCL-PKG-IRCServices.zip
rm TCL-PKG-IRCServices.zip
```

# Installation
## avec setup.tcl (systeme) :

```bash
➜ cd /path/to/install
➜ sudo ./setup.tcl
tcltk/tcl8.6 /usr/lib/tcltk]
Installing /usr/lib/tcltk/IRCServices/pkgIndex.tcl
Installing /usr/lib/tcltk/IRCServices/ircservices.tcl
Done
➜  tclsh
% package require IRCServices
0.0.1
%
```

## avec auto_path (userdir):

Editez votre eggdrop.conf et ajouter avant vos source le repertoire contenant ircservices.tcl (/path/to/install)
```tcl
lappend auto_path /path/to/install
```
les commandes IRCServices seront disponible apres le chargement dans un tcl de celui-ci
```tcl
package require IRCServices
```

# Utilisation
## Exemple
```tcl
➜ tclsh
% package require IRCServices
0.0.1
% set CONNECT_ID [::IRCServices::connection]; # Creer une instance services
::IRCServices::IRCServices0::network
% $CONNECT_ID connect 
wrong # args: should be "::IRCServices::IRCServices0::cmd-connect hostname port password ?ts6? ?name? ?id?"
% $CONNECT_ID connect 127.0.0.0 +7500 passwordlink 1 Extra-Cool.FR 00C; # Creer une instance services
1
% set BOT_ID [$CONNECT_ID bot]; #Creer une instance bot dans linstance services
::IRCServices::IRCServices0::b0::bot
% $BOT_ID create
wrong # args: should be "::IRCServices::IRCServices0::b0::cmd-create botnick botident bothost ?botgecos? ?botmodes?"
% $BOT_ID create ClaraServ services ClaraServ.eggdrop.fr "Visit: https://git.io/JYY9b" +Soiq; # creer le botService et le connecte
1
% $BOT_ID join #Services; # le faire joindre le salon #Services
1
% $BOT_ID eventbind PRIVMSG {
                set cmd         [lindex [msg] 0]
                set data        [lrange [msg] 1 end]
                ##########################
                #--> Commandes Privés <--#
                ##########################
                # si [target] ne commence pas par # c'est un pseudo
                if { [string index [target] 0] != "#"} {
                        if { ${cmd} == "help"             }       { 
                                puts "PRIV: [who2] [target] ${cmd} ${data}"
                        }
                }
                ##########################
                #--> Commandes Salons <--#
                ##########################
                # si [target] commence par # c'est un salon
                if { [string index [target] 0] == "#"} {
                        if { ${cmd} == "!cmds"    }       { 
                                puts "PUB: [who] [target] ${cmd} ${data}"
                        }
                }
        }; # Creer un event sur PRIVMSG

}; # Creer un event sur PRIVMSG
1 
```
Un exemple en fichier tcl : [example.tcl](example.tcl)

# Les commandes IRCServices

## ::IRCServices::**connection**
> La commande [[::IRCServices::connection]](#ircservicesconnection) créée une nouvelle instance pour gérer une connexion IRC.
> 
> La création de cette instance IRCServices ne créée pas automatiquement la connexion réseau.
> 
> Il renvoie une nouvelle commande d'espace de noms **::IRCServices::** qui peut être utilisée pour interagir avec la nouvelle connexion IRC.
> 
> Vous pouvez voir toutes les instances IRCServices avec la commande [[::IRCServices::listnetworks]](#ircserviceslistnetworks)
## ::IRCServices::**listnetworks**
> Renvoie une liste de toutes les connexions actuelles qui ont été créées avec [[::IRCServices::connection]](#ircservicesconnection)
```
<@ZarTek> tcl return [::IRCServices::listnetworks]
<ClaraDev> Return: ::IRCServices::IRCServices2::network ::IRCServices::IRCServices0::network ::IRCServices::IRCServices1::network - 0.076 ms
```

## ::IRCServices::**config** ?clé? ?valeur?
> Définit la configuration ?clé? ?valeur?
>
> Les clés de configuration actuellement définies sont les flags booléens **logger** et **debug**.
> 
> Logger oblige **IRCServices** à utiliser le package logger pour afficher les erreurs.
> 
> le **debug** nécessite un **logger** et affiche une sortie de débogage supplémentaire.
> 
> Si aucune ?clé? ou ?valeur? est donné les valeurs actuelles sont retournées.
```
<@ZarTek> tcl return [::IRCServices::config]
<ClaraDev> Return: logger 0 debug 0 - 0.279 ms

<@ZarTek> tcl return [::IRCServices::config logger 1]
<ClaraDev> Return: 1 - 2.829 ms

<@ZarTek> tcl return [::IRCServices::config]
<ClaraDev> Return: logger 1 debug 0 - 0.016 ms
```
## Les commandes de réseau
> Dans la liste suivante des méthodes de connexion disponibles,
**net** représente une commande de connexion renvoyée par **[[::irc::connection]](#ircconnection)**.

### net **eventbind** ?event? ?script?
> Créé un bind (déclencheur) pour l'événement spécifié.
> La liste d'event ci-dessous et plusieurs autres événements sont définis.
> 
> **defaultcmd** ajoute une commande qui est appelé si aucun autre rappel n'est présent.
> 
> EOF est appelé lors de la fermeture voulue ou accidentelle de la connexion. 
> 
> Les événements **defaultcmd**, **defaultnumeric**, **defaultevent** et ***EOF*** sont obligatoires.
> 
> Le script est exécuté dans l'espace de noms de connexion (::IRCServices:: ...), qui peut tirer parti de plusieurs commandes (voir Commandes de rappel ci-dessous) pour faciliter l'analyse des données.
> 
> Les événements disponibles sont ceux  ci-dessous
#### Liste des events
- PRIVMSG
- JOIN
- PART
- NICK
- OPER
- QUIT
- SQUIT
- TOPIC
- WHOIS
- WHOWAS
- WHO
- NAMES
- NOTICE
- LIST
- INVITE
- KICK
- VERSION
- STATS
- LINKS
- TIME
- ERROR
- PONG
- CONNECT
- TRACE
- ADMIN
- INFO
- KILL
- AWAY
- REHASH
- RESTART
- SUMMON
- USERS
- WALLOPS
- USERHOST
- ISON
- SERVER

### net **eventget** <event> <script>
> Récupére la valeur de **event**
> Sans argument **eventget** affiche la liste des événements
> 
### net **eventexists** event script

Returns a boolean value indicating the existence of the event handler.

### [net](#ircservicesconnection) **connect** <Server_HostName> <[+]Server_Port> <Server_Password> [Server_Protocol] [Server_Name] [Server_ID]

#### Server_HostName
Informer **Server_HostName** avec le **nom de domaine réel** ou l'**IP** auquel le service doit se connecter.

#### Server_Port
Informer **Server_Port** avec le **PORT** du link services défini sur votre IRCD.
Si le **PORT** est précédé d'un **+** , la connexion est **sécurisée** par SSL et nécéssite la présence du **package tls** sur votre système.

#### Server_Password
La connexion du service au IRCD nécéssite un mot de passe, fournissez-le.

#### Server_Name
Si aucune valeur est fournie à **Server_Name**, il est defini sur **Extra-Cool.FR**

#### Server_Protocol (new/old)
Si aucune valeur est fournie à **Server_Protocol**, il est defini sur **1** et utilise le nouveau protocol IRC.

C Server_ID

Si **Server_ID** n'est pas défini, un ID aleatoire sera generé.

This causes the socket to be established. ::irc::connection created the namespace and the commands to be used, but did not actually open the socket. This is done here. NOTE: the older form of 'connect' did not require the user to specify a hostname and port, which were specified with 'connection'. That form is deprecated.

### net **config** [key] [value]

The same as ::irc::config but sets and gets options for the net connection only.
#### key
le nom de la clef à modifier
#### value
la valeur voulue pour la key
### net **log** level message

If logger is turned on by config this will write a log message at level.

### net **logname**

Returns the name of the logger instance if logger is turned on.

### net **connected**

Returns a boolean value indicating if this connection is connected to a server.

### net **sockname**

Returns a 3 element list consisting of the ip address, the hostname, and the port of the local end of the connection, if currently connected.

### net **peername**

Returns a 3 element list consisting of the ip address, the hostname, and the port of the remote end of the connection, if currently connected.

### net **socket**

Return the Tcl channel for the socket used by the connection.

### net **user** username localhostname localdomainname userinfo

Sends USER command to server. username is the username you want to appear. localhostname is the host portion of your hostname, localdomainname is your domain name, and userinfo is a short description of who you are. The 2nd and 3rd arguments are normally ignored by the IRC server.

### net **nick** nick

NICK command. nick is the nickname you wish to use for the particular connection.

### net **ping** target

Send a CTCP PING to target.

### net **serverping**

PING the server.

### net **join** channel ?key?

channel is the IRC channel to join. IRC channels typically begin with a hashmark ("#") or ampersand ("&").

### net **part** channel ?message?

Makes the client leave channel. Some networks may support the optional argument message

### net **quit** ?message?

Instructs the IRC server to close the current connection. The package will use a generic default if no message was specified.

### net **privmsg** target message

Sends message to target, which can be either a channel, or another user, in which case their nick is used.

### net **notice** target message

Sends a notice with message message to target, which can be either a channel, or another user, in which case their nick is used.

### net **ctcp** target message

Sends a CTCP of type message to target

### net **kick** channel target ?message?

Kicks the user target from the channel channel with a message. The latter can be left out.

### net **mode** target args

Sets the mode args on the target target. target may be a channel, a channel user, or yourself.

### net **topic** channel message

Sets the topic on channel to message specifying an empty string will remove the topic.

### net **invite** channel target

Invites target to join the channel channel

### net **send** text

Sends text to the IRC server.

### net **destroy**

Deletes the connection and its associated namespace and information.

## Callback Commands
These commands can be used within callbacks

### **who** ?address?

Returns the nick of the user who performed a command. The optional keyword address causes the command to return the user in the format "username@address".

### **action**

Returns the action performed, such as KICK, PRIVMSG, MODE, etc... Normally not useful, as callbacks are bound to a particular event.

### **target**

Returns the target of a particular command, such as the channel or user to whom a PRIVMSG is sent.

### **additional**

Returns a list of any additional arguments after the target.

### **header**

Returns the entire event header (everything up to the :) as a proper list.

### **msg**

Returns the message portion of the command (the part after the :).
