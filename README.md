# seigler/simple-php-buffer

PHP file for basic file-based output buffering

## Usage
```php
define('CACHE_PATH', sys_get_temp_dir().'/cache_'); // optional, cache-file location prefix
define('CACHE_TIME', 5 * 60); // optional, seconds to cache the output
require 'buffer.php';
```

This will send `last-modified`, `expires`, and `etag` headers. If a request includes `etag` and
`modified-since` headers the script can intelligently return a 304 not modified.

This uses output buffering, but it can't buffer headers. If you need to send out a header every time, cached or not, put that header code above the `require`.

```php
Header('Content-type: image/svg+xml; charset=utf-8');
Header('Content-Disposition: inline; filename="fancy-chart-' . date('Y-m-d\THisT') . '.svg"');
require 'buffer.php';

// remaining code to generate the chart
```

## Credits

* Based on http://www.the-art-of-web.com/php/buffer/

