# dockerized-githooks

Some simple git hooks running in a dockerized environment

## Setup

Simply copy any git hook you want to use in a `hooks/` directory, change the hook as you need.

Add the following in your `package.json`
```json
  "scripts": {
    "hooks": "chmod -R 755 hooks/ && git config core.hookspath hooks"
  }
```
This makes the whole `hooks` directory executable and changes the default git hooks directory to `hooks` instead of `.git/hooks`. After that run 
```
yarn hooks
```

## Hooks Summary

- `pre-commit` : checks if there is any dependabot branch to prompt to run 'yarn upgrade --latest' before committing

- `commit-msg` : adds a [skip-ci] tag at the end of your commit if pushing on a feature branch

- `post-merge` : creates a `conf.txt` file containing the prefered webpack config for future runs (defaults to 'dev') 
then runs 'yarn install' and then 'yarn dev' (or 'yarn watch' based on `conf.txt`) if any change is detected in the 
corresponding file or directory

- `post-checkout` : same as `post-merge`, runs 'yarn install' and then runs 'yarn dev' (or 'yarn watch' based on 
`conf.txt`) if any change is detected in the corresponding file or directory
