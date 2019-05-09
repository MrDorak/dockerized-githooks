# dockerized-githooks

Some simple git hooks running in a dockerized environment

## Setup

Simply copy any git hook you want to use in a `hooks/` directory, configure the hook if needed.

Add the following script in your `package.json`
```json
  "scripts": {
    "hooks": "cp `ls ./hooks/* | grep -v conf.txt` .git/hooks/ && chmod -R 755 .git/hooks/"
  }
```
then run 
```
yarn hooks
```
or 
```
npm run hooks
```

## Hooks Summary

- `pre-commit` : copies `hooks/` directory to `.git/hooks/` if any change is detected and checks if there is any dependabot branch to 
prompt to run 'yarn upgrade --latest' before committing

- `commit-msg` : adds a [skip-ci] tag at the end of your commit if pushing on a feature branch

- `post-merge` : creates a `conf.txt` file containing the prefered webpack config for future runs (defaults to 'dev') and 
then copies `hooks/` directory to `.git/hooks/`, then runs 'yarn install' and then 'yarn run dev' (or 'yarn run watch' based on `conf.txt`) if any
 change is detected in the corresponding file or directory

- `post-checkout` : same as `post-merge` copies `hooks/` directory to `.git/hooks/`, runs 'yarn install' and runs 'yarn run dev' (or 'yarn 
run watch' based on `conf.txt`) if any change is detected in the corresponding file or directory
