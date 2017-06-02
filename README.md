# S3 CRUD documentation

##Terms:

>**S3**: Amazon S3 (Simple Storage Service) is a web service offered by Amazon Web Services that provides storage through web services interfaces (REST, SOAP etc)

**bucket:** In S3, bucket is like a directory inside which all the files are stored

**key:** Every stored file in S3 has a Key which is the path that is used to store and retreive these files.

**presigned url:** It is a URL created by S3 that points to a file for a short period of time.

## Uploading a file to S3:

```php

RandomHelper::mediaPreviewFromS3( array('key'=>'', 'bucket'=>'', 'icon'=>'', 'img'=>'', 'text'=>'', 'jsfunction', 'link'=>'', 'return'=>'') );


```
In the above function `'key'` is manidatory parameter.


```php

RandomHelper::mediaPreviewFromS3($key)


```

* `bucket`
> Used in creating a pre-signed URL

default: `Yii::app()->params['s3_credentials']['bucket']`

* `jsfunction`
> Called when clicked on the preview link/icon/img

default: `previewAttachmentS3(this)`

* `icon`
> Used to display an icon as a preview button

example:

```php

RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'icon'=>'<i class="fa fa-eye"></i>') )

```

* `img`
> Used to display an image as a preview button

where as it is an array: `array('src'=>$src_of_img, 'title'=>'preview');` if you are passing img to preview function, passing both the parameters is mandatory.

example:

```php

RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'img'=>array('src'=>'http:://bit.ly/sa.jpg', 'title'=>'preview')) )

```

* `text`
> Used to disaplay a preview link with text inside it

default: 'Preview'

example:

```php

RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'text'=>'click to preview') )


```

** If neither of img, icon, text is passed, It displays a link with text 'Preview' **

* `jsfunction`
> This function is called when clicked on preview button

default: 'previewAttachmentS3(this)'

```php

RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'jsfunction'=>'customPreviewFunction(this)') )

``` 

* `link`
> target of ajax request that is used to create a PreSignedURL

example:
```php

RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'link'=>'pms/generatePreviewURL') )

```

when preview button is clicked, a ajax request is sent to link, receives a presignedurl to display it using google viewer.

* `return`
Type: 	 boolean
Default: False

example:

```php

$preview_button = RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'return'=>True) )

//use $preview_button

```
