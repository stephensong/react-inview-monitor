# react-inview-monitor

[![NPM version](https://badge.fury.io/js/react-inview-monitor.svg)](https://www.npmjs.com/package/react-inview-monitor)

## Easy to use, declarative scroll into view component for animations and more
[See the demos for some example usage](https://snipsco.github.io/react-inview-monitor/).

There are other ~ scoll monitor libraries for React available, but none of them solved our use cases: to be able to declaratively configure animations and other effects to be
triggered when individual elements came into the view. Inspired by the [wow reveal animation library](http://mynameismatthieu.com/WOW/) we set out to get to the same ease of use but within react's code paradigm.

Note: this library is not neither an overly generic, comprehensive, nor low-level solution to managing scrolling. If you're desiring to solve one of the use cases we've had in mind it should be an ease for you to get running. If you need something that just doesn't quite fit this solution, or if you just you need more control, consider one of the following libraries:
- [react-intersection-observer](https://github.com/thebuilder/react-intersection-observer)
- [react-scrollspy](https://github.com/makotot/react-scrollspy)
- [scrollmonitor-react](https://github.com/stutrek/scrollmonitor-react)

## Usage

### Reveal animation when scrolled into view
```js
<InViewMonitor
  classNameInitial='vis-hidden'
  classNameOnScrollIntoView='animated fadeInUp'
>
  <ElementToAnimateIn />
</InViewMonitor>
```
Note: these classes are not included. We are big fans of [animate.css](https://github.com/daneden/animate.css) for simple "just add water" animations.

### Send custom prop to children when scrolled into view
Can be used for example to auto play a video
```js
<InViewMonitor
  childPropsOnScrollIntoView={{isPlaying: true}}
>
  <VideoPlayer />
</InViewMonitor>
```

[See these and more working examples on demo page](https://snipsco.github.io/react-inview-monitor/).


## Component properties

| Property | Type | Description
:---|:---|:---
| `classNameInitial` | string | className for initial render, typically used to visually hide if element will be animated in. |
| `classNameOnScrollIntoView` | string | className added when scrolled into view, typically animation related classes. |
| `classNameScrolledPastView` | string | className added/removed when scrolled out of view and back in again, typically used for fixing navigation etc on scroll. |
| `childPropsOnScrollIntoView` | object | props propagated to the child element. Can be used to start video, start complex animations, etc. |
| `intoViewRatioShownThreshold` | number | Proportion of element that needs to be inside viewport before it's considered in view. `Default: 0.15`  |
| `useInviewMonitor` | func | Convenient function that can be used to dynamically disable the monitor, for example for mobile devices. |
| `mountInitDelayTime` | number | Can be used if loading in large images etc that changes viewport coordinates on page |


## Performance Note

Each instance of InViewMonitor sets up a (throttled) scroll listener
on the window. This means a large number of concurrent InViewMonitor instances
will likely cause performance issues. If you are looking to do something likely
fading in every item on scroll in a long list, you will be better of setting up
your own single scroll listener and do the calculations for all items there.
