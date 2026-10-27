# Dictionnaire de données : Credit Risk

Description des 14 colonnes du dataset `loan_data.csv` (LendingClub, 9578 clients), pour prédire le défaut de remboursement.

## La variable cible : `not.fully.paid`

C'est la colonne qu'on cherche à prédire. 

- **1** = le client n'a pas remboursé entièrement son crédit (défaut, « mauvais payeur »)
- **0** = le client a remboursé normalement (« bon payeur »)

Objectif du modèle : à partir des 13 autres colonnes, prédire si `not.fully.paid` vaudra 0 ou 1.

## Colonnes « profil du crédit »

| Colonne | Description | Rôle dans l'analyse du risque |
| --- | --- | --- |
| `credit.policy` | Le client respecte-t-il les critères d'octroi de LendingClub (1 = oui, 0 = non) | Premier filtre de l'entreprise |
| `purpose` | Raison du crédit, en texte : debt_consolidation (41%), credit_card, educational, major_purchase… | Seule colonne texte — à traiter au nettoyage |
| `int.rate` | Taux d'intérêt du crédit (0.1189 = 11,89%) | Taux élevé = client déjà jugé risqué par la banque |
| `installment` | Mensualité à payer (ex : 829/mois) | Plus la mensualité est lourde, plus la charge est forte |

## Colonnes « situation financière »

| Colonne | Description | Rôle dans l'analyse du risque |
| --- | --- | --- |
| `log.annual.inc` | Revenu annuel du client, en logarithme (ex : 11.35) | Plus le chiffre est grand, plus le revenu est élevé |
| `dti` | Ratio dettes/revenu (debt-to-income) | Indicateur clé : plus c'est haut, plus le client est déjà endetté (H4) |
| `revol.bal` | Solde restant dû sur le crédit renouvelable (carte) | Montant de dette en cours |
| `revol.util` | Taux d'utilisation du crédit renouvelable (ex : 52,1%) | Proche de 100% = client à la limite financièrement |

## Colonnes « historique de crédit »

| Colonne | Description | Rôle dans l'analyse du risque |
| --- | --- | --- |
| `fico` | Score de crédit FICO (environ 600 à 850) | Indicateur roi : plus il est haut, plus le client est fiable (H3) |
| `days.with.cr.line` | Ancienneté de l'historique de crédit, en jours (5639 ≈ 15 ans) | Plus c'est long, plus la banque a de recul — rassurant |
| `inq.last.6mths` | Nombre de demandes de crédit sur les 6 derniers mois | Beaucoup de demandes = signal d'alerte |
| `delinq.2yrs` | Nombre de retards de paiement sur les 2 dernières années | Le passé prédit le futur |
| `pub.rec` | Nombre d'incidents publics (faillites, etc.) | Signal négatif fort |

## Lien avec les hypothèses du cadrage

- **H2 (montant)** : `installment`, `revol.bal`
- **H3 (historique de crédit)** : `fico`, `days.with.cr.line`, `delinq.2yrs`, `pub.rec`
- **H4 (capacité de remboursement)** : `dti`, `log.annual.inc`, `revol.util`
- **Signal « déjà jugé risqué »** : `int.rate`