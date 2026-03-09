

# 0 - 1ère phrase


Pour quelqu’un qui maîtrise Docker et les services Linux, ce lab est plutôt simple.

C'était l'un de mes premiers projet réseaux.

J'ai commencé par une architecture simple pour déjà bien appréhender la segmentation et faire une analyse rapide de ports exposés.



Pour ton lab, le BTU = montrer que tu comprends l’architecture réseau et la sécurité d’infrastructure
Segmentation DMZ/Internal
Services isolés mais fonctionnels
Scan de surface d’attaque


# 3 - Étapes pour renforcer l’architecture



1️⃣ Ajouter un firewall simple

Sur le host ou sur le conteneur

Exemple : bloquer le SSH ou limiter l’accès à NGINX

iptables -A INPUT -p tcp --dport 22 -j DROP

Explique dans le README que tu simules une politique de filtrage réseau

2️⃣ Ajouter un conteneur “client” pour tester le réseau

Simuler un scanner ou un attaquant

Exemple : un conteneur Ubuntu qui fait :

nmap -sV web_server

Montre que tu sais tester la sécurité d’une infra

3️⃣ Logs et supervision

Active les logs NGINX

Regarde les logs LDAP

Explique comment tu peux détecter un problème ou une attaque

4️⃣ Segmentation stricte

Connecter le conteneur client à DMZ mais pas à Internal

Vérifier que LDAP n’est pas accessible depuis DMZ → montre la sécurité réelle

5️⃣ Optionnel mais impressionnant

Fail2ban pour bloquer tentatives SSH

Reverse proxy pour exposer plusieurs services sur le même port

Simulation d’attaque interne (ping, scan)

4️⃣ Le “BTU” (Back To User / But Technique / Brièvement)


