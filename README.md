# gravatar
---

- [Installation](#installation)
- [Registering the Package](#registering-the-package)
- [Usage](#usage)
- [Generating gravatar url by user() method](#generating-gravatar-url-by-user-method)
- [Generating gravatar url by make() method](#generating-gravatar-url-by-make-method)
- [Generating HTM avatar code](#generating-htm-avatar-code)

## Installation

Add Gravatar to your composer.json file:

```
composer require artlabs/gravatar
```

Use [composer](http://getcomposer.org) to install this package.

```
$ composer update
```

### Registering the Package

Add the Gravatar Service Provider to your config in ``config/app.php``:

```php
'providers' => array(
	Artlabs\Gravatar\GravatarServiceProvider::class
),
```

### Usage


#### Generating gravatar url by user() method

Generating avatar with default settings is very simple and all you have to do is to call
``user()`` method with user email as a paramterer:

```php
<?php
	// user email
	$email = "example@user.email";

	// create a gravatar object for specified email
 	$gravatar = Gravatar::user( $email );

	 // get gravatar url as a string
	$url = $gravatar->url();

?>
```

If you want to customize avatar a little bit you can set some more parameters using additional methods
like ``size()``, ``rating()``, ``defaultImage()``.

```php
<?php
	// user email
	$email = "example@user.email";

	// create a gravatar object for specified email with additional settings
 	$gravatar = Gravatar::user( $email );

 	// Size in pixels, defaults to 80px [ 1 - 2048 ]
	$gravatar->size('220');

	// Maximum rating (inclusive) [ g | pg | r | x ]
	// defaults to 'g'
	$gravatar->rating('g');

	// Default imageset to use [ 404 | mm | identicon | monsterid | wavatar ]
	// You can also specify url to your own default avatar image
	// defaults to 'mm'
	$gravatar->defaultImage('mm');

    // set Gravatar to build urls with https [true = use https, false = ise http]
    // defaults to 'false'
    $gravatar->secured( true );

	// get gravatar url as a string
	$url = $gravatar->url();

?>
```

U can also chain all methods:

```php
<?php
 	$url = Gravatar::user( $email )->size('220')->rating('g')->defaultImage('mm')->url();
?>
```


#### Generating gravatar url by make() method

Basic way to generate gravatar url is just to call ``make()`` method with
user email address as a parameter (all other parameters will be loaded from defaults).

```php
<?php
	// user email
	$email = "example@user.email";

	// create a gravatar object for specified email
 	$gravatar = Gravatar::make( $email );

	 // get gravatar url as a string
	$url = $gravatar->url();

?>
```

U can aslo chain methods:

```php
<?php
	// to get url string
	$url = Gravatar::make( $email )->url();
?>
```

If you want specify size of avatar or some other additional parameters you can do this
by passing array with parameters to ``make()`` method:

```php
<?php
	// user email
	$email = "example@user.email";

	// create a gravatar object in specified size
 	$url = Gravatar::make( ['email' => $email, 'size' => 220] )->url();

	// create a gravatar object with some other additional parameters
 	$url = Gravatar::make( [
 		'email' => $email,
 		'size' => 220,
 		'defaultImage' => 'mm',
 		'rating' => 'g',
 	    'secured' => true
 	])->url();
?>
```


#### Generating HTM avatar code

With Gravatar you can get url string of user avatar by calling ``url()`` method
but also you can generate full html <img> code by calling ``html()`` method instead of ``url()``.

```php
<?php
	// user email
	$email = "example@user.email";

	// create some Gravatar object
 	$gravatar = Gravatar::user( $email )->size('120');

	 // get gravatar <img> html code
	$html = $gravatar->html();
?>
```

If you want to have more controll over
the returned html code you can pass some additional html attributes to html() method, for examle:

```php
<?php
	$html = Gravatar::user( $email )->html( ['class' => 'avatar', 'id' => 'user123' ] );
?>
```
