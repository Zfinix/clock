## TODO

* Composition no repaint boundary because no paints are passed up to it (children that could mark it dirty due to animating are repaint boundaries).

* Create spin-up animation for when the widget is created or updated?

  + Weather comoponent and thermometer come in from left and right, slide and ball from top, and clock scales up.

  + The whole composition is transformed from x rotation `-pi / 2` to `0` and maybe skewed.

  + This could show that the goo actually reacts to the components (even more than the ball push already does).

* Ideas for weather condition animations:

  + Thunderstorm: make the raindrops animate as can be seen [here](https://cdn.dribbble.com/users/2120934/screenshots/6193517/17_tstorm.gif?vid=1).

  + Cloudy: parallax movement of the different clouds.

  + Foggy: ping pong movement of all the bars that is easy on the eyes (needs a curve).

* Find better start and end positions for the ball.

* Use these colors for a color palette: https://www.dwitter.net/d/5455

  + Ensure that sufficient contrast is present for accessibility reasons.

* Effects/filter ideas:

  + Push some subtle animated transforms (in `CompositedClock` ?) that introduce some nice perspective changes.

    - Potentially rotate whole components because it better shows what the individual parts are :)

  + Add some texture over components, e.g.</a> metal-like, wood-like, or just w/e looks interesting.

  + Take inspiration from https://github.com/JustinFincher/FlutterClock.

  + Check https://github.com/gskinnerTeam/flutter_vignettes/tree/master/vignettes/indie_3d for the blending effect.

* Finish all eight themes and ensure that dark mode, light mode, subtle, and vibrant look proper.

  + Choose one as the default scheme for the submission.

<hr>

* Check [**7.** "JUDGING"](https://docs.google.com/document/d/1ybyQCK8Sy7vrD9wuc6pbgwVkyrVZ7Rd_41r5NXGqlt8/edit?usp=sharing).

* Format code and follow all other steps decribed [here](https://flutter.dev/clock#submissions).

* Remove unnecessary depencies and other stuff. For example, `pedantic` or `uses-material-design` if there are no icons in the final design.

* Submit submission :)

  + https://flutter.dev/clock - Check rules and FAQ before that.

  + Remove TODOs.

* Add GIF to README.

* Make repository public.

  + Make clock available on web via GitHub pages.

    - Watch "Designing for the Web with Flutter" from Flutter Interact for this.

* Write article about the creation process of the submission on Flutter Community.

  + Ideally go into details regarding the different stages of the process providing images and maybe snapshots by linking to a particular commit on GitHub.

  + Share some of the technical details that make this submission special apart from what can be seen looking at it.

    - For example: what kinds of `RenderObject` s were used and information about `Canvas` and Bézier curves (the simple quadratic and cubic ones `Canvas` offers).

    - Mention that people can, if they are interested in doing custom layouts but `MultiChildRenderObjectWidget` seems too complicated for them, check out https://stackoverflow.com/a/59483482/6509751 to get started with `CustomMultiChildLayout` .

  + The title could be something like "How I made a Flutter Clock Face using only Custom Canvas", everything painted by Flutter's `Canvas` manually and no use of prebuilt widgets.

  + Consider embedding some visualizations made by https://debugger.skia.org/.

    - Make sure to replace all `Paint.shader` properties by solid colors when taking the screenshots because the debugger seems to not be able to render shaders (https://stackoverflow.com/q/59589892/6509751).

    - Capture using `flutter screenshot --type=skia --observatory-uri=..` .

  + Mention `RenderObject.isRepaintBoundary` for performance optimizations (did not use raster caching) and `RepaintBoundary` for widgets.

    - Show illustrations with the **repaint rainbow** enabled.

  + Can also play with commenting components out from the paint order.

  + Add an "Everything is implicitly animated" screen recording, where the model values are modified programmatically.

  + Mention that usually accessibility and with that semantics are taken care of by prebuilt widgets, but for this clock face it was necessary to do it manually, i.e.</a> override [ `RenderObject.describeSemanticsConfiguration` ](https://api.flutter.dev/flutter/rendering/RenderObject/describeSemanticsConfiguration.html) .

  + Add link to it to README.

  + Potentially post it on https://dev.to/.

  + Share on FlutterDev: Twitter, Reddit, and Discord.

* Share with P.

# clock | [View demo](https://creativecreatorormaybenot.github.io/clock) | [Read article](https://medium.com/flutter-community/) | [![Twitter Follow](https://img.shields.io/twitter/follow/creativemaybeno?label=Follow%20me&style=social)](https://twitter.com/creativemaybeno)

[creativecreatorormaybenot](https://github.com/creativecreatorormaybenot)'s entry to the [Flutter clock challenge](https://flutter.dev/clock).
This is a playful clock display and uses exclusively the Flutter `Canvas` to draw everything you see on screen. That means that there are no assets, plugins, and not even prebuilt widgets used, i.e.</a> every `RenderObject` in the tree was custom made by me.

![Quick screen capture showing the final result of the submission]()

The code entry point for the clock face is [ `canvas_clock/lib/main.dart` ](https://github.com/creativecreatorormaybenot/clock/blob/master/canvas_clock/lib/main.dart).

## Notes

* I was inspired by the design of an old analog barometer and hygrometer kind of device initially and took many design ideas away from that. Later on, many other inspirations came my way :)

* You can follow my whole process of building the clock face in this repository, i.e.</a> every bit of it. Maybe it helps someone :)

### Hand bouncing

* For the animation of the second hand (and minute hand) bouncing of the analog clock, I enjoyed looking at this [slow motion capture of a watch](https://youtu.be/tyl7-gHRBX8?t=29) (the important part is blurry (:, yes).

### Implementation

* No plugins were used at all (check [ `pubspec.yaml` ](https://github.com/creativecreatorormaybenot/clock/blob/master/canvas_clock/pubspec.yaml)).

* No premade widgets from the standard library were used in my own code, i.e.</a> every `RenderObject` in the tree of the clock was custom created by me.

  + Accessibility was implemented customly and it had to because I did not use any prebuilt widgets that come with `Semantics` implementations. Instead I overrode [ `RenderObject.describeSemanticsConfiguration` ](https://api.flutter.dev/flutter/rendering/RenderObject/describeSemanticsConfiguration.html) for every component with semantic relevance.

* No assets were used. The bullet point would be a bit short without this second sentence.

* I did not go with the raw layer (here is an [old demonstration](https://github.com/creativecreatorormaybenot/pong) of the Flutter raw layer I did) nor the rendering layer.<br>This was not compatible with the `ClockCustomizer` and is also not convenient for working with data at all. The Flutter trees are pretty neat, so we should use them (they make the app reactive) :)

