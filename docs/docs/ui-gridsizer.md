## Introduction

Layout children game objects in grids.

- Author: Rex
- Game object

## Live demos

- [Scrollable grids](https://codepen.io/rexrainbow/pen/YMyBom)
- [Full viewport](https://codepen.io/rexrainbow/pen/LYVKXJg)

## Usage

[Sample code](https://github.com/rexrainbow/phaser3-rex-notes/tree/master/examples/ui-gridsizer)

### Install plugin

#### Load minify file

- Load plugin (minify file) in preload stage
    ```javascript
    scene.load.scenePlugin('rexuiplugin', 'https://raw.githubusercontent.com/rexrainbow/phaser3-rex-notes/master/dist/rexuiplugin.min.js', 'rexUI', 'rexUI');
    ```
- Add sizer object
    ```javascript
    var sizer = scene.rexUI.add.gridSizer(config);
    ```

#### Import plugin

- Install rex plugins from npm
    ```
    npm i phaser3-rex-plugins
    ```
- Install plugin in [configuration of game](game.md#configuration)
    ```javascript
    import UIPlugin from 'phaser3-rex-plugins/templates/ui/ui-plugin.js';
    var config = {
        // ...
        plugins: {
            scene: [{
                key: 'rexUI',
                plugin: UIPlugin,
                mapping: 'rexUI'
            },
            // ...
            ]
        }
        // ...
    };
    var game = new Phaser.Game(config);
    ```
- Add sizer object
    ```javascript
    var sizer = scene.rexUI.add.gridSizer(config);
    ```

#### Import class

- Install rex plugins from npm
    ```
    npm i phaser3-rex-plugins
    ```
- Import class
    ```javascript
    import { GridSizer } from 'phaser3-rex-plugins/templates/ui/ui-components.js';
    ```
- Add sizer object
    ```javascript    
    var sizer = new GridSizer(scene, config);
    sscene.add.existing(sizer);
    ```

### Add grid sizer object

```javascript
var gridSizer = scene.rexUI.add.gridSizer({
    // x: 0,
    // y: 0,
    // anchor: undefined,
    // width: undefined,
    // height: undefined,

    column: 0,
    row: 0,
    // columnProportions: undefined,
    // rowProportions: undefined,
    // space: {
    //     left: 0, right: 0, top: 0, bottom:0,
    //     column: 0, // [0, 0, 0]
    //     row: 0     // [0, 0, 0]
    // },

    // name: '',
    // draggable: false
});
```

or

```javascript
var gridSizer = scene.rexUI.add.gridSizer(x, y, {
    column: 0,
    row: 0,
    // columnProportions: undefined,
    // rowProportions: undefined,

    // space: {
    //     left: 0, right: 0, top: 0, bottom:0,
    //     column: 0, // [0, 0, 0]
    //     row: 0     // [0, 0, 0]
    // },

    // width: undefined,
    // height: undefined
});
```

or

```javascript
var gridSizer = scene.rexUI.add.gridSizer(x, y, width, height, {
    column: 0,
    row: 0,
    // columnProportions: undefined,
    // rowProportions: undefined,

    // space: {
    //     left: 0, right: 0, top: 0, bottom:0,
    //     column: 0, // [0, 0, 0]
    //     row: 0     // [0, 0, 0]
    // },    
});
```

or

```javascript
var gridSizer = scene.rexUI.add.gridSizer(x, y, width, height, column, row, {
    // space: {
    //     left: 0, right: 0, top: 0, bottom:0,
    //     column: 0, // [0, 0, 0]
    //     row: 0     // [0, 0, 0]
    // },

    // name: '',
    // draggable: false
});
```

- `x`, `y` : Position of this object, it is valid when this object is the top object.
- `anchor` : See [anchor](anchor.md#create-instance).
    - `left`, `right`, `centerX`, `x`, `top`, `bottom`, `centerY`, `y` : Position based on visible window, which composed of
        - Percentage of visible width/height : `'p%'`, p: `0` ~ `100`.
            - `'left'`(=0%), `'center'`(=50%), `'right'`(=100%)
            - `'top'`(=0%), `'center'`(=50%), `'bottom'`(=100%)
        - Offset : `'+n'`, or `'-n'`.
- `width` : Minimum width. i.e. Width of this gridSizer will larger then this value.
- `height` : Minimum height. i.e. Hieght of this gridSizer will larger then this value.
- `column` : Amount of column grids.
- `row` : Amount of row grids.
- `columnProportions`, `rowProportions` : Proportion of each column/row.
    - Number : Apply this number proportion to each column/row
    - Number array : Apply proportion of column/row through elements of this number array.
- `space` : Pads spaces.
    - `space.left`, `space.right`, `space.top`, `space.bottom` : Space of bounds.
    - `space.column` : Space between 2 columns
        - A number
        - A number array
    - `space.row` : Space between 2 rows
        - A number
        - A number array

### Custom class

- Define class
    ```javascript
    class MyGridSizer extends RexPlugins.UI.GridSizer {
        constructor(scene, x, y, minWidth, minHeight, column, row) {
            super(scene, x, y, minWidth, minHeight, column, row);
            // ...
            scene.add.existing(this);
        }
        // ...
    }
    ```
- Create instance
    ```javascript
    var gridSizer = new MyGridSizer(scene, x, y, minWidth, minHeight, column, row);
    ```

### Add background

```javascript
gridSizer.addBackground(child);
```

### Add child

Add a game obejct to grid sizer

```javascript
gridSizer.add(child, column, row);
```

or

```javascript
gridSizer.add(child, column, row, align, padding, expand, key);
```

or

```javascript
gridSizer.add(child, 
    {
        column: 0, 
        row: 0, 
        align: 'center', 
        padding: {left: 0, right: 0, top: 0, bottom: 0}, 
        expand: false, 
        key: undefined
    }
);
```

- `child` : A game object
- `column`, `row` : Index of grid to add.
- `align` :
    - `'center'`, or `Phaser.Display.Align.CENTER` : Align game object at center. Default value.
    - `'left'`, or `Phaser.Display.Align.LEFT_CENTER` : Align game object at left-center.
    - `'right'`, or `Phaser.Display.Align.RIGHT_CENTER` : Align game object at right-center.
    - `'top'`, or `Phaser.Display.Align.RIGHT_CENTER` : Align game object at top-center.
    - `'bottom'`, or `Phaser.Display.Align.BOTTOM_CENTER` : Align game object at bottom-center.
- `padding` : Add space between bounds. Default is 0.
    - A number for left/right/top/bottom bounds
    - Or a plain object
        ```javascript
        {
            left: 0,
            right: 0,
            top: 0,
            bottom: 0
        }
        ```
- `expand` : Set `true` to height and width.
- `key` : Add this child into childMap, which could be read back by `sizer.getElement(key)`.
    - `undefined` : Don't add this child. Default value.

### Proportion

Set proportion of each column or row via

```javascript
gridSizer.setColumnProportion(columnIndex, proportion);
gridSizer.setRowProportion(rowIndex, proportion);
```

### Layout children

Arrange position of all children.

```javascript
gridSizer.layout();
```

See also - [dirty](ui-basesizer.md#dirty)

### Grid index <-> child

- Grid index -> child
    ```javascript
    var child = gridSizer.getChildAt(columnIndex, rowIndex);
    ```
- Child -> grid index
    ```javascript
    var gridIndex = gridSizer.childToGridIndex(child);
    // var gridIndex = gridSizer.childToGridIndex(child, out);
    ```
    - `gridIndex` : `{x, y}`, or `null` if child is not belong this sizer.

### Remove child

- Remove a child
    ```javascript
    gridSizer.remove(child);    
    ```
    or
    ```javascript
    gridSizer.removeAt(columnIndex, rowIndex);    
    ```
- Remove and destroy a child
    ```javascript
    gridSizer.remove(child, true);
    ```
    or
    ```javascript
    gridSizer.removeAt(columnIndex, rowIndex, true);    
    ```    
- Remove all children
    ```javascript
    gridSizer.clear();
    ```
- Remove and destroy all children
    ```javascript
    gridSizer.clear(true);
    ```

### Grid size

- Amount of column
    ```javascript
    var columnCount = gridSizer.columnCount;
    ```
- Amount of row
    ```javascript
    var rowCount = gridSizer.rowCount;
    ```

### Get element

- Get element
    - All children items
        ```javascript
        var items = gridSizer.getElement('items');
        ```
- Get by name
    ```javascript
    var gameObject = gridSizer.getElement('#' + name);
    // var gameObject = gridSizer.getElement('#' + name, recursive);
    ```
    or
    ```javascript
    var gameObject = gridSizer.getByName('#' + name);
    // var gameObject = gridSizer.getByName('#' + name, recursive);
    ```
    - `recursive` : Set `true` to search all children recursively.

### Set children interactive

```javascript
sizer.setChildrenInteractive({
    // click: {mode: 'release', clickInterval: 100},

    // over: undefined,
    
    // press: {time: 251, threshold: 9},

    // tap: {time: 250, tapInterval: 200, threshold: 9, tapOffset: 10, 
    //       taps: undefined, minTaps: undefined, maxTaps: undefined,},

    // swipe: {threshold: 10, velocityThreshold: 1000, dir: '8dir'},

    // inputEventPrefix: 'child.',
    // eventEmitter: undefined
})
```

- `click` : [Configuration](button.md#create-instance) of Button behavior.
    - `false` : Don't install Button behavior.
- `over` :
    - `false` : Don't fire over/out events
- `press` : [Configuration](gesture-press.md#create-instance) of Press behavior.
    - `false` : Don't install Press behavior.
- `tap` : [Configuration](gesture-tap.md#create-instance) of Tap behavior.
    - `false` : Don't install Tap behavior.
- `swipe` : [Configuration](gesture-swipe.md#create-instance) of Swipe behavior.
    - `false` : Don't install Swipe behavior.
- `inputEventPrefix` : Prefix string of each event, default is `'child.'`.
- `eventEmitter` : Fire event through specific game object.

!!! note
    Input behaviors are installed to this Sizer game object, not each child. And it assumes that all children are not overlapped.
    Use [Grid-Button](ui-buttons.md) if user needs to enable/disable input behaviors of each child individually.

#### Events

- Click
    ```javascript
    sizer.on('child.click', function(child, pointer) { 
        // ...
    }, scope);
    ```
    - `child` : Triggered child game object.
    - `pointer` : [Pointer](touchevents.md#properties-of-point) object.    
- Pointer-over
    ```javascript
    sizer.on('child.over', function(child, pointer) { 
        // ...
    }, scope);
    ```
- Pointer-out
    ```javascript
    sizer.on('child.out', function(child, pointer) { 
        // ...
    }, scope);
    ```
- Press
    ```javascript
    sizer.on('child.pressstart', function(child, pointer) { 
        // ...
    }, scope);
    ```
    ```javascript
    sizer.on('child.pressend', function(child, pointer) { 
        // ...
    }, scope);
    ```
- Tap
    ```javascript
    sizer.on(tapEventName, function(child, pointer) { 
        // ...
    }, scope);
    ```
    - `tapEventName` :  `'child.1tap'`, `'child.2tap'`, `'child.3tap'`, etc ...
- Swipe
    ```javascript
    sizer.on(swipeEventName, function(child, pointer) { 
        // ...
    }, scope);
    ```
    - `swipeEventName` :  `'child.swipeleft'`, `'child.swiperight'`, `'child.swipeup'`, `'child.swipedown'`.

### Other properties

See [base sizer object](ui-basesizer.md).