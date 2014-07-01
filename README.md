#Automated Cross-browser Testing with Sauce Labs

Starter-kit and code examples for an automated cross-browser testing workflow for Drupal using Behat tests supported by Github and Jenkins or Travis CI for continuous integration. 

[Fork the Sauxy repo](https://github.com/greylabel/sauxy/fork) and clone locally to begin working with these code examples.

## Sauce Labs

Sauce Labs is a SaaS platform that provides Selenium testing, JavaScript Unit testing, manual testing, and mobile application testing.

Sauce Labs make cross-browser testing easier and faster for developers by providing access to numerous virtual machines at a very low cost. They support a wide-range of browsers and mobile devices, and provide integration services allowing for robust automated cross-browser testing workflows.

### Setup

Sign up for a [Sauce Labs account](https://saucelabs.com/signup) to get a Sauce Labs USERNAME and ACCESS KEY, which can be found on your [account page](https://saucelabs.com/account).


## Drupal and Behat

[Behat](http://behat.org/) is a behavior-driven development (BDD) framework for PHP applications. The [Behat Drupal Extension](https://www.drupal.org/project/drupalextension) provides Drupal integration and features.

### Set-up
#### Install required components

##### Drush
A command line shell and scripting interface for Drupal.
###### Install (OSX and Homebrew)
`brew install drush`

##### Apache Ant
Apache Ant is a software tool for automating software build processes.

###### Install (OSX and Homebrew)
`brew install ant`

##### Composer
Composer is a dependency management system for PHP applications that is used to manage all the third party dependencies, in this case, the numerous Behat extensions used by the project.

###### Install (OSX and Homebrew)
`brew install composer`

##### Selenium Server
A testing tool that interfaces with a web browser (webdriver) to automate testing when Javascript and other browser specifics are needed.

###### Install (OSX and Homebrew)
`brew install selenium-server-standalone`

###### Start Selenium (OSX and Homebrew)
`selenium-server -p 4444`

###### Install (linux)
Go to http://docs.seleniumhq.org/download/ and find the Selenium Server download towards the middle.

You will be downloading a `.jar` (Java) file.

To start the server, you will run:

`java -jar [the-name-of-the-jar-file]` or _click on the file_

example:
`java -jar ~/Selenium/selenium-server-standalone-2.39.0.jar`

##### PhantomJS
PhantomJS is a headless WebKit scriptable with a JavaScript API. It has fast and native support for various web standards: DOM handling, CSS selector, JSON, Canvas, and SVG.

###### Install (OSX and Homebrew)
`brew install phantomjs`

###### Start PhantomJS (OSX and Homebrew)
`phantomjs --webdriver=8643`

###### Install (linux)
Go to http://phantomjs.org/download.html and find the PhantomJS download towards the middle. Follow the instructions for your OS.

##### Chromedriver for Selenium (Optional to use Chrome instead of Firefox)
A web driver replacement that uses Chrome instead of Firefox

###### Install (OSX and Homebrew)
`brew install chromedriver`


### Setting up Drupal

#### _Make_ Drupal
`cd /{path-to-project-root}`

`drush make sauxy.make docroot && cd docroot`

#### Install Drupal
_Replace PLACEHOLDERS below with desired configuration_

`cd docroot`

`drush si minimal --sites-subdir=default --db-url=mysql://USERNAME:PASSWORD@localhost/DBNAME --account-name=ADMIN --account-pass=PASSWORD --site-mail=ADMIN@EXAMPLE.COM --site-name="SAUXY" --yes`


### Setting up Behat

Using a terminal, go to: `/{path-to-project-root}/tests/behat`

Run Composer to download and install all the Behat extension and dependencies defined in the `composer.json` file.

`composer install`

Make a copy of `behat.local.yml.example` for your own settings and name it`behat.local.yml`.

Open this new `behat.local.yml` config file and fill in your local site information according to the comments. This file tells Behat how to connect to your local site.

Test if Behat is working
`bin/behat -dl`

Run this included sample feature. 
`bin/behat features/drupal.feature`

This test should pass on a fresh Drupal site. If not, you can still confirm Behat is working if you get a failed test. 

This test should also confirm that Selenium is working correctly.

### Testing locally with Sauce Labs using Sauce Connect

Using a terminal, go to: `/{path-to-project-root}/tests/behat`

`bin/sauce_config YOUR-SAUCE-USERNAME YOUR-SAUCE-API-KEY`

Sauce connect: secure tunnel between project infrastructure and Sauce Labs infrastructure.

`bin/sauce_connect`

Run this included sample feature. 
`bin/behat features/drupal.feature`
