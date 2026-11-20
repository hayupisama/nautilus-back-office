# CLAUDE.md — nautilus-back-office

## Rôle

Interface de l'administrateur : validation des chauffeurs (documents, registre VTC, attestation de formation PMR), suivi des courses et incidents, modération et suspensions, alertes d'expiration de documents.

## État

Dépôt vide. Première tâche : `ng new nautilus-back-office --routing --style=scss --standalone` puis `ng add @angular/material`.

## Règles

- Composants standalone, signals, nouveau control flow (`@if`, `@for`).
- Client API : généré (openapi-generator `typescript-angular`) depuis le contrat, dans `src/app/api/`, jamais édité à la main.
- Authentification : Keycloak (OIDC, Authorization Code + PKCE), rôle `admin` requis.
- Accessibilité WCAG 2.2 AA : Angular Material + vérification axe-core dans les tests.
- Toute action de validation ou de suspension doit afficher et confirmer son motif (il est journalisé côté API).

## Contexte projet (commun)

- Projet : **Nautilus** (nom de code), appli VTC marketplace dédiée aux PMR, lancement à Nantes (métropole + aéroport + gare).
- Side project, développeur unique, budget quasi nul, < 5 h/semaine, démarrage janvier 2027.
- Référence fonctionnelle : `nautilus/docs/cahier-des-charges.md`. Glossaire : `nautilus/docs/glossaire.md`. Décisions transverses : `nautilus/docs/decisions.md`.
- Lot en cours : **lot 0 – prototype** avec données fictives. Objectif : un prototype fonctionnel et démontrable. La validation terrain est faite par un autre intervenant.
- Licence : PolyForm Noncommercial 1.0.0. Ne jamais ajouter de dépendance dont la licence interdit cet usage.

## Règles transverses

- Langue : identifiants de code en anglais (voir glossaire FR -> EN) ; docs, commits et messages à l'utilisateur en français.
- Commits : Conventional Commits.
- Mode de travail : Claude développe seul et pilote le projet en Scrum autogéré. Fouad est le client (MOA/MOE) : il supervise et teste, il ne lit pas les tickets. Processus complet : `nautilus/.claude/scrum/PROCESS.md` (à lire avant toute action sur le backlog).
- Autonomie : branches, commits, push de branches, PR, fusion après CI verte, gestion des issues et du tableau de projet sont autorisés sans demander. Demander à Fouad avant : déploiement en production, secret ou service payant, publication sur les stores, opération destructive (force push, suppression), changement de périmètre ou de règle métier du cahier des charges.
- Accessibilité WCAG 2.2 AA obligatoire sur toute interface : c'est un critère d'acceptation, pas une option.
- Données : profil de besoins = besoins fonctionnels, jamais de pathologie. Aucune donnée personnelle réelle dans le code, les tests ou les fixtures.
- Secrets : jamais dans le dépôt (même privé).
- Contrat d'API : la source de vérité est `nautilus-contrat-api`. Ne jamais modifier un client généré à la main.

## Sessions Claude Code

- Au démarrage, le dernier résumé est injecté automatiquement (hook SessionStart). Commande `/reprise` pour reprendre proprement.
- En fin de session, ou quand l'utilisateur annonce une pause : `/cloture`.
- Protocole : `.claude/sessions/_PROTOCOLE.md`. Ce dossier est réservé à Claude Code ; ne pas le mentionner dans la documentation destinée aux humains.
