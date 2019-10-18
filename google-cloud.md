## Migration of project between environments
This step by step cheat sheet defines the process to follow in order to migrate an existing dev, stage, prod project to another environment. This is my approach and might not work for other potential readers.
----
### a) For Firestore:
1) gcloud config set project [project_name]
2) gcloud beta firestore export gs://[project_name] --collection-ids=[coll1],[coll2]
3) gcloud config set project [project_name2]
4) Give access to service account of [porject_name2] to [project_name] on gcloud platform
5) Initialize firestore storage in gcloud platform
6) gcloud beta firestore import gs://[project_name]/[save_name]/

### b) Google Cloud Storage:
1) gcloud config set project [project_name]
2) gsutil cp -r gs://[bucket_name]/[folder] ./[local_dir]
Repeat step 1 for all storage folder needed
3) gcloud config set project [project_name2]
4) gsutil cp -r [local_dir]/[folder] gs://[bucket_name2]
Repeat step 2 for all stroage folder needed

### c) App:
  1) sudo cp --verbose -r [env1]/[app_name] [env2]/[app_name]
  2) change all configs to related environment in [env2]/[app_name], change services dependng on app name such as fire-extensions
  3) sudo ng build --prod
  4) cd dist
  5) gcloud config set project [project_name2]
  6) gcloud app deploy --no-promote (for testing) --promote (for deployment)

### d) Functions:
  1) firebase use [project_id]
  2) change CORS policies in functions if applicable
  2) firebase deploy

### e) FireAuth
  1) Update authorized URLs in settings to the one of your app
