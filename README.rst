++++++++++++++++++++++++
PHPUnit base test case
++++++++++++++++++++++++
:Author: Michael Klapper <development@morphodo.com>
:Description: PHPUnit base test case class which provides use full default helper you'll need for advanced testing applications.
:Homepage: http://www.morphodo.com

How to use
========================

Extend from ``\Morphodo\PHPUnit\TestCase`` to use the additional provided features like fuxture loading, 
easy mock object creation even for abstract classes or private and protected methods and members.

Load data from fixture file
-------------

::

	use Morphodo\PHPUnit\TestCase;
	    
	class MigrateCommandTest extends TestCase {
		public function setUp() {
			$this->setFixtureBasePath(__DIR__);
		}
		
		/**
		 * The ``fixture`` directory should be next the the current test
		 * package besides the current test case file.
		 *
		 * @test
		 */
		public function someTestWithExternalFileFixture() {
			// load the content of "fixture/SettingsReplaceMarker.yaml" into the vfsSteam to create test filesystem files.
			vfsStream::setup('root', NULL, array('deployment.yaml' => $this->getFixtureContent('fixture/SettingsReplaceMarker.yaml')));
		}
	}


Test abstract class
-------------
In the following example we call the protected methods 'loadFile' and pass the arguments to it ``$this->file->_call('loadFile', vfsStream::url('root/index.php'));``.
It is also possible to set/get the value of private/protected member variables ``$this->file->_get('buffer')`` as shown in the example below.

::

	<?php
	
	namespace Morphodo\Tests\Environment\Settings\Handler\File;
	
	use Morphodo\Environment\Settings\Handler\File\AbstractFile;
	use Morphodo\PHPUnit\TestCase;
	use org\bovigo\vfs\vfsStream;
	
	/**
	 * Verify methods provided by abstract class works as they should.
	 *
	 * @author Michael Klapper <development@morphodo.com>
	 * @package Morphodo\Tests\Environment\Settings\Handler\File
	 */
	class AbstractFileTest extends TestCase {
	
		/**
		 * @var AbstractFile
		 */
		protected $file;
	
		public function setUp() {
			$this->file = $this->getAccessibleMockForAbstractClass('\Morphodo\Environment\Settings\Handler\File\AbstractFile');
		}
	
		/**
		 * @test
		 */
		public function verifyFileBufferStateBeforeAndAfterFileReading() {
			vfsStream::setup('root', NULL, array('index.php' => 'the file content with a ###marker### in between.'));
			$this->assertNull($this->file->_get('buffer'));
	
			$this->file->_call('loadFile', vfsStream::url('root/index.php'));
			$this->assertContains('###marker###', $this->file->_get('buffer'));
		}
	}


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



.. _Morphodo: http://www.morphodo.com/de/the-web-company.html
