[Introduction](https://github.com/kristw/d3kit-timeline) |
[Demo](http://kristw.github.io/d3kit-timeline) |
**API Reference**

## d3KitTimeline

<a name="constructor" href="#constructor">#</a> var chart = new **d3KitTimeline**([options:Object]);

There are many options that you can customize. These are often set when creating the chart but also can be changed later via ```chart.options(options)```

| option  | default | description |
| ------- | ------- | ----------- |
| margin  | {left: 40, right: 20, top: 20, bottom: 20} | margin for the chart area (more like a padding) |
| initialWidth | 400 | chart width including margin |
| initialHeight | 400 | chart height including margin |
| scale | d3.scaleTime() | Can specify other type of scale e.g. `d3.scaleLinear()` |
| domain | undefined | If set, will set domain of the scale to this value. Otherwise, the domain will be calculated from the extent of data. |
| direction | 'right' | location of the labels relative to the axis |
| formatAxis | axis => axis | customize the axis before drawing, such as `axis => axis.ticks(0)` to hide all the ticks |
| keyFn | undefined | identifier function for each data point. `(d, i) => ...`|
| timeFn | `d => d.time` | accessor function for time of each data point. `(d, i) => ...`|
| textFn | `d => d.text` | accessor function for text of each data point. `(d, i) => ...`|
| labella | ```{}``` | options for Labella.js layout. See [Labella.js](https://github.com/twitter/labella.js/blob/master/docs/Force.md#constructor) documentation for more details. For example, to set maxixum position for the labels to 500, set this option to `{maxPos: 500}` |
| layerGap | 60 | distance from axis to the first layer of labels and between each layer of labels (in situations where all labels cannot fit within one layer) |
| dotRadius | 3 | radius of the dots. It can be a Number or Function `(d, i) => ...` |
| dotColor | #222 | color of the dots. It can be a color value or Function `(d, i) => ...` |
| labelBgColor | #222 | color of the label background. It can be a color value or Function `(d, i) => ...` |
| labelTextColor | #fff | color of the label text. It can be a color value or Function `(d, i) => ...` |
| linkColor | #222 | color of the paths that link dots to labels. It can be a color value or Function `(d, i) => ...` |
| labelPadding | {left: 4, right: 4, top: 3, bottom: 2} | space to add around the text within each label |
| textYOffset | 0.85em | vertical offset for text within label |
| textStyle | null | style for label text. It must be an object with style field as key, the value can be constant or `(d, i) => ...`. Any style field for svg `<text>` is applicable. See an example below |

```javascript
var options = {
  textStyle: {
    'fill': '#fff',
    'text-decoration' : function(d){ return d.team==='BRA'? 'none': 'underline'},
    'font-weight': function(d){ return d.team==='BRA'? 700: 400}
  }
};
```

### Functions

<a name="data" href="#data">#</a> chart.**data**([data:Array])

Get/Set data for this chart, inherited from [skeleton.data()](https://github.com/twitter/d3kit/wiki/Skeleton#data) in d3Kit.

<a name="options" href="#options">#</a> chart.**options**([options:Object])

Get/Set options for this chart, inherited from [skeleton.options()](https://github.com/twitter/d3kit/wiki/Skeleton#options) in d3Kit. See the list of options from the top of this page.

<a name="on" href="#on">#</a> chart.**on**(eventName:String, handler:Function)

These events are included with d3Kit-timeline. The handler function signature is ```function(d,i){...}``` where ```d``` is the data associated with label and ```i``` is index of the data point.

| name | description |
| ---- | ----------- |
| 'dotClick' | Click on a dot on the timeline |
| 'dotMouseover' | Move cursor into a dot on the timeline |
| 'dotMousemove' | Move cursor within a dot on the timeline |
| 'dotMouseout' | Move cursor out of a dot on the timeline |
| 'dotMouseenter' | Move cursor within a dot on the timeline |
| 'dotMouseleave' | Move cursor out of a dot on the timeline |
| 'labelClick' | Click on a label |
| 'labelMouseover' | Move cursor into a label |
| 'labelMousemove' | Move cursor within a label |
| 'labelMouseout' | Move cursor out of a label |
| 'labelMouseenter' | Move cursor within a label |
| 'labelMouseleave' | Move cursor out of a label |

<a name="resizeToFit" href="#resizeToFit">#</a> chart.**resizeToFit**()

If the direction is *left* or *right*, it will set the width automatically. If the direction is *up* or *down*, it will set the height automatically.
Must be called after `.updateDimensionNow()`