# g-chartframe
_0.2.0 Relese notes: The default frame types are now made by functions rather than provided as constants_


For making the boring but necessary stuff on D3 charts in as painless a fashion as possible.

## Installation

If you use NPM, `npm install @financial-times/g-chartframe`(er... not yet!). Otherwise, download the [latest release](https://github.com/ft-interactive/g-chartframe/releases/latest).

## Use

Preconfigured frames...

```
const webframe = gChartframe.webFrame;
webframe.title('A simple chart')
	.subtitle('showing some interesting things')
	.source('source: FT research|FT Graphic Tom Pearson');

d3.select('.web-chart-container svg')
	.call(webframe);

webframe.plot()
	...add your visualisation code here...

```

Configure your own frame...
```
const myFrame = gChartframe.frame()
	.width(350)
	.height(350)
	.margin({top:20,left:20,bottom:20,right:20,})
	.title('My totally custom title')
	.subtitle('hello hello hello')

d3.select('.custom-chart-container')
	.append('svg')
	.call(myFrame);
```

## API Reference

![reference image indicating whcih properties refer to which bits of the chart frame](https://raw.githubusercontent.com/ft-interactive/g-chartframe/master/markup-frame.png)



<a id="frame-backgroundColour" href="#frame-backgroundColour">#</a>frame.**backgroundColour(_string_)**

Set the background colour of the frame. For the single argument you can use the same css color naming schemes that you use in HTML, whether that's color names (that is red), rgb values (that is rgb(255,0,0)), hex values, rgba values, etc. If no argument is specified returns the current value.

```
myFrame.backgroundColour('#00FF00');
```

<a id="frame-containerClass" href="#frame-containerClass">#</a>frame.**containerClass(_string_)**

Set the class assigned to the containing SVG element. This allows you to select the frame later and to define CSS styles pertaining only to its contents. If no argument is specified returns the current value.

```
myFrame.containerClass('special-frame');
```
would allow you to target the frames contents in your CSS like this...
```
.special-frame line{
	stroke-width:2;
	stroke:#00FF00;
	stroke-opacity:0.5;
	fill:none;
}
```

<a id="frame-dimension" href="#frame-dimension">#</a>frame.**dimension()**

This returns an object with the `height` and `width` of the suggested plot area. This is useful for determining the range of scales.
If no argument is specified returns the current value.

```
const dimension = myFrame.dimension(); // e.g. { width: 200 ,height: 550,}
const horizontalScale = d3.linearScale()
	.range([0, dimension.width]);

const verticalScale = d.lineaScale()
	.range([dimension.height, 0]);
```

<a id="frame-height" href="#frame-height">#</a>frame.**height(_number_)**

Set the height for the frames container (typically be an SVG).
If no argument is specified returns the current value.

<a id="frame-margin" href="#frame-margin">#</a>frame.**margin(_[{[top:number], [left:number], [bottom:number], [right:number],}]_)**

Set the margins for the frame follwing the <a href="https://bl.ocks.org/mbostock/3019563">D3 margin convention</a>.
If no argument is specified returns the current value.

<a id="frame-plot" href="#frame-plot">#</a>frame.**plot()**

This returns a d3 selection of the frames plot group. This is where the graphical elements of the chart can be appended.

```
const plot = myFrame.plot();

plot.selectAll('rect')
	.data(theData)
	.enter()
	.append('rect')
	...

```

<a id="frame-source" href="#frame-source">#</a>frame.**source(_[string]_)**

A string describes the source of the graphic's data, line breaks can be added with the `|` character. The property can also be used to add notes, credits etc. If no argument is specified returns the current value.

```
myFrame.source('Source:FT Research|Graphic: Pam Ampersand');

```

<a id="frame-sourceLineHeight" href="#frame-sourceLineHeight">#</a>frame.**sourceLineHeight(_[number]_)**

Set the line height for the graphic's source text. If no argument is specified returns the current value.

<a id="frame-sourceStyle" href="#frame-sourceStyle">#</a>frame.**sourceStyle(_[{attribute:value}]_)**

Set the appearnce of the graphic's source text. A series of attributes are added to the text element with the specified values. If no argument is specified returns the current value.

```
myFrame.sourceStyle({
	'font-family':'Sans-serif, Helvetica',
	'fill':'#00FF00';
	...
});
```

will result in a text element that looks like...

```
<text class="chart-source"><tspan y="477" x="4" font-family="Sans-serif, Helvetica" fill="#00FF00">Source text</tspan></text>
```

<a id="frame-sourceX" href="#frame-sourceX">#</a>frame.**sourceX(_[number]_)**

Set the X translation of the graphic's source text. If no argument is specified returns the current value.

<a id="frame-sourceY" href="#frame-sourceY">#</a>frame.**sourceY(_[number]_)**

Set the Y translation of the graphic's source text. If no argument is specified returns the current value.

<a id="frame-subtitle" href="#frame-subtitle">#</a>frame.**subtitle(_[string]_)** similar to <a href="#frame-source">_source_</a>

<a id="frame-subtitleLineHeight" href="#frame-subtitleLineHeight">#</a>frame.**subtitleLineHeight(_[number]_)** similar to <a href="#frame-sourceLineHeight">_sourceLineHeight_</a>

<a id="frame-subtitleStyle" href="#frame-subtitleStyle">#</a>frame.**subtitleStyle(_[{attribute:value}]_)** similar to <a href="#frame-sourceStyle">_sourceStyle_</a>

<a id="frame-subtitleX" href="#frame-subtitleX">#</a>frame.**subtitleX(_[number]_)** similar to <a href="#frame-sourceLineX">_sourceX_</a>

<a id="frame-subtitleY" href="#frame-subtitleY">#</a>frame.**subtitleY(_[number]_)** similar to <a href="#frame-sourceY">_sourceY_</a>

<a id="frame-title" href="#frame-title">#</a>frame.**title(_[string]_)** similar to <a href="#frame-source">_source_</a>

<a id="frame-titleStyle" href="#frame-titleStyle">#</a>frame.**titleStyle(_[number]_)** similar to <a href="#frame-sourceStyle">_sourceStyle_</a>

<a id="frame-titleLineHeight" href="#frame-titleLineHeight">#</a>frame.**titleLineHeight(_[number]_)** similar to <a href="#frame-sourceLineHeight">_sourceLineHeight_</a>

<a id="frame-titleX" href="#frame-titleX">#</a>frame.**titleX(_[number]_)** similar to <a href="#frame-sourceLineX">_sourceX_</a>

<a id="frame-titleY" href="#frame-titleY">#</a>frame.**titleY(_[number]_)** similar to <a href="#frame-sourceY">_sourceY_</a>

<a id="frame-units" href="#frame-units">#</a>frame.**units(_[string]_)**

Set the units in which the Height and Width are set. At the moment the only useful argument is 'mm' which allows you to specify height and width in mm -- useful for print. If no argument is specified returns the current value.

<a id="frame-watermark" href="#frame-watermark">#</a>frame.**watermark(_[svgnodes]_)**

The user can supply arbitrary SVG markup as a string. THis will be used as the watermark for the graphic. If no argument is specified returns the current value.

<a id="frame-watermarkLocation" href="#frame-watermarkLocation">#</a>frame.**watermarkLocation(_[href]_)** 

The user can set a URL for a watermark SVG to be used.

<a id="frame-width" href="#frame-width">#</a>frame.**width(_[number]_)**


Set the height for the frames container (typically be an SVG).
If no argument is specified returns the current value.


👉 _Note_: If the chart frame is being called on an SVG element the width, height and title functions will re-write those properties of the parent SVG. If you don't want this to happen you can avoid it by calling the function on a group element instead.

--

Copyright (c) 2015, 2016, 2017 Fiancial Times
