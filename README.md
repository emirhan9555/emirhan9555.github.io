# emirhan9555.github.io

# Creating a complete GitHub-style portfolio folder for the user and zipping it.
import os, zipfile, textwrap, pathlib, json

base = "/mnt/data/bts-sio-e5-portfolio-Ekizceli-Emirhan"
os.makedirs(base, exist_ok=True)

# Helper to write files
def write(path, content, mode="w"):
    os.makedirs(os.path.dirname(path), exist_ok=True)
    with open(path, mode, encoding="utf-8") as f:
        f.write(content)

# Basic README
readme = f"""# Portfolio E5 – BTS SIO SISR - EKIZCELI Emirhan

Ce dépôt contient le portfolio réalisé pour l'épreuve E5 du BTS SIO option SISR.
Auteurs : EKIZCELI Emirhan

Structure prête à être poussée sur GitHub. Les dossiers contiennent : contexte, objectifs, étapes techniques, scripts et preuves à ajouter.

---
Arborescence importante :
- /dossiers/ : dossiers professionnels (7)
- /veille/ : veille technologique (thème : L'IA dans la détection des cyberattaques)
- /table-synthese.md : tableau récapitulatif
"""

write(f"{base}/README.md", readme)

# Table synthese
table = textwrap.dedent("""\
# Tableau de synthèse - E5 BTS SIO SISR

| N° | Sujet | Compétences | Durée (h) | Livrables |
|---:|---|---|---:|---|
| 1 | DHCP / DNS | Admin réseau, configuration DNS/DHCP | 8 | scripts, fichiers de zone, captures |
| 2 | Active Directory | Admin Windows, PowerShell | 10 | scripts PS, captures AD |
| 3 | Proxmox & VM | Virtualisation, cloud-init | 6 | cloud-init, scripts qm |
| 4 | Service web conteneurisé | Docker, nginx, docker-compose | 6 | docker-compose.yml, pages web |
| 5 | Sauvegarde automatisée | Stratégies de sauvegarde, scripts | 5 | scripts borg, logs |
| 6 | Supervision & alerting | Prometheus, Grafana, monitoring | 10 | prometheus.yml, dashboards |
| 7 | Automatisation (Ansible) | Orchestration, playbooks | 8 | playbook, inventaire |
""")
write(f"{base}/table-synthese.md", table)

# Veille technologique - personalized theme
veille = textwrap.dedent("""\
# Veille technologique - L'IA dans la détection des cyberattaques

**Auteur :** EKIZCELI Emirhan
**Thème :** L'IA et l'apprentissage automatique appliqués à la détection des cyberattaques (2024-2025)

## Objectif
Présenter des techniques, outils et bonnes pratiques d'intégration de modèles d'IA pour détecter des comportements malveillants (anomalies réseau, détection d'intrusions, détection de phishing, etc.) et proposer un plan d'expérimentation en laboratoire.

## Sujets suivis
- Détection d'anomalies (unsupervised learning, autoencodeurs)
- Classification des événements (supervised learning, Random Forest, XGBoost)
- Analyses comportementales (User and Entity Behavior Analytics - UEBA)
- Fusion SIEM + modèles ML (ex : Elastic SIEM, Splunk, Wazuh)
- Utilisation de pipelines ML pour l'entrainement et le déploiement (MLflow, Kubeflow)

## Méthodologie de veille
1. Lecture d'articles et whitepapers 2x par semaine.  
2. Tests en laboratoire sur datasets publics (CIC-IDS, UNSW-NB15...) et jeux de données synthétiques.  
3. Développement d'un petit prototype de démonstration (collecte -> feature engineering -> modèle -> alerting).

## Sources (exemples à consulter)
- Articles académiques et conférences (IEEE, Usenix, ACM)
- Blogs sécurité : Elastic, Cisco Talos, SANS
- Repositories GitHub sur détection d'anomalies et SIEM integrations
- Datasets : CIC-IDS-2017, UNSW-NB15, NSL-KDD

## Plan d'expérimentation (bref)
1. Collecte logs réseau (pcap) + logs systèmes.  
2. Prétraitement & extraction de features réseau (flows, durées, ports, flags).  
3. Entraînement d'un autoencodeur pour repérer anomalies.  
4. Création d'une pipeline qui génère alertes vers une plateforme de supervision (Grafana + Prometheus alertmanager ou via Webhook vers Slack).

---
(Compléter avec notes de lecture et preuves lors de la réalisation)
""")
write(f"{base}/veille/veille-technologique.md", veille)
write(f"{base}/veille/sources.txt", "CIC-IDS-2017\nUNSW-NB15\nElastic blog\nCisco Talos\nSANS Institute\n")

