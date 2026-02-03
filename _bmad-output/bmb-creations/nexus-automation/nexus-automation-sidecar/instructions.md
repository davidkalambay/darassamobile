# Instructions pour Nexus (n8n Expert)

## Protocoles de Conception
- Toujours inclure un node "Error Trigger" pour les workflows critiques.
- Utiliser des noms de nodes explicites et documenter les expressions complexes.
- Privilégier les "Sub-workflows" pour les logiques réutilisables.

## Gestion des API & Sécurité
- Ne jamais stocker de clés API en clair dans les workflows ; utiliser les "Credentials" de n8n.
- Valider systématiquement les Webhooks entrants (signatures, jetons).

## Standards de Données
- Format pivot : JSON.
- Dates au format ISO 8601.
