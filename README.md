Paperwork - OpenSource note-taking & archiving
==============================================
[![Build Status](https://travis-ci.org/twostairs/paperwork.svg?branch=master)](https://travis-ci.org/twostairs/paperwork)

![paperwork-logo](https://raw.githubusercontent.com/twostairs/paperwork/master/paperwork-logo.png)

Paperwork aims to be an open-source, self-hosted alternative to services like Evernote (R), Microsoft OneNote (R) or Google Keep (R).

Paperwork is written in PHP, utilising the beautiful Laravel 4 framework. It provides a modern web UI, built on top of AngularJS & Bootstrap 3, as well as an open API for third party integration.

For the back-end part a MySQL database stores everything. With such common requirements (Linux, Apache, MySQL, PHP), Paperwork will be able to run not only on dedicated servers, but also on small to mid-size NAS devices (Synology (R), QNAP (R), etc.).

## Screenshots (might not be up to date, please use the demo below!)

![01](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/01.png)
![02](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/02.png)
![03](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/03.png)
![04](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/04.png)
![05](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/05.png)
![06](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/06.png)
![07](https://raw.githubusercontent.com/twostairs/paperwork/gh-pages/images/screenshots/07.png)

## Demo (yes, there is one!)

At [demo.paperwork.rocks](http://demo.paperwork.rocks) you can actually see the current development status of Paperwork. Every night at 3am (CET) the database is being dropped and newly created, and the latest sources from GitHub are being deployed on the machine.

Feel free to create/modify/delete accounts, notebooks and notes. This demo can be used for heavy playing without regrets. Just try not to take down that thing. :)

## Run (quick & dirty documented)

First of all, you need to clone this project to your machine. After that, make sure that you have one of the latest PHP versions > 5.1 and an up-to-date "composer" installed. If you're not sure how composer works, please continue reading here: https://getcomposer.org/

Second, you need to switch to the command line: "cd" into the "frontend" directory of your local paperwork clone. There, run "composer install" and/or "composer update". This will install all the needed dependencies.

Now, before you do anything else, please check the files within the frontend/app/config/ directory. Especially the database.php. If you'd like to use the default DB settings (MySQL/MariaDB), you'll just need to have the database server running on port 3306 and create a database named "paperwork". You could use this SQL:

```
DROP DATABASE IF EXISTS paperwork; CREATE DATABASE IF NOT EXISTS paperwork DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```

In addition, you need the "paperwork" user to have full access to this database:

```
GRANT ALL PRIVILEGES ON paperwork.* TO 'paperwork'@'localhost' IDENTIFIED BY 'paperwork' WITH GRANT OPTION; FLUSH PRIVILEGES;
```

With these settings, you won't need to modify the database.php configuration file.

After completing these steps, run the migration jobs, that fill the database:

```
php artisan migrate
```

If anything here should fail, it's most likely an authentication/connection issue, so check your database setup again.

Now, for the last step, make sure that your Webserver has the right to create/modify/delete files within the frontend/app/storage/attachments/ folder. This folder is being used for uploaded documents.

That's pretty much it. From here on, you should be able to access your paperwork instance through the web.

## Run using Docker

Basically you just have to:

    fig up

To run the migrations (once):

    fig run web php artisan migrate --force

## API documentation

The API documentation can be found at [docs.paperwork.apiary.io](http://docs.paperwork.apiary.io/) or built using the ``apiary.apib`` file from this repository. It's not yet complete and could change at any time!

## Some last words

The current development status is far from being worth called "version 1.0". However, if I could get you interested in this project and you feel like contributing, don't hesitate to ping me by e-mail ([marius@twostairs.com](mailto:marius@twostairs.com)) or twitter ([@devilx](https://twitter.com/devilx)) so we can talk. :-)