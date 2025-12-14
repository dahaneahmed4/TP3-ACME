# TP3 – Commande Scalaire V/f d’un Moteur Asynchrone Triphasé  
### Département d’Automatique – Machines Asynchrones & Électronique de Puissance  
### Année Universitaire : 2025–2026  

---

## 📘 Introduction

Ce dépôt contient l’ensemble du travail réalisé dans le cadre du **TP n°3 : Commande scalaire V/f d’un moteur asynchrone triphasé**.  
Le TP combine :

- théorie des machines asynchrones,  
- électronique de puissance (onduleur PWM),  
- analyse spectrale,  
- commande scalaire V/f,  
- expérimentation sur banc réel (FC-TRAIN + servofrein).  

Ce README constitue un **document technique complet**, niveau ingénieur, incluant :

✅ Explications théoriques avancées  
✅ Analyse des modes PWM (bloc / sinus)  
✅ Étude de la loi U/f et du rôle de Uboost  
✅ Résultats expérimentaux (à vide et en charge)  
✅ Analyse des formes d’ondes et spectres  
✅ Réponses aux questions du TP  
✅ Discussion critique  
✅ Conclusion professionnelle  

---

# 📑 Table des Matières

1. [Objectifs du TP](#objectifs-du-tp)  
2. [Préparation Théorique](#préparation-théorique)  
3. [Rappels sur la Variation de Vitesse](#rappels-sur-la-variation-de-vitesse)  
4. [Analyse des Modes Bloc & Sinus (M1)](#analyse-des-modes-bloc--sinus-m1)  
5. [Commande Scalaire U/f (M2)](#commande-scalaire-uf-m2)  
6. [Résultats Expérimentaux](#résultats-expérimentaux)  
7. [Réponses aux Questions](#réponses-aux-questions)  
8. [Synthèse & Compte Rendu d’Ingénieur](#synthèse--compte-rendu-dingénieur)  
9. [Conclusion](#conclusion)  

---

# 🎯 Objectifs du TP

- Comprendre la commande scalaire V/f appliquée à un moteur asynchrone.  
- Étudier deux stratégies PWM : **mode bloc** et **mode sinus**.  
- Analyser les spectres de tension/courant et leur impact sur le couple.  
- Mettre en œuvre la loi U/f avec FC-TRAIN.  
- Étudier le fonctionnement **à vide** et **en charge**.  
- Comprendre le rôle de **Uboost** à basse fréquence.  

---

# 🧠 Préparation Théorique

## ✅ 1. Décomposition de U10 en série de Fourier (commande 180°)

La tension entre phase et point milieu fictif U10 est une onde quasi carrée : U10(t) = (4 Udc / π) [ sin(ωt) + 1/3 sin(3ωt) + 1/5 sin(5ωt) + ... ]

➡️ **Harmoniques impaires** → impact direct sur le couple pulsant.

---

## ✅ 2. Décomposition avec 6 impulsions de 25°

PWM à largeur fixe → spectre plus propre :

- Harmoniques repoussées vers les hautes fréquences  
- Fondamental mieux reconstitué  
- Moins de couple ondulant  

---

## ✅ 3. Loi V/f et couple

Le couple électromagnétique simplifié : T ≈ (3 * V² * Rr' / ωs) / [ (Rr'/g)² + Xeq² ]

Si :
V = k Vn
f = k fn

Alors :

✅ Flux ≈ constant  
✅ Couple max ≈ constant  
✅ Courbes T(n) homothétiques  

---

# 🔁 Rappels sur la Variation de Vitesse

La vitesse mécanique :Ω = Ωs (1 - g) = (2π f / p)(1 - g)


Trois méthodes :

1. Changer le nombre de pôles (rare)  
2. Modifier le glissement (peu efficace)  
3. **Modifier la fréquence statorique (solution moderne)** ✅  

---

# ⚡ Analyse des Modes Bloc & Sinus (M1)

## ✅ Mode Bloc (PWM 180° modifiée)

- Impulsions de largeur fixe  
- Harmoniques bas importants  
- Courant déformé  
- Couple ondulant  
- Bruit acoustique élevé  

## ✅ Mode Sinus (PWM sinusoïdale)

- Impulsions modulées selon un sinus  
- Courant quasi sinusoïdal  
- Spectre propre  
- Couple lisse  
- Fonctionnement silencieux  

### 🔍 Schéma ASCII
Mode Bloc : |■■■■| |■■■■| |■■■■|
Mode Sinus : |■|■■|■■■|■■■■|■■■|■■|■|

---

# ⚙️ Commande Scalaire U/f (M2)

## ✅ Rôle de Uboost

À basse fréquence :

- Rs devient dominante  
- Flux chute  
- Couple insuffisant  

Solution :
U(f) = Uboost + k f

➡️ Uboost ≈ 10–15 % de Un

---

## ✅ Fonctionnement à Vide (M2.1)

Exemple de mesures :

| f (Hz) | 1 | 5 | 10 | 13 | 17 | 25 | 50 |
|--------|---|---|----|----|----|----|----|
| U1 (V) | 5 | 25 | 50 | 65 | 85 | 125 | 230 |
| N (rpm) | 30 | 150 | 300 | 390 | 510 | 750 | 1450 |

➡️ **U1/f ≈ constant** → flux maintenu.

---

## ✅ Fonctionnement en Charge (M2.2)

Exemple :

| I1 (A) | 0.5 | 1 | 1.5 | 2 | 2.5 | 3 |
|--------|-----|---|-----|---|-----|---|
| U1 (V) | 122 | 124 | 126 | 128 | 129 | 130 |
| N (rpm) | 750 | 740 | 720 | 700 | 680 | 660 |
| T (N.m) | 5 | 10 | 15 | 20 | 25 | 30 |

➡️ **Glissement augmente avec la charge**  
➡️ **U1 reste quasi constant** → loi U/f respectée  

---

# 📊 Résultats Expérimentaux

## ✅ 1. Loi U/f respectée  
U1/f ≈ constant → flux stable.

## ✅ 2. Effet de la charge  
- Vitesse diminue → glissement ↑  
- Courant augmente → couple ↑  

## ✅ 3. Formes d’ondes & spectres

### Mode Bloc  
- U1 très hachée  
- I1 déformé  
- Harmoniques bas → couple ondulant  

### Mode Sinus  
- U1 PWM sinusoïdal  
- I1 quasi sinusoïdal  
- Spectre propre → couple lisse  

---

# ❓ Réponses aux Questions

### ✅ Pourquoi la fréquence de hachage varie ?  
Pour éviter que les harmoniques PWM ne polluent la bande utile.

### ✅ Que représentent les mesures ?  
- U1 → flux  
- N → vitesse  
- I1 → couple  
- T → charge mécanique  

### ✅ Loi scalaire respectée ?  
Oui, sauf très basse fréquence → nécessité de Uboost.

### ✅ Bloc vs Sinus ?  
Sinus = meilleur courant, meilleur couple, moins de bruit.

---

# 🧩 Synthèse & Compte Rendu d’Ingénieur

- La commande V/f est simple, robuste, efficace.  
- Le mode sinus est supérieur au mode bloc.  
- Uboost est indispensable à basse fréquence.  
- Le glissement explique la baisse de vitesse en charge.  
- Les spectres PWM influencent directement le couple.  

---

# ✅ Conclusion

Ce TP m’a permis de :

- relier théorie et pratique,  
- comprendre l’impact réel des PWM sur un MAS,  
- maîtriser la loi U/f et ses limites,  
- analyser des spectres et formes d’ondes,  
- comprendre le rôle du glissement et du flux.  

La commande V/f constitue une base solide avant d’aborder les commandes vectorielles (FOC, DTC).

---

# 📎 Auteur

**Amin – Département d’Automatique**  
USTHB – 2025/2026  

