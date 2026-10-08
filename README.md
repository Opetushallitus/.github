# .github
Kehittäjiä helpottavia actions-pohjia

| Tiedosto      | Käyttötarkoitus |
| ----------- | ----------- |
| build-java-package.yml      | Rakenna javakirjasto ja lataa se github packagesiin |
| push-scan-java-ecr.yml   | Rakenna javaimage ja lataa se AWS ECR:ään |
| deploy-from-ecr-to-ecs.yml   | Ota image ECR:stä ja aseta se ajoon haluamaasi ympäristöön |
| update-deployment-metadata.yml   | Kirjaa deployment keskitettyyn dashboardiin (DynamoDB `deployments` ja `services`) |
| update-build-metadata.yml   | Kirjaa buildin keskitettyyn dashboardiin (DynamoDB `builds`) |

## Build java package

## Push scan java ecr

## Deploy from ecr to ecs

## Update deployment metadata

Kutsutaan onnistuneen deploymentin jälkeen. Kirjoittaa samat kentät kuin `cloud-base`-repon `deploy.py` (`save_deployment_metadata`): `deployments` (EnvService, Build, User, Time) ja `services` (EnvService, LatestDeployedBuild).

OIDC-roolin ARN luetaan ympäristömuuttujasta `AWS_OPINTOPOLKU_OPS_DASHBOARD_UPDATER_ROLE_ARN`. Arvo tulee GitHub-organisaation secretistä samalla nimellä (rooli `github-actions-ops-dashboard-updater-role`). Kutsuva workflow välittää secretin `secrets: inherit` -asetuksella.

## Update build metadata

Kutsutaan onnistuneen buildin jälkeen. Kirjoittaa samat kentät kuin `ci-tools`-repon `github-build/upload-image.sh`: DynamoDB-taulu `builds` (`Service`, `Build`, `Branch`, `Commit`, `Time`). Haara on kutsuvan workflown ref; pull requestissa `head>base`.

Käyttää samaa OIDC-roolia kuin deployment-metadatan kirjaus (`AWS_OPINTOPOLKU_OPS_DASHBOARD_UPDATER_ROLE_ARN`, rooli `github-actions-ops-dashboard-updater-role`). Kutsuva workflow välittää secretin `secrets: inherit` -asetuksella.