# Sketch Generator v0.1-not-yet-ready-for-production-use

This command is a recreation for Sketch of the Photoshop Generator functionality introduced by Adobe on Photoshop CC (see [this blog post on Adobe](http://blogs.adobe.com/photoshopdotcom/2013/09/introducing-adobe-generator-for-photoshop-cc.html) for more information).

It is a work in progress: most features in Photoshop Generator are implemented, but some are not there yet due to either lack of time or current technical limitations in Sketch (see the **Pending Features** section below).


## What is this?

If you've ever had to prepare a screen design for production use, you know how painful and time consuming it is: creating slices, naming them, making sure they're properly aligned, painstakingly exporting assets...

Well, it's 2013, and slicing images is *so* last century. Computers were invented to let us work less and spend more time watching kitten videos, so get ready to reclaim some of your precious time back.

Sketch Generator will let you export *all* your assets, no matter how complex your design, with a single keystroke. Forget about slicing, exporting, or moving files manually: welcome to the future, where everything that can be made automatically *is made automatically* :)

## Installation

- Just download this project, and move **Generate Assets.sketchplugin** to Sketch's plugins folder (to find it, open Sketch, select 'Custom Script...' from the 'Plugins' menu, click the gear icon and choose 'Open Plugins Folder')

## Usage

- Open your Sketch document
- Find an element you want to export as an asset (say, a button)
- Name the layer or layer group using the rules in the **Rules** section (i.e: 'button.png, button@2x.png 200%')
- Run Generator by either choosing it from the Plugins menu, or pressing the keyboard shortcut (Ctrl + Alt + Command + G)
- A new folder named "your-document-name-assets", containing all your assets grouped by Page and Artboard will be created in your document's current location.

## Features & limitations

So far, it supports the following features:

- Multiple assets per layer / layer group
- Export assets in PNG, GIF, PDF, SVG, EPS & TIFF format
- Arbitrary & unlimited asset scaling in output (extreme example: I've used a 10000% scale to export a 31800 × 9800 pixels JPG. Takes some time, but it works :)

## Rules

Here are some examples of supported tags (beware: not all are supported, see **Pending Features** section):

- .png (Default value: png32 with semi-transparent alpha), .png8, .png24, .png32
- .jpg (Default value: 9), .jpg(1-10), .jpg(1-100%)
- .gif
- 1-n%, (Number) px x (Number) px for scaling
- can also so '200x? logo.jpg', apparently

Here are some examples of how tags can be used:

- “200% logo-retina.png, logo.png” produces both a 2x and a 1x asset
- “heroImage.jpg10” produces a 1x asset with max quality
- “400% tuningfork.png, 250×250 tuningfork.jpg40%” produces a 4x PNG asset and a custom-scaled JPEG asset

For a more complete list of layer names this should support, check the tests in <https://github.com/adobe-photoshop/generator-assets/blob/master/test/test-parse-layer-name.js>


## Pending Features

### Not yet implemented, but feasible

- Set asset size in pixels (using XXX px x YYY px or the shorthand XXXx? to scale proportionally)
- Clean assets before exporting
- Export on save (this can be faked via a keyboard shortcut trick)

### Not implemented due to lack of technical support in Sketch

- Set JPG export quality. Reason: there’s no API in Sketch yet.
- Set PNG export format (PNG8, PNG24, PNG32). Reason: there’s no API in Sketch yet.
- Realtime export on layer modification. Reason: Sketch lacks a realtime backend (Photoshop is using a node.js backend for Generator)

### Upcoming features not included in Photoshop Generator

- Export for all Android pixel densities
- Add support for '@2x' and 'HDPI' style scales
- Export only layer groups, in PNG format, without requiring layer renames (this is how Sketch Framer works currently, and I think it makes more sense than Adobe's choice)
- Export selection only (for quick exports in complex documents)
