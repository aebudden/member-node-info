This repository contains information about DataONE Member Nodes that can be used for presentations, web sites, and other fora where Member Nodes are being presented.

## Files and Folders

```
.
└── production          Content for the production environment
    └── graphics        Folder with Member Node icons / logos
        ├── originals   Original images
        └── web         Images to be used in Web interfaces
```

Image files are named with the node Id minues the "urn:node:" portion. So for 
example, the member node:

```
  urn:node:KNB
```

Has web image file named:

```
  production/graphics/web/KNB.png
```
which can be directly linked to from GitHub using the URL:

  https://raw.githubusercontent.com/DataONEorg/member-node-info/master/production/graphics/web/KNB.png


## Tools

A couple of handy tools for image introspection and manipulation:

* [exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)
* [Imagemagick convert](https://www.imagemagick.org/script/index.php)

To generate a list of images with dimensions:

```bash
for img in $(ls .); do SZ=$(exiftool -s -s -s -ImageSize ${img}); \
  printf "%15s %10s\n" ${img} ${SZ}; done
```

To create copies of images with dimensions of no smaller than 125 pixels wide by
40 pixels high while preserving preserving aspect ratio and saving as .png:

```bash
for img in $(ls originals/*.jpg); do echo ${img}; \
  convert ${img} -resize 125x40^ "web/$(basename ${img%.*}).png"; \
  done
```

## A Note on Image Sizes

Several of the original images that were being served up were rather large, even though they rendered with correct size and placement in the browser because the image size is specified in the containing HTML. This is very inefficient for larger images as each client must download a large image and downscale it for rendering. It is good practice to resize images appropriately before serving.

