# OpenLayers LayerSwitcher

Grouped layer list control for an OpenLayer map.

To be shown in the layer switcher layers should have a `title` property; base
layers should have a `type` property set to `base`. Group layers
(`ol.layer.Group`) can be used to visually group layers together; a group with
a `fold` property set to either `open` or `close` will be displayed with a
toggle. See [Examples](#examples) for usage.

Compatible with OpenLayers version 3, 4, 5 and 6 (see note in [Install - Parcel,
Webpack etc.](#parcel-webpack-etc) regarding installing the appropriate version
of `ol-layerswitcher` for OpenLayers).

## Examples

The examples demonstrate usage and can be viewed online thanks to [raw.githack.com](http://raw.githack.com/):

- [Basic usage](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/layerswitcher.html)
  - Create a layer switcher control. Each layer to be displayed in the layer switcher has a `title` property as does each Group; each base map layer has a `type: 'base'` property. See the comments in [examples/layerswitcher.js](./examples/layerswitcher.js) for other layer/ group options including `combine` and `fold`.
- [Add layer](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/addlayer.html)
  - Add a layer to an existing layer group after the layer switcher has been added to the map.
- [Scrolling](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/scroll.html)
  - Makes the panel scroll vertically, the height of the layer switcher is controlled by setting the `max-height` style (see [examples/scroll.css](examples/scroll.css)) and it's position relative to the bottom of the map (see the `.layer-switcher.shown` selector in [src/ol-layerswitcher.css](src/ol-layerswitcher.css)).
- [Side bar](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/sidebar.html)
  - Demonstrates rendering the layer tree into a [Turbo87/sidebar-v2](https://github.com/Turbo87/sidebar-v2) pane. This uses the static method [`LayerSwitcher.renderPanel`](#renderpanel) which can be used to render the layer tree to any arbitrary HTML element.
- [Collapse groups](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/collapse-groups.html)
  - Shows the effect of setting the `fold` property of a Group to allow the group to be collapsed.
- [Selectable Groups](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/select-groups.html)
  - Demonstrates setting the [`groupSelectStyle`](#layerswitcher) option which determines if groups have a checkbox and how toggling a groups visibility affects it's children. The demo includes the ability to change the `groupSelectStyle` to easily see the effect of the different values.
- [Bundling with `ol` package (Browserify, Parcel, Webpack...)](https://github.com/walkermatt/ol-layerswitcher-examples)
  - To use the layer switcher with the [`ol` package](https://www.npmjs.com/package/ol) and a module bundler such as Browserify, Parcel, Webpack etc. see [ol-layerswitcher-examples](https://github.com/walkermatt/ol-layerswitcher-examples).
- [Activate panel with click](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/activation-mode-click.html)
  - Shows setting `activationMode: 'click'` (default is `'mouseover'`). When using this mode the control's button persists in the panel - use `collapseLabel` to set its text (default is `collapseLabel: '»'`, see the comments in [examples/layerswitcher.js](./examples/layerswitcher.js) for other examples). The close button is positioned to the left of the panel, to move it to the right add the following to your CSS:

```CSS
.layer-switcher.shown.layer-switcher-activation-mode-click {
padding-right: 34px;
}
.layer-switcher.shown.layer-switcher-activation-mode-click > button {
right: 0;
border-left: 0;
}
```

- [Start with panel active](http://raw.githack.com/walkermatt/ol-layerswitcher/master/examples/startactive-click.html)
  - Example with the layer switcher starting open using `startActive: true`. Here shown in combination with \`activationMode: 'click' which, while not required, is probably the most common scenario.

The source for all examples can be found in [examples](examples).

## Changelog

See [CHANGELOG](./CHANGELOG.md) for details of changes in each release.

## Install

### Browser

#### JS

Load `ol-layerswitcher.js` after OpenLayers. The layerswitcher control is available as `LayerSwitcher` or `ol.control.LayerSwitcher`.

```HTML
<script src="https://unpkg.com/ol-layerswitcher@3.7.0"></script>
```

#### CSS

```HTML
<link rel="stylesheet" href="https://unpkg.com/ol-layerswitcher@3.7.0/src/ol-layerswitcher.css" />
```

### Parcel, Webpack etc.

NPM package: [ol-layerswitcher](https://www.npmjs.com/package/ol-layerswitcher).

#### JS

Install the package via `npm`

    npm install ol-layerswitcher --save

:warning: If you're using the [`ol` package](https://www.npmjs.com/package/ol) prior to v5 you'll need to install `ol-layerswitcher@v2.0.0`.

#### CSS

The CSS file `ol-layerswitcher.css` can be found in `./node_modules/ol-layerswitcher/src`

To use the layerswitcher with the [`ol` package](https://www.npmjs.com/package/ol) and a module bundler such as Parcel, Webpack etc. see [ol-layerswitcher-examples](https://github.com/walkermatt/ol-layerswitcher-examples).

## Tests

To run the tests you'll need to install the dependencies via `npm`. In the root of the repository run:

    npm install

Then run the tests by opening [test/index.html](test/index.html) in a browser.

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

- [LayerSwitcher](#layerswitcher)
  - [setMap](#setmap)
  - [showPanel](#showpanel)
  - [hidePanel](#hidepanel)
  - [renderPanel](#renderpanel)
  - [renderPanel](#renderpanel-1)
  - [isBaseGroup](#isbasegroup)
  - [getGroupsAndLayers](#getgroupsandlayers)
  - [forEachRecursive](#foreachrecursive)
  - [uuid](#uuid)

### LayerSwitcher

**Extends ol/control/Control~Control**

OpenLayers Layer Switcher Control.
See [the examples](./examples) for usage.

**Parameters**

- `opt_options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Control options, extends ol/control/Control~Control#options adding:
  - `opt_options.startActive` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Whether panel is open when created. Defaults to false.
  - `opt_options.activationMode` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Event to use on the button to collapse or expand the panel.
    `'mouseover'` (default) the layerswitcher panel stays expanded while button or panel are hovered.
    `'click'` a click on the button toggles the layerswitcher visibility.
  - `opt_options.collapseLabel` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Text label to use for the expanded layerswitcher button. E.g.:
    `'»'` (default) or `'\u00BB'`, `'-'` or `'\u2212'`. Not visible if activation mode is `'mouseover'`
  - `opt_options.label` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Text label to use for the collapsed layerswitcher button. E.g.:
    `''` (default), `'«'` or `'\u00AB'`, `'+'`.
  - `opt_options.tipLabel` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** the button tooltip.
  - `opt_options.collapseTipLabel` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** the button tooltip when the panel is open.
  - `opt_options.groupSelectStyle` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** either `'none'` - groups don't get a checkbox,
    `'children'` (default) groups have a checkbox and affect child visibility or
    `'group'` groups have a checkbox but do not alter child visibility (like QGIS).
  - `opt_options.reverse` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Reverse the layer order. Defaults to true.

#### setMap

Set the map instance the control is associated with.

**Parameters**

- `map` **ol/Map~Map** The map instance.

#### showPanel

Show the layer panel.

#### hidePanel

Hide the layer panel.

#### renderPanel

Re-draw the layer panel to represent the current state of the layers.

#### renderPanel

**Static** Re-draw the layer panel to represent the current state of the layers.

**Parameters**

- `map` **ol/Map~Map** The OpenLayers Map instance to render layers for
- `panel` **[Element](https://developer.mozilla.org/docs/Web/API/Element)** The DOM Element into which the layer tree will be rendered
- `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Options for panel, group, and layers
  - `options.groupSelectStyle` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** either `'none'` - groups don't get a checkbox,
    `'children'` (default) groups have a checkbox and affect child visibility or
    `'group'` groups have a checkbox but do not alter child visibility (like QGIS).
  - `options.reverse` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Reverse the layer order. Defaults to true.

#### isBaseGroup

**Static** Determine if a given layer group contains base layers

**Parameters**

- `grp` **ol/layer/Group~GroupLayer** GroupLayer to test

Returns **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**

#### getGroupsAndLayers

**Static** Get an Array of all layers and groups displayed by the LayerSwitcher (has a `'title'` property)
contained by the specified map or layer group; optionally filtering via `filterFn`

**Parameters**

- `grp` **(ol/Map~Map | ol/layer/Group~GroupLayer)** The map or layer group for which layers are found.
- `filterFn` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Optional function used to filter the returned layers

Returns **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;ol/layer/Base~BaseLayer>**

#### forEachRecursive

**Static** Call the supplied function for each layer in the passed layer group
recursing nested groups.

**Parameters**

- `lyr` **ol/layer/Group~LayerGroup** The layer group to start iterating from.
- `fn` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Callback which will be called for each `ol/layer/Base~BaseLayer`
  found under `lyr`. The signature for `fn` is the same as `ol/Collection~Collection#forEach`

#### uuid

**Static** Generate a UUID
Adapted from <http://stackoverflow.com/a/2117523/526860>

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** UUID

## License

MIT (c) Matt Walker.

## Also see

If you find the layer switcher useful you might also like the
[ol-popup](https://github.com/walkermatt/ol-popup).

## Publishing

    npm run build
    # Open ./tests/ in browser
    # Open examples and manually test
    # Determine new version number (check current with `git tag --list`, check npm and GitHub)
    # Update version number in `package.json`, `bower.json` and `README.md`
    # Add entry to CHANGELOG.md
    git commit bower.json package.json CHANGELOG.md README.md
    git tag vX.Y.Z
    git push origin master --tags
    npm publish
