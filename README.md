# S3 CRUD documentation

>**S3**: Amazon S3 (Simple Storage Service) is a web service offered by Amazon Web Services that provides storage through web services interfaces (REST, SOAP etc)

**bucket:**In S3, bucket is like a directory inside which all the files are stored

**key:**Every stored file in S3 has a Key which is the path that is used to store and retreive these files.

## Uploading a file to S3

```php

RandomHelper::mediaPreviewFromS3( array('key'=>'', 'bucket'=>'', 'icon'=>'', 'img'=>'', 'text'=>'', 'jsfunction', 'link'=>'') );


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