# Create 7 dossiers with dossier.md and scripts/examples
dossiers = [
    ("01-dhcp-dns", "Déploiement d'un serveur DHCP/DNS (Bind9)"),
    ("02-active-directory", "Installation et gestion d'Active Directory (Windows Server)"),
    ("03-proxmox", "Virtualisation et gestion de VM (Proxmox)"),
    ("04-docker-web", "Service Web conteneurisé (NGINX + Docker Compose)"),
    ("05-sauvegarde", "Stratégie de sauvegarde automatisée (BorgBackup)"),
    ("06-supervision", "Supervision et alerting (Prometheus + Grafana)"),
    ("07-ansible", "Automatisation avec Ansible (playbook infra)"),
]

for idx, (folder, title) in enumerate(dossiers, start=1):
    dirpath = f"{base}/dossiers/{folder}"
    os.makedirs(dirpath, exist_ok=True)
    # dossier.md content
    dossier_md = f"# Dossier professionnel {idx:02d} – {title}\n\n" \
                 f"**Auteur :** EKIZCELI Emirhan\n\n" \
                 "## 1. Contexte\n\n" \
                 "Décrire le contexte professionnel ou de stage.\n\n" \
                 "## 2. Objectifs\n\n" \
                 "- Objectif 1\n- Objectif 2\n\n" \
                 "## 3. Compétences E5 mobilisées\n\n" \
                 "- Administration système\n- Gestion de services réseau\n- Documentation & preuves\n\n" \
                 "## 4. Architecture\n\n" \
                 "Ajouter un schéma ou description.\n\n" \
                 "## 5. Réalisation technique\n\n" \
                 "Étapes détaillées, commandes et explications.\n\n" \
                 "## 6. Scripts / fichiers\n\n" \
                 "Voir le dossier `scripts/`.\n\n" \
                 "## 7. Preuves\n\n" \
                 "- Captures d'écran\n- Logs\n- Résultats de tests\n\n" \
                 "## 8. Bilan\n\n" \
                 "Points forts, difficultés, améliorations possibles.\n"
    write(f"{dirpath}/dossier.md", dossier_md)

# Add example scripts for each folder
# 01 DHCP/DNS
dhcp_install = textwrap.dedent("""\
#!/bin/bash
# Install Bind9 and ISC DHCP server (Debian/Ubuntu)
apt update
apt install -y bind9 isc-dhcp-server

cat > /etc/dhcp/dhcpd.conf <<'EOF'
option domain-name "ekizceli.local";
option domain-name-servers 192.168.10.10;
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.10.0 netmask 255.255.255.0 {
  range 192.168.10.100 192.168.10.200;
  option routers 192.168.10.1;
}
EOF

cat > /etc/bind/db.ekizceli.local <<'EOF'
$TTL 604800
@ IN SOA ns1.ekizceli.local. admin.ekizceli.local. (
    2025112101 ; Serial
    604800
    86400
    2419200
    604800 )
@ IN NS ns1.ekizceli.local.
ns1 IN A 192.168.10.10
www IN A 192.168.10.20
EOF

systemctl restart bind9 isc-dhcp-server
echo \"DHCP & DNS installed. Update zone files as needed.\"
""")
write(f"{base}/dossiers/01-dhcp-dns/scripts/install.sh", dhcp_install)
write(f"{base}/dossiers/01-dhcp-dns/scripts/dhcpd.conf", "## Exemple de dhcpd.conf - adapter selon réseau\n")
write(f"{base}/dossiers/01-dhcp-dns/scripts/db.ekizceli.local", "$TTL 604800\n...")

