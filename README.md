# Art Engine 
Create generative art by using the canvas api and node js.

## Flow of the project
Create your different layers as folders in the 'layers' directory, and add all the layer assets in these directories. You can name the assets anything as long as it has a rarity weight attached in the file name like so: `example element#70.png`. You can optionally change the delimiter `#` to anything you would like to use in the variable `rarityDelimiter` in the `src/config.js` file.

Once you have all your layers, go into `src/config.js` and update the `layerConfigurations` objects `layersOrder` array to be your layer folders name in order of the back layer to the front layer.

The `name` of each layer object represents the name of the folder (in `/layers/`) that the images reside in.

Optionally you can now add multiple different `layerConfigurations` to your collection. Each configuration can be unique and have different layer orders, use the same layers or introduce new ones.

Update your `format` size, ie the outputted image size, and the `growEditionSizeTo` on each `layerConfigurations` object, which is the amount of variation outputted.

You can mix up the `layerConfigurations` order on how the images are saved by setting the variable `shuffleLayerConfigurations` in the `config.js` file to true. It is false by default and will save all images in numerical order.

If you want to have logs to debug and see what is happening when you generate images you can set the variable `debugLogs` in the `config.js` file to true. It is false by default, so you will only see general logs.

If you want to play around with different blending modes, you can add a `blend: MODE.colorBurn` field to the layersOrder `options` object.

If you need a layers to have a different opacity then you can add the `opacity: 0.7` field to the layersOrder `options` object as well.

If you want to have a layer _ignored_ in the DNA uniqueness check, you can set `bypassDNA: true` in the `options` object. This has the effect of making sure the rest of the traits are unique while not considering the `Background` Layers as traits, for example. The layers _are_ included in the final image.

To use a different metadata attribute name you can add the `displayName: "Awesome Eye Color"` to the `options` object. All options are optional and can be addes on the same layer if you want to.

## Working
When you are ready, run the following command and your outputted art will be in the `build/images` directory and the json in the `build/json` directory:
```sh
npm run build
```
or
```sh
node index.js
```

The program will output all the images in the `build/images` directory along with the metadata files in the `build/json` directory. Each collection will have a `_metadata.json` file that consists of all the metadata in the collection inside the `build/json` directory. The `build/json` folder also will contain all the single json files that represent each image file.

You can also add extra metadata to each metadata file by adding your extra items, (key: value) pairs to the `extraMetadata` object variable in the `config.js` file.

You might possibly want to update the baseUri and description after you have ran your collection. To update the baseUri and description simply run:
```sh
npm run update_info
```

To see the percentages of each attribute across your collection, run:
```sh
npm run rarity
```

Create a preview image collage of your collection, run:
```sh
npm run preview
```

In order to convert images into pixelated images you would need a list of images that you want to convert. So run the generator first.
Then simply run this command:
```sh
npm run pixelate
```
All your images will be outputted in the `/build/pixel_images` directory.
If you want to change the ratio of the pixelation then you can update the ratio property on the `pixelFormat` object in the `src/config.js` file. The lower the number on the left, the more pixelated the image will be.

### Generate GIF images from collection

In order to export gifs based on the layers created, you just need to set the export on the `gif` object in the `src/config.js` file to `true`. You can also play around with the `repeat`, `quality` and the `delay` of the exported gif.

Setting the `repeat: -1` will produce a one time render and `repeat: 0` will loop forever.

```js
const gif = {
  export: true,
  repeat: 0,
  quality: 100,
  delay: 500,
};
```