++++++++++++++++++++++++
PHPUnit base test case
++++++++++++++++++++++++
:Author: Michael Klapper <development@morphodo.com>
:Description: PHPUnit base test case class which provides use full default helper you'll need for advanced testing applications.
:Homepage: http://www.morphodo.com

Installing via Composer
========================
The recommended way to install PHPUnit base test case is through [Composer](http://getcomposer.org).

1. Add ``morphodo/phpunit-base-test-case`` as a dependency in your project's ``composer.json`` file:

::

  {
		"require-dev": {
			"morphodo/phpunit-base-test-case": "*"
		}
	}

Consider tightening your dependencies to a known version when deploying mission critical applications (e.g. ``1.0.*``).
2. Download and install Composer:

::

  curl -s http://getcomposer.org/installer | php

3. Install your dependencies:

::

	php composer.phar install --dev

4. Require Composer's autoloader

Composer also prepares an autoload file that's capable of autoloading all of the classes in any of the libraries that it downloads. To use it, just add the following line to your code's bootstrap process:

::

	require 'vendor/autoload.php';

You can find out more on how to install Composer, configure autoloading, and other best-practices for defining dependencies at http://getcomposer.org.
