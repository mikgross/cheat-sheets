## Migration of project between environments

This step by step cheat sheet defines the process to follow in order to migrate an existing dev, stage, prod project to another environment. This is my approach and might not work for other potential readers.

### a) For Firestore:
1) gcloud config set project [project_name]
2) gcloud beta firestore export gs://[project_name].appspot.com --collection-ids=[coll1],[coll2]
  if error: ERROR: (gcloud.beta.firestore.export) NOT_FOUND: Google Cloud Storage file does not exist, go on google cloud console and initialize firestore
3) gcloud config set project [project_name2]
4) Give access to service account of [porject_name2] to [project_name] on gcloud platform
5) Initialize firestore storage in gcloud platform
6) gcloud beta firestore import gs://[project_name].appspot.com/[save_name]/

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
    Typical config might include the following (not complete pleas think!):
    a) `environment.ts` and `environment.prod.ts` files
  3) sudo ng build --prod
  4) cd dist
  5) copy app.yaml file from one of the sosympl projects (try to select the last one used)
  6) gcloud config set project [project_name2]
  7) gcloud app deploy --no-promote (for testing) --promote (for deployment)

### d) Functions:
  1) firebase use [project_id]
  2) change all configs to related environment in [env2]/[app_name], change services dependng on app name such as fire-extensions
    
      Typical config might include the following (not complete pleas think!):
      a) `environment.ts` and `environment.prod.ts` files
  3) Pass environment variables from [project1] to [project2]
  3) change CORS policies in functions if applicable
  4) firebase deploy

### e) FireAuth
  1) Update authorized URLs in settings to the one of your app
