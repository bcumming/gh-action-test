# gh-action-test

Key variables set inside the container running the action:
```bash
# the repository that is running the action (this repo)
GITHUB_REPOSITORY=bcumming/gh-action-test
# the commit/branch
GITHUB_REF=refs/heads/main
# SHA of the commit
GITHUB_SHA=c5d269fd1d240151d1c0b829939e54755937049c
```

The repository that contained the workflow that triggered the action is not available inside the container (i.e. it has not been cloned and mounted in side the container).

So we have to clone the repository?

```
echo '--- CLONE and CHECKOUT ${GITHUB_REPOSITORY}@${GITHUB_SHA} ---`
base_path=`pwd`/repo
git clone https://github.com/${GITHUB_REPOSITORY}.git repo --recursive
cd "${base_path}"
git fetch
git checkout ${GITHUB_SHA}
```
