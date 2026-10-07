# Gitops demo

This repository demonstrates the benefits of GitOps in a DevOps context.

The demo triggers a Jenkins job whenever a Pull Request is authorized and merged into the main branch.

There is a small group belonging to the `asg-org` organization, having different roles, approvers, and developers.

When a developer submits a PR, another team member reviews it. After the pull request is approved and merged, a Jenkins SCM polling mechanism, which monitors the state of the pull request, detects the authorization and fires the  job.

The Jenkins job runs a `helloWorld.sh` bash script.


## Show case example


### Initial setup

Using another github account (`asgcloudops`) using git local settings in other directory.

1. Fork the GitHub repository.

2. Clone it locally.

```bash
git clone https://github.com/asgcloudops/gitops-demo.git
```

3. Set up the git local settings for the `asgcloudops` user.

```bash
git config --local user.name "Cloudops User"
git config --local user.email "antonio.salazar.cloudops@gmail.com" 
git config --local --list
```

4. Set up the `origin` and `upstream` reposigories

```bash
git remote -v
git remote add upstream https://github.com/ansalazadevops/gitops-demo.git
git remote -v
```

5. Login to GitHub as `asgcloudops` to ensure the pull and push operations are done properly.

```bash
gh auth login
```

> Choose whether to login by HTTPS or token


### Create a new Pull Request and Submit it

1. Create the new branch locally.

```bash
git checkout -b ${PR-BRANCH}
```

2. Edit the `scripts/helloWorld.sh` script by adding some lines. i.e. `echo "Greetings by Cloud Ops user from $(hostname -s)"`

3. Add and commit to the git tree.

```bash
git status
git add .
git commit -m "Adding a new line"
```

4. Push the PR to the origin repository.

```bash
git push origin ${PR-BRANCH}
```

5. Once the PR gets submitted, login to a different user from the `asg-org` group, then approve it and merge it.

6. Monitor the Jenkins job named helloWorld gets fired after a minute.

7. Close the PR.

```bash
git checkout main
git branch -D ${PR-BRANCH}
git push origin ${PR-BRANCH} --delete
```