# Prevent Direct Access to PHP
## _We will look at how to prevent PHP file from direct URL access._

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)



Here are the steps to prevent direct access to PHP file. Let us say you have a PHP file /form.php at /var/www/html/form.php and it is executed during a form submission on your website http://example.com. Let us say that you don’t want people to access your PHP file directly at http://example.com/form.php. In such cases, follow the steps below.

## Prevent Direct Access to PHP file
Add the following lines to the top of your PHP file.



```php
<?php
    if ( $_SERVER['REQUEST_METHOD']=='GET' && realpath(__FILE__) == realpath( $_SERVER['SCRIPT_FILENAME'] ) )
    {        
        header( 'HTTP/1.0 403 Forbidden', TRUE, 403 );
        die( header( 'location: /index.php' ) );
    }
?>
```

Let us look at the above code line by line.
In the first line, we have an if condition where we check if the request method is GET and if the absolute path of the file is same as the full path of the requested file.
In such cases, the server will call header function to return 403 access forbidden response code. You may also use 404 page not found code instead to avoid giving any hints to malicious users about the authenticity of requested URL.
Lastly, we use the die function to exit the page and redirect to index.php page that is home page. You may also redirect to another page as per your requirement.
If the above code does not work for you, you may add the following code to the top of your file form.php instead....
```sh
if(!isset($_SERVER['HTTP_REFERER'])){
    // redirect them to your desired location
    header('location: /index.php');
    exit;
}
```
## License
MIT
