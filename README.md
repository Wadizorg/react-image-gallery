React Image Gallery
===

[![npm version](https://badge.fury.io/js/react-image-gallery.svg)](https://badge.fury.io/js/react-image-gallery)
[![Download Count](http://img.shields.io/npm/dm/react-image-gallery.svg?style=flat)](http://www.npmjs.com/package/react-image-gallery)

![demo gif](https://github.com/xiaolin/react-image-gallery/raw/master/static/image_gallery.gif)

React image gallery is a React component for building image galleries and carousels

Features of `react-image-gallery`
* Mobile friendly
* Thumbnail navigation
* Fullscreen support
* Custom rendered slides
* Responsive design

## Live Demo (try it on mobile)
Live demo: [`linxtion.com/demo/react-image-gallery`](http://linxtion.com/demo/react-image-gallery)

## Getting started

```
npm install react-image-gallery
```

### Style import

```
# SCSS
@import "../node_modules/react-image-gallery/styles/scss/image-gallery.scss";

# CSS
@import "../node_modules/react-image-gallery/styles/css/image-gallery.css";

# Webpack
import "react-image-gallery/styles/css/image-gallery";

```


### Example
Need more example? See [`example/app.js`](https://github.com/xiaolin/react-image-gallery/blob/master/example/app.js)
```js
import ImageGallery from 'react-image-gallery';

class MyComponent extends React.Component {

  handleImageLoad(event) {
    console.log('Image loaded ', event.target)
  }

  render() {

    const images = [
      {
        original: 'http://lorempixel.com/1000/600/nature/1/',
        thumbnail: 'http://lorempixel.com/250/150/nature/1/',
        originalClass: 'featured-slide',
        thumbnailClass: 'featured-thumb',
        originalAlt: 'original-alt',
        thumbnailAlt: 'thumbnail-alt',
        thumbnailLabel: 'Optional',
        description: 'Optional description...',
        srcSet: 'Optional srcset (responsive images src)',
        sizes: 'Optional sizes (image sizes relative to the breakpoint)'
      },
      {
        original: 'http://lorempixel.com/1000/600/nature/2/',
        thumbnail: 'http://lorempixel.com/250/150/nature/2/'
      },
      {
        original: 'http://lorempixel.com/1000/600/nature/3/',
        thumbnail: 'http://lorempixel.com/250/150/nature/3/'
      }
    ]

    return (
      <ImageGallery
        ref={i => this._imageGallery = i}
        items={images}
        slideInterval={2000}
        onImageLoad={this.handleImageLoad}/>
    );
  }

}
```

# Props

* `items`: (required) Array of objects, see example above,
* `infinite`: Boolean, default `true`
  * infinite sliding
* `lazyLoad`: Boolean, default `false`
* `showNav`: Boolean, default `true`
* `showThumbnails`: Boolean, default `true`
* `showFullscreenButton`: Boolean, default `true`
* `showPlayButton`: Boolean, default `true`
* `showBullets`: Boolean, default `false`
* `showIndex`: Boolean, default `false`
* `autoPlay`: Boolean, default `false`
* `disableThumbnailScroll`: Boolean, default `false`
  * disables the thumbnail container from adjusting
* `slideOnThumbnailHover`: Boolean, default `false`
  * slides to the currently hovered thumbnail
* `disableArrowKeys`: Boolean, default `false`
* `disableSwipe`: Boolean, default `false`
* `defaultImage`: String, default `undefined`
  * an image src pointing to your default image if an image fails to load
  * handles both slide image, and thumbnail image
* `onImageError`: Function, `callback(event)`
  * overrides defaultImage
* `onThumbnailError`: Function, `callback(event)`
  * overrides defaultImage
* `indexSeparator`: String, default `' / '`, ignored if `showIndex` is false
* `slideInterval`: Integer, default `3000`
* `startIndex`: Integer, default `0`
* `onImageLoad`: Function, `callback(event)`
* `onSlide`: Function, `callback(currentIndex)`
* `onScreenChange`: Function, `callback(fullscreenElement)`
* `onPause`: Function, `callback(currentIndex)`
* `onPlay`: Function, `callback(currentIndex)`
* `onClick`: Function, `callback(event)`
* `renderCustomControls`: Function, custom controls rendering
  * Use this to render custom controls or other elements on the currently displayed image (like the fullscreen button)
  ```javascript
    _renderCustomControls() {
      return <a href='' className='image-gallery-custom-action' onClick={this._customAction.bind(this)}/>
    }
  ```
* `renderItem`: Function, custom item rendering
  * As a prop on a specific item `[{thumbnail: '...', renderItem: '...'}]`
  * As a prop passed into `ImageGallery` to completely override `_renderItem`, see original below
    ```javascript
      _renderItem(item) {
        const onImageError = this.props.onImageError || this._handleImageError

        return (
          <div className='image-gallery-image'>
            <img
                src={item.original}
                alt={item.originalAlt}
                srcSet={item.srcSet}
                sizes={item.sizes}
                onLoad={this.props.onImageLoad}
                onError={onImageError.bind(this)}
            />
            {
              item.description &&
                <span className='image-gallery-description'>
                  {item.description}
                </span>
            }
          </div>
        )
      }
    ```


# Functions

* `play()`: continuous plays if image is not hovered
* `pause()`: pauses the slides
* `fullScreen()`: activates full screen
* `exitFullScreen()`: deactivates full screen
* `slideToIndex(index)`: slides to a specific index
* `getCurrentIndex()`: returns the current index

# Notes

* Feel free to contribute and or provide feedback!

# Build the example locally

```
git clone https://github.com/xiaolin/react-image-gallery.git
npm install
npm start
```

Then open [`localhost:8001`](http://localhost:8001) in a browser.


# License

MIT
