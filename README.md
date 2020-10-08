# Tanzu Build Service Update Pipeline

The purpose of this pipeline is to install Tanzu Build Service updates when manually triggered.

## Maintainer

- Current mainainers are Chris Willis (mailto:chwillis@vmware.com) and Grig Gheorghiu (mailto:grig.gheorghiu@linquest.com)
- Originally forked from https://github.com/making/tbs-pipeline

## Set Variables
The following variables are required in credhub or `vars.yml`.`

| Keyword       | Explanation                                                                            |
|:--------------|:---------------------------------------------------------------------------------------|
| `harbor_hostname` | the Harbor instance TBS has been configured to use |
| `harbor_username` | a username that has access to the Harbor project TBS uses |
| `harbor_password` | password for `harbord_username` |
| `harbor_project` | the name of the Harbor project that TBS uses |
| `kubeconfig` | the full kubeconfig for a service account that has appropriate access to the cluster running TBS |
| `pivnet_api_token` | API token for a pivnet account that will be used to retrieve TBS updates |
| `pivnet_username` | username for a pivnet account that will be used to retrieve TBS updates |
| `pivnet_password` | password for a pivnet account that will be used to retrieve TBS updates |
| `ca_cert` | CA cert that Harbor uses |
| `git_url` | the git URL that TBS will use when pulling down source code to build container images |
| `aws_access_key_id` | the AWS access key ID for the account that will be used to copy TBS install artifacts to S3 storage |
| `aws_secret_access_key` | the AWS secret access key for the account that will be used to copy TBS install artifacts to S3 storage | |
aws_region: us-gov-west-1
s3_bucket: s31-tbs-install
s3_endpoint: https://s3.us-gov-west-1.amazonaws.com

## Getting Started
0. `fly -t dev login -c https://concourse.dev.km.spaceforce.mil`
0. Edit `vars.yml` and put in the appropriate values
0. `fly -t dev sp -p "Update TBS <ENV_NAME>" -c ./pipeline.yml -l ./vars.yml`
0. `fly -t dev up -p "Update TBS <ENV_NAME>"`
0. `fly -t dev tj -j "Update TBS <ENV_NAME>/kp-import"`

### Notes
* To delete a previous tanzu build service install run `kapp delete -a tanzu-build-service`
* Make sure to clean up `kp secret list` prior to running pipeline or the `kp create secret` steps may fail in the pipeline





# tbs-install-pipeline


### Notes
* To delete a previous tanzu build service install run `kapp delete -a tanzu-build-service`
* Make sure to clean up `kp secret list` prior to running pipeline or the `kp create secret` steps may fail in the pipeline