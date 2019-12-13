### Overview
Track changes in GCP predefined IAM roles.
Inspired by https://github.com/SummitRoute/aws_managed_policies


### Updating
```
# collect list of gcp roles
gcloud iam roles list --format json > gcp-roles.json
# remove old roles
rm -rf roles && mkdir roles
# synchronize roles
cat gcp-roles.json | jq -r '.[].name' | xargs -n3 -I{} sh -c 'gcloud iam roles describe --format json {} > {}.json 2>&1'
# git commit update
git add . && git commit -m "Update $(date '+%F %T %Z')"
```
