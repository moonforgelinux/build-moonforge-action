# build-moonforge-action

This GitHub action can build [Moonforge](https://github.com/moonforgelinux/meta-moonforge) images using [kas](https://kas.readthedocs.io/en/latest/).

## Usage

See the following example:

```yml
jobs:
  build:
    runs-on: self-hosted
    steps:
      - uses: moonforgelinux/build-moonforge-action@main
        with:
          kas_file: kas/image.yml
          dl_dir: /path/to/cached/downloads
          sstate_dir: /path/to/cached/sstate-cache
          image_id: ${{ github.ref_name }}
          image_version: ${{ github.run_id }}
```

## Inputs

| Input         | Description                                    | Mandatory | Default | Reference
| ------------- | ---------------------------------------------- | --------- | ------- | ---------
| kas_file      | Path to the image kas file                     | Yes       |         |
| dl_dir        | Path to the Yocto downloads directory          | Yes       |         | See [Yocto documentation](https://docs.yoctoproject.org/5.0.15/ref-manual/variables.html#term-DL_DIR)
| sstate_dir    | Path to the Yocto shared-state cache directory | Yes       |         | See [Yocto documentation](https://docs.yoctoproject.org/5.0.15/overview-manual/concepts.html#shared-state-cache)
| image_id      | Image ID to be used in os-release              | Yes       |         | See [Freedesktop documentation](https://www.freedesktop.org/software/systemd/man/latest/os-release.html#IMAGE_ID=)
| image_version | Image version to be used in os-release         | Yes       |         | See [Fredesktop documentation](https://www.freedesktop.org/software/systemd/man/latest/os-release.html#IMAGE_VERSION=)

> [!IMPORTANT]
> This action assumes that the *dl_dir* and *sstate_dir* directories are properly set up. Running this action on runners with no cached directories can result in unnecessary long and credit-consuming workflows.

> [!NOTE]
> This action can be used together with other GitHub actions to store artifacts in remote locations (e.g., Amazon S3). The resulting artifacts can be accessed in subsequent steps, under *./build/tmp/deploy/images/*.

## Legal

MIT License

Copyright (c) 2026 Igalia, S.L.
