# SAÉ 5.02 : Déploiement d'une infrastructure IT conteneurisée avec Ansible

## 📌 Présentation du Projet
Ce projet consiste à automatiser le déploiement complet d'une infrastructure de gestion et de supervision IT. L'ensemble des services est déployé sous forme de **conteneurs Docker**, orchestrés et configurés via **Ansible**.

**Réseau virtuel dédié :** `sae502_saubin`

---

## 🏗 Architecture des Conteneurs

| Conteneur | Services | Fonctions |
| :--- | :--- | :--- |
| **nodes-manager** | Ansible CLI, SSH, Docker | Nœud de contrôle : lancement des playbooks |
| **mariadb** | MariaDB | Bases de données pour GLPI et Centreon |
| **glpi-web** | Apache2, PHP, GLPI | Gestion de parc et inventaire |
| **centreon-master** | Centreon Web, Broker | Interface de supervision et gestion SQL |
| **centreon-collector** | Centreon Engine, SNMP | Collecte des données de supervision |
| **web-test** | Apache2, SNMPD | Hôte supervisé (Tests HTTP, CPU, RAM) |
| **backup** | rsync, Cron | Sauvegarde automatisée des données |

---

## 🤖 Automatisation — Ansible

Le déploiement est piloté par le playbook global : `sae502-saubin.yml`.

### Rôles principaux :
* **common** : Préparation système, mises à jour et SSH.
* **mariadb** : Initialisation des bases `glpidb` et `centreon`.
* **glpi** : Déploiement de la pile LAMP + application GLPI.
* **snmp_agent** : Configuration de SNMPD sur les hôtes à superviser.
* **centreon_*** : Installation Master/Collector et liaison Broker.
* **backup_rsync** : Automatisation des sauvegardes via rsync.

---

## 📋 Déroulement du Déploiement
1.  **Infrastructure** : Création du réseau et des conteneurs via Ansible.
2.  **Base de données** : Configuration de MariaDB et des utilisateurs.
3.  **Gestion & Supervision** : Déploiement de GLPI et de la stack Centreon (Master/Collector).
4.  **Test & Supervision** : Mise en place du serveur web de test et configuration des checks SNMP.
5.  **Sauvegarde** : Activation du système de backup `rsync` pour les configurations et fichiers critiques.

---

## 🎯 Résultats Attendus
- [ ] Déploiement 100% automatique via Ansible.
- [ ] Instance GLPI opérationnelle.
- [ ] Supervision Centreon active (Master + Collecteur).
- [ ] Serveur `web-test` supervisé via SNMP.
- [ ] Sauvegardes rsync fonctionnelles (Configs & Données).

**Estimation de charge :** ~50 heures

---
## 📝 Auteur
* **SaubinT** - [BUT RT3 / C2]
* **Dépôt Git :** [https://github.com/SaubinT/SAE502](https://github.com/SaubinT/SAE502)
