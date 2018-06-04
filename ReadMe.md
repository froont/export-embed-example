# Froont export embed example

This is example of exported code from Froont app, to be used as embed in another page.


## What is it for?

It allows a user to place HTML/CSS/JS content created in Froont directly in to their webpage through CMS, while keeping your own header/footer and other page peaces that don't need to be changed. This is perfect campaign banners and publications.


## Try it
To try it out copy the HTML from this file: [embed-with-linked-assets.html](./embed-with-linked-assets.html) and paste in your CMS HTML editing mode.


## Base Style and Script

The froont-export-main.js and froont-export-main.css are Froont global CSS and JavaScript files. They are provided here for user to be able to store them in their own CDN (the paths to files should be updated in HTML).
The froont-export-main.js and froont-export-main.css can also be provided embedded in the HTML.


## Font Loader
By default Froont adds [JavaScript code](./embed.html#L542) for loading Google or TypeKit fonts. If this code is not required the code can be excluded. This is useful for when you only use your own fonts hosted on your server (see: [example-without-font-loader.html](./example-without-font-loader.html)).


## Amazon S3 export

For better integration with your back-end system Froont provides export to Amazon S3 bundle directly.

### Required configuration

* `aws_s3_bucket_name` - name of bucket for export
* `aws_user_key` - (key for a user that has read/write access to this bucket)
* `aws_user_secret` - (secret for a user that has read/write access to this bucket)

### Export process

Export happens on user action - "Export to S3":

1. Froont generates export code:
    * All assets are linked from their current location
    * Images are hosted on Froont server or your S3
    * Froont CSS and JS libraries hosted on Froont server or your S3
2. Froont pushes index.html with to S3 ([your s3 bucker]/[project]/export/index.html)

### Usage

Host the returned HTML and link the base assets provided by Froont.

1. Host or link to Froont base assets
    * Exported HTML file doesn't include base assets which are the same for all projects (`froont-export-main.js` and `froont-export-main.css`)
    * Those can be acquired from Froont and hosted on your own server for better performance
    * Or link the assets from Froont directly
2. Embed the code returned from Froont in any of your pages
    - Through CMS (HTML input)
    - Load directly from hard drive (like [embed.html](./embed.html) example) or database


## Amazon S3 static asset upload

For security and better performance Froont allows to upload your static assets directly to your own Amazon S3 bucket. This replaces the static upload to Froont server, so your assets would be only stored in your S3 bucket.

### Required configuration

* `aws_s3_bucket_name` - name of bucket for export
* `aws_user_key` - (key for a user that has read/write access to this bucket)
* `aws_user_secret` - (secret for a user that has read/write access to this bucket)

### Upload process

Upload happens on user action - "Image upload in Froont editor":

- File is checked by our server, if it is actually an image
- If check is passed it is pushed to configured S3 bucket ([your s3 bucker]/[project]/static/image.png)
