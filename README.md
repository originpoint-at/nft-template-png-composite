# PNG Composite template for CandyMint

[CandyMint][1] is a platform for creating and minting NFTs. This repository contains the png-composite template that generate the final NFT images by compositing layers.

## Usage

1. Click `Use this template` to create your own repository
1. Put images in the `image` directory
1. Update the `layouts.yaml` file
1. Connect your repository with your collection created in the CandyMint platform

## Template Structure

```text
image
├── crocodiale                # suite
│   ├── 01_desktop            # layer, should be sequential
│   │   ├── desktop_01.png    # item, should be sequential
│   │   ├── desktop_02.png
│   ├── other layers...
├── other suites...
README.md
layouts.yaml
```

- `image/<suite>/<layer>/<item>.png` is the core structure of the PNG Composite template:
- `README.md` is the README file of the repository.
- `layouts.yaml` is the configuration file of the NFT items, see [Anatomy](#anatomy) for more details.

## Anatomy

```yaml
template: png_composite       # template name, DO NOT change
engine: 0.1.0                 # engine version, DO NOT change
config:
  mime: image/png             # image mime type
  size:
    width: 64                 # image width
    height: 64                # image height
    # ...                     # other properties used internally, DO NOT change
suites:
  - name: crocodile           # suite name, should be unique and same as the directory name
    backgrounds:              # background options of the suite, order is important
      - color: "#D7F8FF"
      - color: "#AE9B81"
      # other backgrounds...
    layers:
      - name: 01_desktop       # layer name, should be unique and same as the directory name
        items:
          - image: desktop_01.png   # file name of the item
            x: 0
            y: 51
            width: 64
            height: 13
            trait_type: desktop     # trait type, can be arbitrary string, will include in the NFT metadata
            value: desktop_01       # trait value of the item, will include in the NFT metadata
            display_type: string    # display type of the trait, can be string or number, etc.
          - image: desktop_02.png
            x: 0
            y: 51
            width: 64
            height: 13
            trait_type: desktop
            value: desktop_02
            display_type: string
          # other items...
      # other layers...
  # other suites...
```

**Caveats:**

- The `image` directory **MUST** contain only images.
- The `layouts.yaml` file **MUST** be valid YAML.
- **Image Size**: This template is designed for on-chain storage by default, taking into account Gas fees, currently, it supports image sizes up to **50KB**.
- **Backgrounds**: If the final NFT image does not require a background color, or if there is a dedicated background layer, please leave the backgrounds field blank, like `backgrounds: []`.
- **Layer Composite**: This template generates the final NFT image by merging layers. In the layouts file, the first layer in the suite is at the bottom, and the last layer is at the top. Please organize the layers appropriately.
- In order to build a solid collection, the layers and their items **MUST** be sequential.
- **Preserving order in `layouts.yaml`**: CandyMint allows managing multiple collection versions. When adding new images and updating the `layouts.yaml`, it's crucial to append new elements at the end. **DO NOT** rearrange the existing order of backgrounds, layers, or items. This ensure all versions function correctly.
- Manually measuring rectangles in PNG images can strain your hands and eyes, so we've created the [PNG Measure][5] to make this task easier.

## TODO

- [ ] Add a license

## Other Templates

- [Default Template](https://github.com/originpoint-at/nft-template-default)
- [SVG Composite Template](https://github.com/originpoint-at/nft-template-svg-composite)
- [PNG Composite Template](https://github.com/originpoint-at/nft-template-png-composite)

## Relative Links

- [CandyMint][1]
- [CandyMint Testnet][2]
- [CandyMint Docs][3]
- [PNG Composite Tool][5]
- [Discord][4]
- Twitter
- Telegram

[1]: https://candymint.io
[2]: https://testnet.candymint.io
[3]: https://docs.candymint.io
[4]: https://discord.gg/DyP5Vxw5VB
[5]: https://candymint.io/tools/png-measure
