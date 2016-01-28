SETUP & EXECUTION
=================

Select a location for the framework
===================================
Create a folder, ideally inside your Drupal project root.



Get the framework
=================
In terminal, open the above folder and type:<br><br>
```
composer require cw_test/behat_framework
``` 

    
Install the framework
===================
Run the bootstrap shell script:<br>
```
cd vendor/cw_test/behat_framework && ./bootstrap.sh
```

Inside `vendor/cw_test/behat_framework/Behat/behat.local.yml`, update:<br>
* the `base_url` to your local site url<br>
* the `drupal_root` value to the path to your local drupal installation.
       

Optional Step
=============
This is only required if you want to run tests on Chrome.<br>
(By default, Firefox works out-of-the-box.)

1. Download chromedriver from `http://chromedriver.storage.googleapis.com/index.html?path=2.17/`
2. Save it to `/usr/local/bin`


Verify Setup Successful
=======================
Navigate to:

```
[LOCAL DRUPAL INSTALL FOLDER]/Behat
```

Execute the following:

```
./run-behat.sh setup firefox
```

You should see `1 scenarios (1 passed)` in the terminal window after 15-20 seconds.


Test Execution
==============
Navigate to:

```
[LOCAL DRUPAL INSTALL FOLDER]/Behat
```

To execute the tests, select one of the following options based on the format `./run-behat.sh [tag] [profile]`:

```
./run-behat.sh regression firefox
```

or

```
./run-behat.sh regression chrome
```

Test Results
============
The results of all tests will be stored in `[LOCAL DRUPAL INSTALL FOLDER]/Results/Behat/Twig_***.html`


Test Scripting
==============
There are 3 parts to creating every new test:

 * create/update the XXXX scenario in a .feature file
 * create/update the XXXX Page.php file 
 * create/update the XXXX Context.php file,
 
where XXXX is the name of the page being tested, e.g. Basic, Article, Login, etc.

`It is a good idea to read through the LOGIN feature, page, and context files while reading through the following descriptions.`
 
<u>FEATURE file</u><br>
This file contains the high-level test scenarios written in a Gherkin syntax.<br>
For example, in the `LoginPage.feature`, there are tests to ensure a vaild login is successful.<br>
These files are located in Project_Files/features/.<br>
They all follow the structure ****/****.feature, where **** is the name of the page being tested.<br>

<u>PAGE.php file</u><br>
This file contains the path, page objects, and getters/setters for all the fields on the page XXXX.<br>
For example, in the `LoginPage.php`, there are the username, password, and login button objects detailed.<br>
These files are located in Project_Files/pages/.<br>
They all follow the structure XXXXPage.php, where XXXX is the name of the page being tested.<br>

<u>CONTEXT.php file</u><br>
This file contains all of the functions that are specific to the XXXX page.<br>
For example, in the `LoginContext.php`, there is are functions to fill in the username and password fields, and press the login button.<br>
These files are located in Project_Files/contexts.<br>
They all follow the structure XXXXContext.php, where XXXX is the name of the page being tested.<br>


If you are creating a test for a page that has not previously been automated, then you will need to create all 3 of the files listed above.<br>
If you are creating or updating a test for a page that has previously been automated, then all three of the above files will already exist. In this case, it will require updating these existing files.<br>

The basic process for writing any test would be:

1. Decide what the business scenario is that you would like to test.
2. Write it down in a `.feature` file.
3. Once a new sentence has been created, the objects required for it will need to be added to the `XXXXPage.php` file.
4. Once the objects have been added, the relevant functions will need to be created in the `XXXXContext.php` file.


<u>Points abouts the `FEATURE` file</u><br>
Follow the syntax used in other tests.<br>
Where possible, re-use existing sentences from the `.feature` file as these will already have been automated.<br>
If you are creating a new sentence, keep it short but descriptive.<br>


<u>Points abouts the `PAGE` file</u><br>
Follow the syntax and naming conventions from other PAGE files.<br>
Group obejcts by type, like input fields, buttons, iframes.<br>

<u>Points abouts the `CONTEXT` file</u><br>
Follow the syntax and naming conventions from other CONTEXT files.<br>
Keep all functions as short as possible, ideally doing one thing each, like filling in a text field.<br>



TROUBLESHOOTING
===============
1. If you get API rate limit messages during the `./bootstrap.sh` step, please see:<br>
https://github.com/composer/composer/blob/master/doc/articles/troubleshooting.md#api-rate-limit-and-oauth-tokens

2. If you get the folowing when running the tests, please upgrade your version of java:<br>
`Exception in thread "main" java.lang.UnsupportedClassVersionError: org/openqa/grid/selenium/GridLauncher : Unsupported major.minor version 51.0`