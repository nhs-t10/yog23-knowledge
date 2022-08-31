# Making a CV Pipeline

All CV analysis is done in a pipeline. CVManager's pipelines will extend `PipelineThatExposesSomeAnalysis`. To make a CV pipeline, first **make a new class** in the `managers.CV` package, and then make sure it `extends PipelineThatExposesSomeAnalysis`.

```java
package org.firstinspires.ftc.teamcode.managers.CV;

public class SamplePipeline extends PipelineThatExposesSomeAnalysis {

}
```

## Adding Structure Methods

When you add the pipeline, you *must* implement two methods: `int getAnalysis() {}` and `Mat processFrame(Mat input) {}`. Mat is short for "Matrix"-- it's an image in OpenCV. `processFrame` will do all of the work in the CV pipeline.

## Doing the Work

This is the tricky part. Because of memory concerns (CV is tough on performance), you *may not* make any local Object variables in the `processFrame` method. Instead, you have to make *fields* on the `Pipeline` object and reuse them-- see `FancyPantsEdgeDetectionPipeline` for an example of that. 

Other than that note, pipeline-writing can be broken down into several steps.

If you want to, you can just search online-- chances are, someone's done an FTC pipeline before. You can also adapt `FancyPantsEdgeDetectionPipeline` for your use-case. 

Otherwise, writing a pipeline from scratch!

### Pipeline Processing: Breaking Down the Problem

Most FTC games involve determining whether a coloured object is on the right side, the left side, or the middle. First, break down the problem into simpler steps:

1. Determine position of object
2. Check if position is right, left, or center

### Determining the Position

To figure out where a colour is, first try to filter it out into a color mask. [This Michael Reeves video](https://youtu.be/USKD3vPD6ZA?t=112) is a bit profane, but it's a good explanation of how color-masking works.

After you have a colour mask, you need to find the "contours"-- connected blobs of coloured pixels. Use `Imgproc.findContours` for this.

Next, the **biggest** contour will be the object you're looking for, so loop through the contours list and calculate the biggest. You can use `Imgproc.boundingRect(contour).area()` to find the area of a contour quickly.

After you have the contour of your object, you need to calculate an x-position. To do that, find its bounding rectangle (the smallest rectangle that covers the contour) with `contourRect = Imgproc.boundingRect(contour)`, and calculate its horizontal center with `contourRect.x + (contourRect.width / 2f)`!

You're done! You have the x-coordinate-- from here, it's just checking if it's left, right, or center.

### Checking if a coordinate is left, right, or center 

Having an x-coordinate in pixels means that, in order to calculate the percentage, you need to have the width in pixels too. To get the width, use `input.width()`-- `input` is the `Mat` parameter that `processFrame` takes.

Zero is the *left* side of the screen, so with the percentage, you can use something like this:

```java
this.centerPercentage = centerX / (double)input.width();

if(centerPercentage < 0.33) {
    this.position = 0;
} else if(centerPercentage < 0.66) {
    this.position = 1;
} else {
    this.position = 2;
}
```

Note that it's *not* `return`ing the position. Instead, it sets the position to an instance variable. Because OpenCV requires us to `return` the `Mat`, this is necessary to get the `position` out of the pipeline.

## Getting the Position from the Pipeline

After you've written the `processFrame` method, you need to update `getAnalysis`! Instead of the auto-generated `return 0`, have it `return this.position`.

Your pipeline is complete! 

If you want, you can also implement the `float getAnalysisPrecise()` method-- usually, this will `return this.centerPercentage`.
