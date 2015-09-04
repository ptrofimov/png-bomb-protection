# PNG Bomb Protection

* if you found super large (400 GB) file in your tmp directory (/tmp) with the name like "magick-*"
* or if see lack of the memory on the server for uploaded images
* or if see lack of disk space on the server for uploaded images
* or if there are some unexplained problems with uploading of images

It seems that someone uploaded to your server PNG bomb (a unicolor picture in PNG format with a very big width and height).

**The solution:** check image width and height before image processing.

For this you could use image magick tool. Here is an example for PHP:

```php
exec('identify -format "%w %h" ' . escapeshellarg($uploadedImageFileName), $output, $error);
if (!$error) {
    list($width, $height) = explode(' ', $output[0]);
    if ($width > 10000 || $height > 10000) {
        // invalid image
    }
}
```

More information you could find here:

* [Decompression bomb vulnerabilities](http://www.aerasec.de/security/advisories/decompression-bomb-vulnerability.html)
* [Decompression bomb protection](https://github.com/python-pillow/Pillow/issues/515)
* [files in /tmp](http://www.imagemagick.org/discourse-server/viewtopic.php?t=18130)
* [Файл 420 байт разжимается в картинку png на 40 гигапикселей](http://webcache.googleusercontent.com/search?q=cache:bJziLnmJRmsJ:https://xakep.ru/2015/09/03/png-bomb/+&cd=1&hl=en&ct=clnk&gl=by)
