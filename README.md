# "Build AWS Lambda Extension" GitHub Action

This GitHub action will create a ZIP file containing:

- the AWS Lambda layer (that needs to be preperaded in advance. see [Prerequesites](#prerequesites))
- the latest version of the [Sentry Lambda Extension](https://github.com/getsentry/sentry-lambda-extension).

## Prerequesites

Befor you can use this action to bundle Lambda Layer and the Sentry Lambda extension together
you need to prepare your Lambda Layer in a directory called `/dist-serverless`:

A very basic example would be:

```yaml
steps:
  - run: |
      echo "Create the Lambda in the dist-serverless directory"
      mkdir dist-serverless
      cp -r stuff/* dist-serverless/
```

You also have to make sure to include this directory in the build cache you need to set up
using the [actions/cache@v3](https://github.com/actions/cache) Github action.

How this is done you can learn in the build workflow of the Javascript SDK:

https://github.com/getsentry/sentry-javascript/blob/master/.github/workflows/build.yml

## Usage

To bundle the above prepared Lambda layer with the latest Sentry Lambda Extension and save it in a file called `sentry-python-serverless.zip` you can the following to your GitHub workflow:

(The .zip file will be uploaded in the GitHub action so it can be used by other actions or steps in your workflow.)

```yaml
steps:
    - uses: getsentry/action-build-aws-lambda-extension@v1
    with:
        artifact_name: ${{ github.sha }}
        zip_file_name: sentry-python-serverless.zip
```

This test script illustrates the usage of the action:

[.github/workflows/test_production.yml](.github/workflows/test_production.yml)

For an full example usage see the Sentry Python SDK:

https://github.com/getsentry/sentry-python/blob/master/.github/workflows/ci.yml

### Inputs

The following are all _required_.

| name                | description                                                                                                                                      |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `artifact_name`     | Name of the prepared articact the Lambda Layer zip file should be uploaded to                                                                    |
| `zip_file_name`     | Name of the zip file that will be created                                                                                                        |
| `build_cache_key`   | Build cache key                                                                                                                                  |
| `build_cache_paths` | Paths of the build cache                                                                                                                         |
| `debug_enabled`     | If set to "true" debugging is enabled and you can log into the running action. (See https://github.com/marketplace/actions/debugging-with-tmate) |

## Testing

If you want to see what an example of a zip file created by this action looks like you can manually run the GitHub action "Test Production". This will create a dummy lambda layer (just containing one placeholder file) and the latest [relay](https://github.com/getsentry/relay) based Sentry Lambda Extension. After the GitHub action has run, you can download the generated artifact at the bottom of the summary page of the GitHub action result.

## Contributing

See the [Contributing Guide](CONTRIBUTING.md).

## License

See the [License File](LICENSE).
