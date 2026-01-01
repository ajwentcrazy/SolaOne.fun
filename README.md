# SolaOne White Paper (French)

## 1. Introduction

**SolaOne** est une plateforme d'échecs en ligne "**Web2.5**" qui redéfinit les paris basés sur la **compétence**. 

**Contrairement** aux jeux de hasard traditionnels où la chance prédomine, **SolaOne** se concentre sur le **"Skill-to-Earn"**. La plateforme exploite la blockchain **Solana** pour les micro-transactions et une **architecture côté serveur robuste** pour garantir la **sécurité et le fair-play**, éliminant les problèmes de confiance dans les paris pairs à pairs.

Le jeu offre un environnement **sécurisé, instantané et équitable** permettant aux joueurs de **monétiser leurs compétences** aux échecs.

## 2. Fonctionnement

### 2.1 La Boucle de Jeu

SolaOne propose une **boucle de jeu simplifiée** conçue pour l'engagement et la fluidité, **similaire aux leaders de l'industrie** comme **Chess.com**, mais avec des enjeux élevés.

1. **Lobby et Configuration :** Les joueurs sélectionnent une cadence (Bullet 1|1, Blitz 5|5, Rapide 10|0) et un montant de mise ($1, $5, 10$).
2. **Matchmaking :** Le système met en relation le joueur avec un adversaire d'un niveau de compétence similaire.
3. **Le Match :** La partie se joue en temps réel. Les fonds sont conservés sous séquestre (escrow) par le serveur de jeu pendant le match.
4. **Règlement :** Immédiatement après l'Échec et Mat, l'Abandon ou le Temps Écoulé, le gagnant reçoit la cagnotte directement sur son portefeuille de jeu.
5. **Ajustement du Classement :** Les classements ELO des deux joueurs sont mis à jour dynamiquement en fonction du résultat du match.

### 2.2 Économie Financée par les Joueurs

SolaOne fonctionne sur un modèle de **jeu à somme nulle** (moins les frais de plateforme). Les gains sont **directement financés par la mise de l'adversaire**. La plateforme **ne parie pas** contre les joueurs ; elle facilite simplement l'échange sécurisé de valeur.

## 3. Fair-Play et Matchmaking

L'équité est la pierre angulaire de SolaOne. Nous mettons en œuvre des protocoles stricts pour garantir que chaque match est équitable.

1. **File d'Attente Basée sur l'ELO :** L'algorithme de matchmaking connecte strictement les joueurs dans une plage maximale de **50 points ELO**. Cela garantit une probabilité de victoire de 50/50 pour les deux parties.
2. **Validation Côté Serveur :** Le serveur agit comme l'arbitre faisant autorité. Chaque coup est validé par rapport aux règles FIDE des échecs avant d'être diffusé, empêchant les coups illégaux ou la manipulation côté client.

### 3.1 Anti-Smurfing et Anti-Triche

1. **Proof-of-History :** SolaOne utilise une vérification unique de "**Proof-of-History**". Les joueurs doivent **lier leur compte SolaOne à un compte Chess.com actif**. Cela est une **première couche de protection** envers les joueurs de hauts niveau qui créer de nouveaux comptes "débutants" pour s'attaquer aux joueurs plus faibles. 
2. **Statistiques des joueurs :** Les statistiques que le serveur récupère en continue permettent d’établir quels joueurs est suceptible d’être un smurf ou un tricheur.

## 4. Architecture

SolaOne est construit sur une **Architecture Hybride** (Web2.5) haute performance, combinant la vitesse des serveurs centralisés avec la sécurité de la finance décentralisée.

### 4.1 Intégrations **Third-Party**

SolaOne intègre des **services standard de l'industrie**:
La plateforme utilise un service tiers pour assurer l’authentification des utilisateurs.

Pour **interagir** avec la blockchain pour la création de portefeuilles et les transferts de fonds, la plateforme utilise **RPC Solana**. Et d’autres services tiers permettent de récolter le taux de change du token Solana en temps réel, 

### 4.2 Logique du Serveur de Confiance

Le backend sert de **Source de Vérité**.

- Il maintient l'état officiel du jeu (chaînes FEN).
- Il gère les horloges officielles du jeu, compensant le décalage réseau.
- Il détecte les déconnexions et résout automatiquement les parties abandonnées.

### 4.3 Performances et Stockage

Nous utilisons une **base de données en mémoire** pour les données chaudes (parties actives, coups) et une **base de données persistante** pour le stockage froid (historique des matchs, journaux financiers).

## 5. Web3 et Intégration Solana

Nous avons choisi la **Blockchain Solana** pour ses avantages spécifiques : des **frais de transaction extrêmement bas** (< 0,001 $) et un **débit élevé** (TPS), ce qui en fait l’une des seules chaînes viables pour les micro-paris.

### 5.1 Logique de Transaction et Séquestre

- **Portefeuilles de Jeu Gérés :** Pour offrir une Expérience Utilisateur fluide, SolaOne génère un portefeuille non custodial dérivé pour chaque session utilisateur. Les clés privées sont uniquement géré par les serveurs. Cela permet aux serveurs de signer **automatiquement** les transactions liées au jeu **sans besoin de confiance** envers l’utilisateur.
- **Flux :**
    - **Avant-Jeu :** Les utilisateurs déposent des SOL sur leur portefeuille de jeu.
    - **Après-Jeu :** La logique calcule le résultat. Les serveurs déclenche une transaction blockchain transférant 90 % du pot au gagnant et 10 % à la trésorerie de la plateforme.d

### 5.2 Transparence Économique

- **Paiements :** Tous les paiements sont exécutés on-chain et sont vérifiables via n'importe quel explorateur Solana.
- **Commission de Plateforme :** SolaOne facture des frais transparents sur les gains pour financer les coûts des serveurs et le développement (10%).
- **Ségrégation des Fonds :** Les fonds des joueurs sont mathématiquement ségrégués des fonds de la plateforme grâce à l'architecture de portefeuille dérivé.

## 6. Architecture de Sécurité

La sécurité est mise en œuvre via une stratégie de "Défense en Profondeur".

- **Validation Côté Serveur :** Ne jamais faire confiance au client. Le serveur vérifie chaque entrée (légalité des coups, messages de chat, montants des paris).
- **Gestion des Identités :** Un mappage strict entre les identifiants Google, les UUID internes et les portefeuilles Solana empêche l'usurpation d'identité.
- **Anti-Triche :**
    - **Niveau Protocole :** Les messages WebSocket ne contiennent pas d'identifiants utilisateur ; le serveur déduit l'identité à partir de la session sécurisée, empêchant les attaques par usurpation.
    - **Niveau Jeu :** Analyse par moteur pour détecter l'assistance par ordinateur.
- **Protection des Portefeuilles :** Le serveur crée des signatures dans un environnement sécurisé et isolé. Les fonds des utilisateurs sont protégés contre la manipulation pendant le jeu car le frontend (client) n'a aucun accès au matériel de clé privée.

## 7. Conclusion

SolaOne représente la prochaine évolution des jeux de société en ligne. En supprimant la friction des paiements et en assurant un environnement sans triche grâce à des choix architecturaux rigoureux, nous offrons un terrain de jeu où la compétence est la seule monnaie qui compte.
