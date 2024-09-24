# install-b2-cli-action

[![test-action](https://github.com/sylwit/install-b2-cli-action/workflows/test-action/badge.svg)](https://github.com/sylwit/install-b2-cli-action/actions?query=workflow%3Atest-action)

Install and authorize Backblaze B2 CLI directly on a GitHub Actions Linux host.

After this action, every step is capable of running `b2` CLI.

You must set 2 environment variables (secrets) `B2_APPLICATION_KEY_ID` and `B2_APPLICATION_KEY` to authenticate your cli.

### Usage

Add the following step to a job in your workflow

```yaml
- id: install-b2-cli
  uses: andromidasj/install-b2-cli-action@v1.0.0
  with:
    version: v4.1.0     # default to latest
  env:
    B2_APPLICATION_KEY_ID: ${{ secrets.B2_APPLICATION_KEY_ID }}
    B2_APPLICATION_KEY: ${{ secrets.B2_APPLICATION_KEY }}
```

### Full example

```yaml
name: Update CORS
on:
  push:

jobs:
  sync:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2.4.0

      - uses: andromidasj/install-b2-cli-action@v1.0.0
        env:
          B2_APPLICATION_KEY_ID: ${{ secrets.B2_APPLICATION_KEY_ID }}
          B2_APPLICATION_KEY: ${{ secrets.B2_APPLICATION_KEY }}
      ...

      - name: Update CORS
        run: b2 bucket update --cors-rules "$(<./b2-cors.json)" myBucket allPrivate
```

## Authors

Created and maintained by [Sylvain Witmeyer](https://github.com/sylwit)
Forked and updated by [Josh Andromidas](https://github.com/andromidasj)

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/sylwit/install-b2-cli-action/blob/master/LICENSE) file for details
