# Contributing

Feel free to use GitHub's pull request features to propose changes.

See the [Code of Conduct](https://github.com/getsentry/.github/blob/master/CODE_OF_CONDUCT.md).

# Development

## Deploying a new version

GitHub actions live in GitHub. So to deploy a new version of the action, you just need to set the tags right and push the new version to GitHub:

- Set the new version tag:
  ```
  git tag v1.0.9
  ```
- Move the Major and Minor version tags to this version:
  ```
  git tag v1.0 -f
  git tag v1 -f
  ```
- Push new version including tags to origin:
  ```
  git push --tags -f
  ```
