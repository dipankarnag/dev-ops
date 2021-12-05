Gitlab_Runners are the workers installed in a Host [VM/Pod/Container] that runs gitlab CI jobs


Install Gitlab Runner in a Host

While registering there are basically two type of these runners

1. Shell : These runner will execute jobs inside the Host only
2. Docker: These runner will execute jobs inside a docker container. Default Image is Ruby if unspecifed in .gitlab-ci.yml. N.B.: Docker must be installed in the Host

List all the runners in a Host:

sudo gitlab-runner list


Verifiy status of runners:
sudo gitlab-runner verify

Stop runner:
sudo gitlab-runner stop

If it fails, then make sure the runner is stopped from repo in gitlab UI. [settings > CI CD > Runner] and runner can be remeved from there as well

Delete removed runners:
sudo gitlab-runner verify --delete