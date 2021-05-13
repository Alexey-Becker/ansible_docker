Voraussetzung:
- Installatierte Ubuntu 20.04
- Erreichbarkeit über netzwerk SSH
- User mit SUDO Rechte
- In der Datei "./hosts.txt" die IP Adressen anpassen.
  Hier dürfen mehrere Systeme hinterlegt werden, dann erfolgt die Installation automatisiert auf mehreren Systemen.
- In der Datei "./gorup_vars/DOCKER_SERVER" den Parameter "ansible_ssh_private_key_file" anpassen.
  Hier den Pfad zu eigenem SSH private Key hinterlegen.
- In der Datei "./playbook_create_docker_user.yml" den Parameter "key" unter "autorized_key" anpassen.
  Hier den Pfad zu eigenem SSH private Key hinterlegen.

Reihenfolge:
1. SSH Key auf dem remote Host ohne Docker User hinterlegen.
Hier die richtige IP Adresse des Zielsystems einsetzen.

--
ssh-copy-id user@192.168.x.x
--

1.1 Prüfen ob man sich ohne EIngabe des Kennworts per SSH anmelden kann.
Hier die richtige IP Adresse des Zielsystems einsetzen.

--
ssh user@192.168.x.x
--

2. Docker User mit SUDO Rechte erstellen, SSH Key hinterlegen.
Hier wird Benutzer "docker" mit Passwort "docker" angelegt.
!!! bei dem Befehl muss das Kennwort des "user" eingegeben werden. !!!

--
ansible-playbook playbook_create_docker_user.yml -K
--

3. Installation Docker und Docker-Compose mittel einer Rolle.
Ausführung wird mit dem User "docker" gestartet.
Hier muss das Kennwort "docker" für SUDO eigegeben werden.

-- 
ansible-playbook playbook_install_docker_role.yml -K
--
