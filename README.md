# SolaOne White Paper

## 1. Introduction

**SolaOne** is an online chess platform "**Web2.5**" that redefines **skill-based betting**.

**Unlike** traditional gambling games where luck dominates, **SolaOne** focuses on **"Skill-to-Earn"**. The platform leverages the **Solana blockchain** for micro-transactions and a **robust server-side architecture** to ensure **security and fair play**, eliminating trust issues in peer-to-peer betting.

The game provides a **secure, instant, and fair** environment that allows players to **monetize their chess skills**.

## 2. Functioning

### 2.1 The Game Loop

SolaOne offers a **simplified game loop** designed for engagement and fluidity, **similar to industry leaders** like **Chess.com**, but with high stakes.

1. **Lobby and Setup:** Players select a time control (Bullet 1|1, Blitz 5|5, Rapid 10|0) and a stake amount ($1, $5, $10).
2. **Matchmaking:** The system pairs the player with an opponent of similar skill level.
3. **The Match:** The game is played in real-time. Funds are held in escrow by the game server during the match.
4. **Settlement:** Immediately after Checkmate, Resignation, or Time Expired, the winner receives the pot directly in their game wallet.
5. **Rating Adjustment:** Both players' ELO ratings are dynamically updated based on the match result.

### 2.2 Player-Funded Economy

SolaOne operates on a **zero-sum game model** (minus platform fees). Winnings are **directly funded by the opponent's stake**. The platform **does not bet** against players; it merely facilitates the **secure exchange of value**.

## 3. Fair Play and Matchmaking

Fairness is the cornerstone of SolaOne. We implement strict protocols to ensure that every match is fair.

1. **ELO-Based Queue:** The matchmaking algorithm strictly connects players within a maximum range of **50 ELO points**. This ensures a 50/50 chance of winning for both parties.
2. **Server-Side Validation:** The server acts as the authoritative referee. Each move is validated against FIDE chess rules before being broadcast, preventing illegal moves or client-side manipulation.

### 3.1 Anti-Smurfing and Anti-Cheating

1. **Proof-of-History:** SolaOne uses a unique **"Proof-of-History"** verification. Players must **link their SolaOne account to an active Chess.com account**. This is a **first layer of protection** against high-level players creating new "beginner" accounts to target weaker players.
2. **Player Statistics:** Continuously collected server statistics help determine which players are likely smurfs or cheaters.

## 4. Architecture

SolaOne is built on a **High-Performance Hybrid Architecture** (Web2.5), combining the speed of centralized servers with the security of decentralized finance.

### 4.1 Third-Party Integrations

SolaOne integrates **industry-standard services**:
The platform uses a third-party service for user authentication.

To **interact** with the blockchain for wallet creation and fund transfers, the platform uses **Solana RPC**. Other third-party services provide real-time exchange rates for the Solana token.

### 4.2 Trusted Server Logic

The backend serves as the **Source of Truth**.

* It maintains the official game state (FEN strings).
* It manages official game clocks, compensating for network latency.
* It detects disconnections and automatically resolves abandoned games.

### 4.3 Performance and Storage

We use an **in-memory database** for hot data (active games, moves) and a **persistent database** for cold storage (match history, financial logs).

## 5. Web3 and Solana Integration

We chose the **Solana Blockchain** for its specific advantages: **extremely low transaction fees** (< $0.001) and **high throughput** (TPS), making it one of the few viable chains for micro-betting.

### 5.1 Transaction and Escrow Logic

* **Managed Game Wallets:** To provide a smooth User Experience, SolaOne generates a non-custodial wallet derived for each user session. Private keys are only managed by the servers. This allows servers to **automatically** sign game-related transactions **without requiring trust** from the user.
* **Flow:**

  * **Pre-Game:** Users deposit SOL into their game wallet.
  * **Post-Game:** The logic calculates the result. Servers trigger a blockchain transaction transferring 90% of the pot to the winner and 10% to the platform treasury.

### 5.2 Economic Transparency

* **Payments:** All payments are executed on-chain and verifiable via any Solana explorer.
* **Platform Fee:** SolaOne charges transparent fees on winnings to cover server costs and development (10%).
* **Segregation of Funds:** Player funds are mathematically segregated from platform funds through the derived wallet architecture.

## 6. Security Architecture

Security is implemented via a "Defense in Depth" strategy.

* **Server-Side Validation:** Never trust the client. The server verifies every input (move legality, chat messages, bet amounts).
* **Identity Management:** Strict mapping between Google IDs, internal UUIDs, and Solana wallets prevents identity spoofing.
* **Anti-Cheating:**

  * **Protocol Level:** WebSocket messages do not contain user identifiers; the server infers identity from the secure session, preventing spoofing attacks.
  * **Game Level:** Engine-based analysis detects computer assistance.
* **Wallet Protection:** The server creates signatures in a secure, isolated environment. User funds are protected from manipulation during the game as the frontend (client) has no access to private key hardware.

## 7. Conclusion

SolaOne represents the next evolution of online board games. By removing payment friction and ensuring a cheat-free environment through rigorous architectural choices, we offer a playground where skill is the only currency that matters.




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
