# CachedImageView Widget
## Overview
The *CachedImageView* widget implements the [best practice of caching remote images](http://docs.appcelerator.com/titanium/latest/#!/guide/Image_Best_Practices-section-30082525_ImageBestPractices-Cachingremoteimages) for [Titanium](http://www.appcelerator.com/platform) [Alloy](http://projects.appcelerator.com/alloy/docs/Alloy-bootstrap/index.html) by [Appcelerator](http://www.appcelerator.com).

## Features
* Initialize the widget directly through the requiring view.
* Provide a seperate URL for the image to use on IOS retina devices.
* Provide a local filename to be used instead of the MD5 hash of the URL.
* Provide an extension for the local file if the remote doesn't have one.

## Future work
* Provide a subdirectory to save the image under.
* Provide a choice to which system directory (cache, data) to save under.
* Provide a maximum age for the cached image before re-downloading it.

## Quick Start
* [Download the latest version](https://github.com/FokkeZB/nl.fokkezb.cachedImageView/tags) of the widget as a ZIP file.
* Move the file to your project's root folder.
* Unzip the file and you'll find the widget under `app/widgets/nl.fokkezb.cachedImageView`.
* Add the widget as a dependency to your `app/config.json` file like so:

```javascript
	…
	"dependencies": {
		"nl.fokkezb.cachedImageView":"1.2"
	}
```

* Use the widget in a view just like you'd use an `ImageView`. Only use `Widget` instead of `ImageView` and add the `src` attribute to point to the widget.

```xml
<Widget src="nl.fokkezb.cachedImageView"
id="civ" image="http://url.to/image.png" />
```

* Optionally add any of the additional parameters as attributes.

## Additonal parameters
The only required parameter is the `image` parameter. All parameters are passed on to the resulting *Ti.UI.ImageView*. You can add the following additional parameters to change the widget's behaviour. They can be used both as attributes in `<Widget>` and when initializing the widget in your controller.

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| cacheHires | *string* | URL of the image to use for iOS retina devices. |
| cacheName | *string*  | Basename for the local file instead of the MD5 hash of the URL. Use it when the URL contains some time-dependant key. |
| cacheExt | *string* | Extension for the local file if the URL doesn't have one, like with generated images. |

## Methods

| Method | Params | Description |
| ------ | ------ | ----------- |
| init   | *object* | Any ImageView parameters plus the additional above |
| applyProperties | *object* | Alias for `init` |
| setImage | *string* | Alias for calling `init` with only an `image` parameter |
| getImage | *bool* returnPath | Return the (path to the) local image. Calling this method before it has been cached will return `undefined` |

## Initialization in the Controller
If you don't include the `image` parameter as an attribute in `<Widget/>`, the resulting *Ti.UI.ImageView* will not be automatically initialized for you. This allows you to do this yourself in your controller. This can be usefull if you want to add some advanced decission logic to determine which image to use. If this would only depend on the *formFactor* and *platform* however, I would recommend using [conditional code](http://docs.appcelerator.com/titanium/3.0/#!/guide/Alloy_Views-section-34636249_AlloyViews-ConditionalCode) in `<Widget/>` instead.

**NOTE:** The `$.cid` in the example below corresponds to the `id` attribute in the `<Widget/>` example. You can change it to whatever value. From 1.2 on you can also call the more common `applyProperties`.

```javascript
$.cid.init({
    image: OS_IOS ? 'http://url.to/image.png' : 'http://url.to/android-image.png'
});
```

## Styling the ImageView
You can style the resulting *Ti.UI.ImageView* by applying the styles to the `<Widget/>` instead. Add the style declaration to the TTS file that belongs to the view where you've added the `<Widget/>`. The styling will be passed on to the resuling *Ti.UI.ImageView*. Be aware that any attributes you add directly to `<Widget/>` will override the TTS style.

**NOTE:** The `$.cid` in the example below corresponds to the `id` attribute in the `<Widget/>` example.

```javascript
"#cid": {
	width: 57,
	height: 57,
	preventDefaultImage: true
}
```

## Changelog
* 1.2: Added `getImage`, `setImage`, `applyProperties` and deleted `__parentSybmol`
* 1.1: Support for styling via TSS before setting image via init() 
* 1.0.1: Fixed for Alloy 1.0GA
* 1.0: Initial version
