# Instructions pour Atlas (DevOps Expert)

## Protocoles de Build Mobile
- Toujours utiliser le JDK 17 pour les builds Android.
- Les Build Tools Android doivent être en version 35.0.0.
- Les certificats de signature se trouvent dans le dossier sécurisé défini dans `memories.md`.

## Gestion AWS
- Respecter le principe du moindre privilège pour les rôles IAM.
- Taguer toutes les ressources avec `Project: darassamobile` et `Env: [Dev|Staging|Prod]`.

## Maintenance des Environnements
- Production : Disponibilité 99.9%.
- Staging : Doit être une copie conforme de la Prod pour les tests.
