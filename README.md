# swappy-image-view
An image change/sort view for editing profile, image slider, product slider etc.

<img src="https://github.com/abalta/swappy-image-view/blob/master/assets/swappy.gif" width="360" height="640">

## Download

### Step 1. Add the JitPack repository to your build file

```
allprojects {
    repositories {
	    ...
	    maven { url 'https://jitpack.io' }
	}
}

```

### Step 2. Add the dependency

```
dependencies {
	        implementation 'com.github.abalta:swappy-image-view:1.0.0'
	}

```

## Usage

### Add swappy image view to your layout xml

```xml
    <com.abdullahbalta.swappy.SwappyImageView
            android:id="@+id/swappy_view"
            android:layout_width="match_parent"
            android:layout_height="240dp"/>
```

### Add image from gallery/camera

Implement **OnSwappyListener** to your activity/fragment

```kotlin
    override fun onAddingImage(imageView: ImageView) {
        //Trigger gallery/camera intent code
    }

    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
	    ...
            swappy.addImage('drawable' or 'bitmap')
        }
    }
```

### Add image from url

Implement **OnSwappyListener** to your activity/fragment, to handle placeholder you need to call **setImageAddedFailed()** or **setImageAddedSuccess()**

```kotlin
    override fun onAddingImage(imageView: ImageView) {
    	//Use any image loading library
        Glide.with(this).load(edtUrl.text.toString()).listener(object: RequestListener<Drawable> {
            override fun onLoadFailed(e: GlideException?, model: Any?, target: Target<Drawable>?, isFirstResource: Boolean): Boolean {
                swappy.setImageAddedFailed()
                return false
            }

            override fun onResourceReady(resource: Drawable?, model: Any?, target: Target<Drawable>?, dataSource: DataSource?, isFirstResource: Boolean): Boolean {
                swappy.setImageAddedSuccess()
                return false
            }

        }).into(imageView)
    }
```

## Features

```kotlin
       /**
         * app:add_icon -> customize add icon (vector supported)
         * app:remove_icon -> customize remove icon (vector supported)
         * app:placeholder -> customize empty imageview background (solid color supported)
         * app:item_padding -> padding imageviews
         * app:main_image -> pre-defined main image (vector supported)
         * app:first_image -> pre-defined first image (vector supported)
         * app:second_image -> pre-defined second image (vector supported)
         * app:third_image -> pre-defined third image (vector supported)
         */
```

### Thanks to

Sample app uses following libraries demonstrates demo app, you may use different way to show swappy image view

* [alhazmy13 - MediaPicker](https://github.com/alhazmy13/MediaPicker)
* [bumptech - glide](https://github.com/bumptech/glide)

## License

    Copyright 2018 Abdullah Balta

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
