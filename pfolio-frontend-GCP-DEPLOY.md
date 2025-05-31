

#########
# INSTALL
#
```
git clone git@github.com:heidless-stillwater/pfolio-frontend-0.git

mv pfolio-frontend-0 pfolio-frontend-deploy-test-0

pfolio-frontend-deploy-test-0

```
  
#######################
# GCLOUD Deploy - React
#######################

# gCloud DEPLOY
```
## project
source .env-vars

#################
## storage bucket
#
source .env-vars
echo ' '
echo GCP_BUCKET: ${GCP_BUCKET}
echo GCP_REGION: ${GCP_REGION}

export bucket_path='gs://'${GCP_BUCKET}
echo bucket_path: ${bucket_path}

gsutil mb -l ${GCP_REGION} ${bucket_path}

## [bucket permissions]()
gsutil iam ch allUsers:objectViewer $bucket_path

```

# Cloud Run - SUBMIT
```
## push to repository

source .env-vars

echo gcloud builds submit --tag gcr.io/${GCP_PROJECT}/${GCP_SERVICE_NAME} .

gcloud builds submit --tag gcr.io/${GCP_PROJECT}/${GCP_SERVICE_NAME} .

```

## build service - DEPLOY
```
source .env-vars
gcloud run deploy ${GCP_SERVICE_NAME} \
     --platform managed \
     --region ${GCP_REGION} \
     --image gcr.io/${GCP_PROJECT}/${GCP_SERVICE_NAME} \
     --add-cloudsql-instances ${GCP_PROJECT}:${GCP_REGION}:${GCP_INSTANCE} \
     --allow-unauthenticated

# URL
https://pfolio-frontend-svc-1089619978780.europe-west2.run.app

```




















# UTILS
## gCloud upload images
```
# local
IMAGES_DIR=./public/images
LOGO_DIR=./public/logo

# gsCloud
GCP_BUCKET=heidless-frontend-bucket-4
GCP_IMAGES_DIR=gs://${GCP_BUCKET}
GCP_LOGO_DIR=gs://${GCP_BUCKET}

echo ICONS_DIR: ${LOGO_DIR}
echo IMAGES_DIR: ${IMAGES_DIR}
echo BUCKET: ${GCP_BUCKET}
echo GCP_IMAGES_DIR: ${GCP_IMAGES_DIR}
echo GCP_LOGO_DIR: ${GCP_LOGO_DIR}

# upload
gsutil cp -r ${IMAGES_DIR} ${GCP_IMAGES_DIR}
gsutil cp -r ${LOGO_DIR} ${GCP_LOGO_DIR}

```

## create Serice
```
-> deploy uploaded Container Registry
-> i.e  NOT continuous deployment

CLOUD RUN->DeployContainer->Service->'Select'
--
IMAGE:
gcr.io/heidless-portfolio-0
- heidless-pfolio-frontend-0
	- 'latest'
--

REGION:
--
europe-west2
--

AUTHENTICATION:
--
Allow unauthenticated invocations
--

CREATE

```




#######################
# GCLOUD Deploy - React
#######################
```
# install '.env-vars' exemplar
SRC=


```

Step 1: Set Up a Project in Google Cloud
1. Go to the Google Cloud Console (https://console.cloud.google.com/) and create a new project.
2. Choose a unique project name, and select the desired organization if applicable.
3. Once the project is created, note down the Project ID, as you'll need it later.

Step 2: Enable the necessary APIs
1. In the Google Cloud Console, navigate to the "APIs & Services" section.
2. Click on "Library" in the left sidebar.

#######################
# APIs
#
```
enable 'Cloud Storage'
enable 'App Engine Admin API'
```

#################
# STORAGE
#
```
create Bucket


```

##################
# DEPLOY
#
```
gcloud auth login

gcloud config set project PROJECT_ID

gcloud app deploy

```

#####################
# VERIFY
#
```

Step 5: Verify the Deployment
1. Visit the URL provided in the deployment output or go to the "App Engine" section in the Google Cloud Console.
2. You should see your React app running live on the provided URL.


########################################
########################################





