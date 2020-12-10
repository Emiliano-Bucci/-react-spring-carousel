# react-spring-carousel-js

> A performant React carousel component powered by `react-spring` and `react-use-gesture`.

[![NPM](https://img.shields.io/npm/v/react-spring-carousel-js.svg)](https://www.npmjs.com/package/react-spring-carousel-js) [![NPM](https://img.shields.io/bundlephobia/minzip/react-spring-carousel-js)](https://img.shields.io/bundlephobia/minzip/react-spring-carousel-js)

## Features

- **Extreemely performant**: thanks to react-spring, you'll get a very performant results, and smooth and natural transitions with zero config.
- **Stateless :smirk:**: We don't use `state` to update the animation: this means solid and stable animations in every moment.
- **Custom events**: Use our custom events to intercept when things happen and take the experience to the next level!
- **Mobile first**: You can swipe/drag with no config needed thanks to **react-use-gesture**.
- Resizable: the carousel will automatically resize and adapt if the browser viewport change. Very useful when changing to landscape on mobile devices.
- **Fullscreen capable**: we provide you the **API** to enter/exit from fullscreen mode! (thanks to **screenful.js**).
- **Headles UI**: no more headaches trying to style the elements of the carousel. You decide every aspect of the elements of the carousel.
- **Totally composable**: we give you the instruments (**API**) and you decide where to place all the elements of the carousel and how they will behave and interact.
- **Easy to configure**: you can configure some aspects of the carousel in an easy and simple way.

## Install

```bash
npm install --save react-spring-carousel-js
```

or

```bash
yarn add --save react-spring-carousel-js
```

## Usage

At it's most basic, to start you can do:

```tsx
import { useReactSpringCarousel } from 'react-spring-carousel-js'

const { carouselFragment, thumbsFragment } = useReactSpringCarousel({
  items: [
    {
      id: 'item-1',
      renderItem: <ItemComponent />,
      renderThumb: <ThumbComponent />
    },
    {
      id: 'item-2',
      renderItem: <ItemComponent />,
      renderThumb: <ThumbComponent />
    }
  ]
})

return (
  <div>
    {carouselFragment}
    {thumbsFragment}
  </div>
)
```

As you can see, you don't have to call the component in the traditional way but instead the main **hook** return the **carousel fragment** (which is the carousel) and the **thumbs fragment** (which render the list of tumbs). It's up to you to decide **how** and **where** render boths, and they're not tied in any way, so basically you can customize the UI pretty much in any way you want to!

## Props

You can provide this **options** to better customize the behavior and the aspect of the Carousel:

| Prop                       | Type                                                                                                   | Default          | Description                                                                                     |
| -------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------- | ----------------------------------------------------------------------------------------------- |
| items                      | `T[]`                                                                                                  | `[]`             | You can extend the main interface - `ReactSpringCarouselItem` - and add custom props.           |
| withLoop                   | `boolean`                                                                                              | `false`          | Set to `true` if you want to enable the infinite loop behavior.                                 |
| withThumbs                 | `boolean`                                                                                              | `true`           | Set to false if you don't want to render the list of thumbs.                                    |
| springConfig               | `SpringConfig`                                                                                         | `config.default` | Customize the spring animation props.                                                           |
| shouldResizeOnWindowResize | `boolean`                                                                                              | `true`           | Set to false if you want to disable the auto rezise                                             |
| draggingSlideTreshold      | `number`                                                                                               | `50`             | Set the minimum treshold that is required to slide after the item is dragged and then released. |
| enableThumbsWrapperScroll  | `boolean`                                                                                              | `true`           | Set to false if you don't want to auto-scroll the list of thumbs when an item is selected.      |
| CustomWrapper              | `React.ForwardRefExoticComponent<{ children: React.ReactNode } & React.RefAttributes<HTMLDivElement>>` | `undefined`      | You can provide a custom `element` that will be used as the main Wrapper element                |
| CustomThumbsWrapper        | `React.FC<{ children: React.ReactNode }>`                                                              | `undefined`      | You can provide a custom `element` to customize the wrapper of the thumb list.                  |
| carouselSlideAxis          | `x / y`                                                                                                | `x`              | Specify the slide axis direction of the carousel                                                |
| thumbsSlideAxis            | `x / y`                                                                                                | `x`              | Specify the slide axis direction of the thumbs list                                             |
| thumbsMaxHeight            | `number`                                                                                               | `0`              | Set the max height of the thumb list wrapper; to be only used if you set thumbsSlideAxis to `y` |

## Options (API)

The following options and API can be both extracted from the main `hook` or from the own Carousel `Context` (that can be imported and used inside any component rendered inside the Carousel :smirk:)

| Option                 | Type                                                                            | Default Value | Description                                                                                                                                                                                                                                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| isFullscreen           | `boolean`                                                                       | `false`       | Indicates if the carousel entered in fullscreen mode.                                                                                                                                                                                                                                                                                |
| getIsActiveItem        | `(id: string): boolean`                                                         | `false`       | By providing the `id` of an item, you can check if that item the current active one.                                                                                                                                                                                                                                                 |
| getIsPrevItem          | `(id: string): boolean`                                                         | `false`       | By providing the `id` of an item, you can check if that item is the previous one in the list of items. Pretty useful if, for example, you render a list of items and want to preload on demand.                                                                                                                                      |
| getIsNextItem          | `(id: string): boolean`                                                         | `false`       | By providing the `id` of an item, you can check if that item is the next one in the list of items. Pretty useful if, for example, you render a list of items and want to preload on demand.                                                                                                                                          |
| slideToItem            | `(item: number, callback?: VoidFunction): void`                                 | `() => {}`    | You can use this method to programmatically slide to a specific item. You can also pass a callback if you want to perform some action after the animation is completed. **NOTE**: The callback is passed and called by the `onRest()` method of `react-spring`.                                                                      |
| getIsAnimating         | `(): boolean`                                                                   | `() => false` | Use this method to check if the carousel is `animating` or not. Under the hood, `react-carousel-spring-js` uses a ref to keep track of this value. We don't use a state to avoid useless re-render that could impact in the animation smoothness.                                                                                    |
| getIsDragging          | `(): boolean`                                                                   | `() => false` | Use this method to check if the carousel is `dragging` or not. Under the hood, `react-carousel-spring-js` uses a ref to keep track of this value. We don't use a state to avoid useless re-render that could impact in the animation smoothness.                                                                                     |
| enterFullscreen        | `(elementRef?: HTMLElement): void`                                              | `() => {}`    | Use this method to enter in the `fullscreen` mode. **NOTE**: By default, the main wrapper of the carousel will enter in fullscreen mode, but normally you will want to put in the fullscreen mode also other elements, that's why you can pass a custom element ref.                                                                 |
| slideToPrevItem        | `(): void`                                                                      | `() => {}`    | Use this method slide to the `previous` item. This is useful to build your own navigation buttons. You just need to call it and that's it; the carousel itself will handle all the internal logic part (for example, if the `withLoop` property is set to `false`, when reaching the first item, if you call it it will do nothing.) |
| slideToNextItem        | `(): void`                                                                      | `() => {}`    | Use this method slide to the `next` item. This is useful to build your own navigation buttons. You just need to call it and that's it; the carousel itself will handle all the internal logic part (for example, if the `withLoop` property is set to `false`, when reaching the last item, if you call it it will do nothing.)      |
| useListenToCustomEvent | `<T>(eventName: ReactSpringCustomEvents, eventHandler: (data?: T): void): void` | `() => {}`    | Use this hook to perform callback actions in your application when the carousel internal `state` change.                                                                                                                                                                                                                             |

## Events

Most of the React carousel libraries out there handle the animations by updating the state (`this.setState()` or `useState()`). While this is totally fine from the React perspective, it isn't that much from the `animation` perspective, since when React triggers a rerender lots of things happen under the hood and this can cause animations to junky a bit. For this reason we decide to not leverage at all on React state to animate things (pretty much like `react-spring` do, actually), but we stick to the `react-spring` way.

So far so good, but we still needed a way to interact when things happens in our carousel. For simple cases probably we wouldn't need to respond at all, but what if we had to render a carousel full of images that need to be lazy loaded in a particular way, or if we need to do some handy stuff when a particular item becomes the active one? To solve this problem, without sacrificing performance, we use `custom events`.

### How they works?

Every instance of the Carousel will expose a `useListenToCustomEvent` hook. `useListenToCustomEvent` accept two arguments:

- The event name to listen
- A callback that will receive some data (dependind on the event that we listen)

This way, whenever we listen for some particular events, we can update our UI in a simple and effective way, getting the best possible result.

### List of events

| Event                    | Description                                                                                                                             |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| RCSJS:onSlideStartChange | The event is emitted every time a slide is about to slide .                                                                             |
| RCSJS:onSlideChange      | The event is emitted after the animation slide is completed. **NOTE**: The event is emitted inside the `onRest()` react-spring callback |
| RCSJS:onDrag             | The event is emitted when a user drags the carousel items                                                                               |

In order to know which props the callback of the event emitter will receive, you can use the following types:

- RCSJS:onSlideStartChange -> `RCSJSOnSlideStartChange`
- RCSJS:onSlideChange -> `RCSJSOnSlideChange`
- RCSJS:onDrag -> `RCSJSOnDrag`

## License

MIT © [Emiliano-Bucci](https://github.com/Emiliano-Bucci)
