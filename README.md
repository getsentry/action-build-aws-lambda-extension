# "Build AWS Lambda Extension" GitHub Action

This GitHub action will create a ZIP file containing:

- the AWS Lambda layer (that needs to be preperaded in advance. see [Prerequesites](#prerequesites))
- the latest version of the [Sentry Lambda Extension](https://github.com/getsentry/sentry-lambda-extension).

## Prerequesites

Befor you can use this action to bundle Lambda Layer and the Sentry Lambda extension together you need to prepare your Lambda Layer in a directory called `/dist-serverless` and upload with [actions/upload-artifact@v3](https://github.com/actions/upload-artifact)

Example how to do this:

```yaml
steps:
    - run: |
        echo "Create the Lambda in the dist-serverless directory"
        mkdir dist-serverless
        cp -r stuff/* dist-serverless/

    - uses: actions/upload-artifact@v3
    with:
        name: ${{ github.sha }}
        path: |
        dist-serverless/*
```

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

For an full example usage see the Sentry Python SDK:

https://github.com/getsentry/sentry-python/blob/master/.github/workflows/ci.yml

### Inputs

The following are all _required_.

| name            | description                                                 |
| --------------- | ----------------------------------------------------------- |
| `artifact_name` | Name of the artifact containing the Lambda layer directory. |
| `zip_file_name` | The name the generated .zip file should have.               |

## Contributing

See the [Contributing Guide](CONTRIBUTING.md).

## License

See the [License File](LICENSE).
