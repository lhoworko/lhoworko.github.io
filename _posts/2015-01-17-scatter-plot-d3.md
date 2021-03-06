---
layout: post
title: Scatter Plot in D3
---


For my first tutorial we are going to go through the process of making an updatable scatter plot in D3. By the end of the post you should have an understanding of how to add arbitrary data points to the chart, as well as smoothly transition them as data is changed or updated. This is the first of what will hopefully be a series of D3 tutorials. Lets get started.

<!--excerpt-->

{% include scatter_plot_d3/basics.html %}

So first things first lets make a basic html page and include the D3.js script.

{% highlight html %}
<!doctype html>
<head>
    <meta charset="utf-8">
    <title>D3 Scatter Plot</title>
    <style>

    </style>
</head>
<body>
    <script src="http://d3js.org/d3.v3.min.js"></script>
    <script>

    </script>
</body>
{% endhighlight %}

To be able to view progress as we go you will need to run a web server. The easiest one I have found is python's SimpleHTTPServer. From the command line run the following: 

{% highlight bash %}
    python -m SimpleHTTPServer
{% endhighlight %}

and navigate to localhost:8000.

## Scales

The first thing we will add to our code other than the basic variables is the x and y linear scales. What these do is map the input data to an output pixel value for the chart. It's definitely possible to manually do this math, but D3 just makes it so much easier. Take a look [here](http://alignedleft.com/tutorials/d3/scales) for a very in depth explanation of linear scales. As for the data used in this example we will be using random points between 0 and 1. All of the following goes inside the empty html script tags.

{% highlight javascript %}
var width = 600,
    height = 400,
    data = [];

var margin = {
    "left": 15,
    "top": 5,
    "right": 5,
    "bottom": 15
}

var chart_width = width - margin.left - margin.right,
    chart_height = height - margin.top - margin.bottom;

var x = d3.scale.linear()
        .domain([0, 1])
        .range([0, chart_width);

var y = d3.scale.linear()
        .domain([0, 1])
        .range([chart_height, 0]);
{% endhighlight %}

## SVG

The first thing we need to add to the page is a place to put the chart. Everything needs to be within an svg tag. To group the chart pieces together we will also add a g element. This allows us to offset the contents of the g element by the margins so that we don't have to do so individually with every element. An example would be if we want to move a bunch of books to the left by one foot, it's easier to have all the books in a box which is moved, rather than moving each book one by one.

{% highlight javascript %}
// Create the svg element to hold the chart.
var svg = d3.select("body")
        .append("svg")
        .attr("width", width)
        .attr("height", height);

// Create the g element inside the svg element. 
// Translate it left by margin.left, and down by margin.top.
var chartGroup = svg.append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
{% endhighlight %}

## Axes

Next is the x and y axes. We will use the x and y scales to let each axis know how long to be (from the range), and what values to have (from the domain). The xAxis and yAxis variables goes after the x and y scale variable initializations and the svg initialization.

{% highlight javascript %}
// Create an x axis and scale it by the x scale.
var xAxis = d3.svg.axis()
        .scale(x);

// Similarly for the y axis.
var yAxis = d3.svg.axis()
        .scale(y);
{% endhighlight %}

Now we need to add the axes to the chart. Looking back at the book example above, we want to put the axes inside the chartGroup, or the box.

{% highlight javascript %}
// Create a new group to hold the x axis. Calling .call(xAxis) will init the axis.
chartGroup.append("g")
        .attr("class", "x axis")
        .call(xAxis);

// Similarly for the y axis.
chartGroup.append("g")
        .attr("class", "y axis")
        .call(yAxis);
{% endhighlight %}

Lets take our first look at what we have so far. If you haven't yet started the HTTP server do that now and go to localhost:8000. You should have something like this..

<div class="scatter" id="scatter1"></div>
{% include scatter_plot_d3/scatter1.html %}

This is a good start but obviously not what we want. We need to rotate the yAxis to be on the left, and shift the xAxis to be at the bottom. This is a simple fix, just modify the code like so.

{% highlight javascript %}
...
// Orient the yAxis to be on the left.
var yAxis = d3.svg.axis()
        .orient('left')
        .scale(y);
...
// Notice the new translate line.
chartGroup.append("g")
        .attr("class", "x axis")
        .attr("transform", "translate(0," + chart_height + ")")
        .call(xAxis);
{% endhighlight %}

We will also make the axes a bit cleaner with the following css rules.

{% highlight html %}
<style>
    body {
        font: 12px sans-serif;
    }

    .axis path,
    .axis line {
        fill: none;
        stroke: #000;
        shape-rendering: crispEdges;
    }
</style>
{% endhighlight %}

We now have something like this..

<div class="scatter" id="scatter2"></div>
{% include scatter_plot_d3/scatter2.html %}

Much better.

## Data

If you were making a static chart you would add the data points at this point. What we want to do is add 100 data points, then every second move them around the chart. The way we will do this is every second we will generate 100 new data points. These points will be either added to the chart (on the first update) or move to their new location. This will demonstrate the use of D3 transitions and enter.

Lets make a function that we will be calling every second. Call it update.

{% highlight javascript %}
function update() {
    // Add 100 random points to the data array.
    for (var i = 0; i < 100; i++) {
        data[i] = [Math.random(), Math.random()];
    }

    // Enter the data points onto the chart.
    chartGroup.selectAll("circle")
            .data(data)
            .enter()
            .append("circle")
            .attr("r", 5);

    // Move the points to their new locations.
    chartGroup.selectAll("circle")
            .attr("transform", function (d) {
                return "translate(" + x(d[0]) + "," + y(d[1]) + ")";
            })

    setTimeout(update, 1000);
}

update();
{% endhighlight %}

This can be a bit much to digest. I can't do enter() justice, so please take a look at [Three Little Circles](http://bost.ocks.org/mike/circles/) as it nicely explains how this works. The basics of it is that every call to update causes the circles to move to their new position.

Lets take another look at what we have..

<div class="scatter" id="scatter3"></div>
{% include scatter_plot_d3/scatter3.html %}

## Transition

You will notice that on each update the circles disapear and appear at their new location. Lets make them nicely slide there instead. This is easily done with D3 transitions. In the second chartGroup bit simply add the lines .transition and .duration.

{% highlight javascript %}
// Notice the transition and duration lines.
chartGroup.selectAll("circle")
        .transition()
        .duration(800)
        .attr("transform", function (d) {
            return "translate(" + x(d[0]) + "," + y(d[1]) + ")";
})
{% endhighlight %}

That's it. Seriously. You don't even need the duration line as if it's omitted, a default value of 250ms is used.

Now after all of that we have the following. Seems almost funny that it's more difficult to get the axes correct than adding and moving data points.

<div class="scatter" id="scatter4"></div>
{% include scatter_plot_d3/scatter4.html %}

There is much more we could do to make the chart better, but that's all for this tutorial. If you made it this far thanks for reading. Hopefully I'll have more D3 stuff up shortly.

Full code can be found [here](http://bl.ocks.org/lhoworko/ef36fdd4e7315978925b).
