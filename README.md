# S3 CRUD documentation

## Terms:

>**S3**: Amazon S3 (Simple Storage Service) is a web service offered by Amazon Web Services that provides storage through web services interfaces (REST, SOAP etc)

**bucket:** In S3, bucket is like a directory inside which all the files are stored

**key:** Every stored file in S3 has a Key which is the path that is used to store and retreive these files.

**presigned url:** It is a URL created by S3 that points to a file for a short period of time.

## PushTos3:

To upload a file to S3

It returns an array: array('ObjectURL'=>'', 'Key'=>'', 'Bucket'=>'')

```php

RandomHelper::pushToS3( array('key'=>'', 'deleteAfterUpload'=>'', 'ACL'=>'', 'tenant_id'=>'', 'folder_name'=>'', 'file_name'=>'', 'source_file_path'=>'') );

```

* `source_file_path`:
> Path of file to be uploaded


* `key`:
> The s3 key og file

example:
```php

$s3_links = RandomHelper::pushToS3( array('source_file_path'=>'/data/live/upload/123.doc', 'key'=>'2/docs/2124_doc.doc') );
//store $s3_links in a databases

```

* `tenant_id`, `folder_name`, `file_name`:
> Instead of passing a key, you can pass the above parameters and It creates key

Example:
```php

$s3_links = RandomHelper::pushToS3( array('source_file_path'=>'/data/live/upload/123.doc', 'tenant_id'=>Yii::app()->user->getTenantId(), 'folder_name'=>'resumes', 'filename'=>'new_resume.doc') );
//store $s3_links in a databases


```

* `deleteAfterUpload`:
> By default after uploading the file to s3 it deletes it from local

example:
```php

$s3_links = RandomHelper::pushToS3('source_file_path'=>'data/live/uplaod/2/sadasd.doc', 'key'=>'new/s3/key/filename.extension', 'deleteAfterUpload'=>False);

```

* `ACL`:
> A S3 file can be public or private, by default all files are private, to make it public use `'ACL'=>'public-read'`

Example:
```php

$s3_links = RandomHelper::pushToS3( array('source_file_path'=>'local/file/path', 'tenant_id'=>Yii::app()->user->getTenantId(), 'folder_name'=>'s3/folder/name'. 'file_name'=>'filename.extension', 'ACL'=>'public-read') );

```

##  Perview S3:

To Display Preview button

```php

RandomHelper::mediaPreviewFromS3( array('key'=>'', 'bucket'=>'', 'icon'=>'', 'img'=>'', 'text'=>'', 'jsfunction', 'link'=>'', 'return'=>'') );


```
In the above function `'key'` is mandatory parameter.


```php

RandomHelper::mediaPreviewFromS3( array('key'=>$key) )


```

* `bucket`
> Used in creating a pre-signed URL

default: `Yii::app()->params['s3_credentials']['bucket']`

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
> If passed as True, returns the result instead of echoing it.

Type: 	 boolean
Default: False

example:

```php

$preview_button = RandomHelper::mediaPreviewFromS3( array('key'=>$key, 'return'=>True) )

//use $preview_button

```

## Download From S3:

To Display Download Button

```php

RandomHelper::DownloadFromS3( array('key'=>'', 'bucket'=>'', 'icon'=>'', 'img'=>'', 'text'=>'', 'link'=>'', return=>'') );

```

All the parameters are same as the preview function with key being the mandatory parameter.
However, It do not use jsfunction.

## Delete From S3:

To delete a file from S3

Example:

```php

$result = RandomHelper::pushToS3($key);
// result is a boolean, if uploaded return true, else false

```
