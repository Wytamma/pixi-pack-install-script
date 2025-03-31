# Pixi-pack install script 

This action will create a unix install script for pixi-pack environments created with the [pixi-pack action](https://github.com/marketplace/actions/pixi-pack-action).

# Example 

We have a repo https://github.com/Wytamma/pixi-python that contains a pixi environment with python and uses the pixi-pack action to create a packed versions of the environment. This action can be used to create a install script for the version of `python` from the packed environment. Here we use the `--name` option to rename python to `pixi-python` in the install script.

```yaml
```bash
curl -sSL https://github.com/Wytamma/pixi-python/releases/latest/download/install.sh | bash -s -- --name pixi-python
pixi-python -V
```

# Example workflow

```yaml
name: "Create install script for pixi-packed environments"
on:
  push:
    tags:
      - 'v*.*.*'

permissions:
  contents: write

jobs:
  create-install-script-and-release:
    runs-on: ubuntu-latest

    steps:
      - name: Create install script
        uses: wytamma/pixi-pack-install-script@v1
        with:
          entrypoint: "python"

      - name: Upload to Release
        uses: softprops/action-gh-release@v2
        with:
          files: "install.sh"
```
