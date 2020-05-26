# OpenWrt json generator

These script generate JSON files for OpenWrt images and packages as a base for
further tools.  In the current setup a GitHub action reloads daily both packages
and image merging scripts and pushes the result to the [gh-pages
branch][gh-pages], so all files are available at
`https://aparcar.github.io/openwrt-json`. As GitHub does not automatically index
folders, all available files can be clicked [through via GitHub][gh-pages].

All JSON files are available as uncompressed JSON with a `.json` suffix or
Gzipped with `.json.gz` as suffix.

[gh-pages]: https://github.com/aparcar/openwrt-json/tree/gh-pages

## profiles.json

An overview of all available binary firmware images group by profiles. A
stripped example is available at `examples/profiles.json`.

The file is generated by merging the per `target/subtarget` generated JSON files
into a single file.

## manifest.json

The file exists per `target/subtarget` and gives details of all available
packages, taking into account the target specific packages and all activated
feeds. It basically converts `Packages.manifest` to JSON and changes the case to
lower. A stripped example is available at
`examples/ath79/generic/manifest.json`.

## index.json

The file exists per `target/subtarget` and gives an overview of all available
packages by name only as a list/array. This is usable to know what packages
exists without processing all the metadata of `manifest.json`. A stripped
example is available at `examples/ath79/generic/index.json`.

## Configuration

The configuration is done via `config.yml`, it is possible to set active targets
and feeds and also the upstream address to parse available packages and firmware
images.

## Running

Install the dependencies via `pip install -r requirements.txt` and run the
scripts:

```shell
python3 merge-packages.py
python3 merge-profiels.py
```