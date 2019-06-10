
## List down current services/versions
gcloud app services list
gcloud app versions list

## Set traffic for each version
gcloud app services set-traffic default --splits 20190508t125131=1.00(0.5)
gcloud app services set-traffic default --splits v2=1 --migrate