gcloud iam service-accounts create travis-ci --display-name "Travis CI" --project "docker-181710"
gcloud iam service-accounts keys create credentials.json --iam-account "travis-ci@docker-181710.iam.gserviceaccount.com"  --project "docker-181710"
gcloud projects add-iam-policy-binding docker-181710 --member "serviceAccount:travis-ci@docker-181710.iam.gserviceaccount.com" --role "roles/editor"

ssh-keygen -t rsa -f google_compute -C appuser
chmod 400 google_compute
https://console.cloud.google.com/compute/metadata/sshKeys?project=docker-181710

zip secrets.zip credentials.json google_compute
travis encrypt-file secrets.zip  --add