# 02 Active Directory - PowerShell sample
ad_ps = textwrap.dedent("""\
# PowerShell script sample to install AD DS and create a user (run as Administrator)
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
Import-Module ADDSDeployment
# Example: Install-ADDSForest -DomainName "ekizceli.local" -SafeModeAdministratorPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force)
# Create a user
# New-ADUser -Name "Ekizceli Emirhan" -GivenName Emirhan -Surname Ekizceli -SamAccountName eekizceli -AccountPassword (ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force) -Enabled $true
""")
write(f"{base}/dossiers/02-active-directory/scripts/create_user.ps1", ad_ps)

# 03 Proxmox - cloud-init example
cloudinit = textwrap.dedent("""\
#cloud-config
users:
  - name: ekizceli
    sudo: ALL=(ALL) NOPASSWD:ALL
    ssh-authorized-keys:
      - ssh-rsa AAAAB3NzaC1...yourkey
chpasswd:
  list: |
    ekizceli:Password123
  expire: False
package_update: true
packages:
  - htop
  - git
""")
write(f"{base}/dossiers/03-proxmox/scripts/cloud-init.yaml", cloudinit)

# 04 Docker Web - docker-compose example
docker_compose = textwrap.dedent("""\
version: '3.8'
services:
  web:
    image: nginx:stable
    volumes:
      - ./www:/usr/share/nginx/html:ro
    networks:
      - webnet
  reverse:
    image: jwilder/nginx-proxy
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
    networks:
      - webnet
networks:
  webnet:
    driver: bridge
""")
write(f"{base}/dossiers/04-docker-web/scripts/docker-compose.yml", docker_compose)
write(f"{base}/dossiers/04-docker-web/scripts/www/index.html", "<html><body><h1>Portfolio E5 - Ekizceli Emirhan</h1></body></html>")

# 05 Sauvegarde - backup script borg example
backup_sh = textwrap.dedent("""\
#!/bin/bash
# Exemple basique de script de sauvegarde avec borg
REPO=/srv/backup/borg
export BORG_PASSPHRASE='ChangeMePassphrase'
borg init --encryption=repokey $REPO || true
borg create --stats $REPO::\"{hostname}-{now:%Y-%m-%d}\" /etc /home || true
borg prune -v --list $REPO --keep-daily=7 --keep-weekly=4 --keep-monthly=6 || true
""")
write(f"{base}/dossiers/05-sauvegarde/scripts/backup.sh", backup_sh)

# 06 Supervision - docker-compose for prometheus+grafana basic
prom_compose = textwrap.dedent("""\
version: '3.8'
services:
  prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - 9090:9090
  grafana:
    image: grafana/grafana
    ports:
      - 3000:3000
""")
prom_yml = textwrap.dedent("""\
scrape_configs:
  - job_name: 'node'
    static_configs:
      - targets: ['node_exporter:9100']
""")
write(f"{base}/dossiers/06-supervision/scripts/docker-compose.yml", prom_compose)
write(f"{base}/dossiers/06-supervision/scripts/prometheus.yml", prom_yml)

# 07 Ansible - simple playbook
ansible_playbook = textwrap.dedent("""\
- hosts: webservers
  become: true
  tasks:
    - name: Installer nginx
      apt:
        name: nginx
        state: present
    - name: Copier fichier index
      copy:
        content: '<html><body><h1>Deployed via Ansible</h1></body></html>'
        dest: /var/www/html/index.html
      notify: Restart nginx
  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted
""")
write(f"{base}/dossiers/07-ansible/scripts/site.yml", ansible_playbook)

# Create a license file and .gitignore
write(f"{base}/LICENSE", "CC BY-NC-SA 4.0 - Portfolio created by EKIZCELI Emirhan\n")
write(f"{base}/.gitignore", ".DS_Store\n__pycache__/\n")

# Create a small images folder with a placeholder
write(f"{base}/images/placeholder.txt", "Ajouter captures d'écran ici.\n")

# Create a simple portfolio PDF placeholder (text file) to indicate optional PDF
write(f"{base}/portfolio_notes.txt", "Générer PDF via pandoc / LibreOffice si nécessaire.")

# Now zip the folder
zip_path = "/mnt/data/portfolio_Ekizceli_Emirhan.zip"
def zipdir(path, ziph):
    for root, dirs, files in os.walk(path):
        for file in files:
            full = os.path.join(root, file)
            arcname = os.path.relpath(full, os.path.dirname(path))
            ziph.write(full, arcname)

with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zf:
    zipdir(base, zf)

zip_path

