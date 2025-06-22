# Cleaver

Map and manage your personal relationships


Cleaver is a planned open-source Personal Relationship Manager (PRM). It helps you move beyond a simple list of contacts to a meaningful, interactive map of your personal and familial network. It's designed to be a private, simple, and powerful tool for anyone who wants to better understand and nurture the connections in their life.

## Introduction

Your phone's contacts app is a list of names and numbers. A CRM is a tool for managing sales leads. Cleaver is different. It's a space for you to document the relationships you care about—family, friends, and colleagues—and visualize how they all connect.

We will start with the basics of a great contacts app and add a powerful relationship engine, all while prioritizing your privacy and data ownership.

## Core Principles

This project is guided by a few key principles:

* **Simple is Better:** Cleaver aims for simplicity in its features, its code, and its user experience. It should do a few things very well.
* **You Own Your Data:** Your data is yours. Period. Cleaver is designed to be self-hosted, and you can easily import and export your information at any time using open formats like CSV and GEDCOM.
* **Private by Design:** There is no tracking, no advertising, and no cloud-based AI scanning your personal information. It's your server, your data.
* **Pragmatic & Open:** We favor practical solutions that deliver value now. The project will be open-source from day one.

## Planned Features

The goal is to build a platform with the following capabilities:

* **Contact Management:** A robust system to add and manage all the people you know.
* **Effortless Data Import:** Get your data in easily with **CSV** and **vCard** import.
* **Relationship Mapping:** Define relationships between your contacts (e.g., Friend, Family, Colleague).
* **Interaction Logging:** Keep a simple log of your activities and conversations with your contacts.
* **Event Reminders:** Get gentle reminders for birthdays and important anniversaries.
* **GEDCOM Compatibility:** Import and export your data using the standard format for genealogical data, ensuring you're never locked in.
* **Visual Network Graph:** An interactive visualization of your relationship map to see the bigger picture.

## Roadmap

Development will proceed in phases, with each phase delivering a more capable application.

1. **Phase 1: The Core PRM.** The initial focus is on building a functional contacts application. This includes creating the core contact model, enabling data import via CSV, and setting up basic user authentication.
2. **Phase 2: The Connected Network.** This phase introduces the core feature: relationships. We will build the functionality to link contacts together and display those connections.
3. **Phase 3: The Genealogical Bridge.** We will add compatibility with the GEDCOM standard, starting with a robust export feature to ensure data portability, followed by a basic importer.
4. **Phase 4 & Beyond: Enhancing the Experience.** Later phases will focus on quality-of-life improvements like interaction logging, event reminders, and a more dynamic user interface.

---

[![Built with Cookiecutter Django](https://img.shields.io/badge/built%20with-Cookiecutter%20Django-ff69b4.svg?logo=cookiecutter)](https://github.com/cookiecutter/cookiecutter-django/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

License: GPLv3

## Settings

Moved to [settings](https://cookiecutter-django.readthedocs.io/en/latest/1-getting-started/settings.html).

## Basic Commands

### Setting Up Your Users

- To create a **normal user account**, just go to Sign Up and fill out the form. Once you submit it, you'll see a "Verify Your E-mail Address" page. Go to your console to see a simulated email verification message. Copy the link into your browser. Now the user's email should be verified and ready to go.

- To create a **superuser account**, use this command:

      $ python manage.py createsuperuser

For convenience, you can keep your normal user logged in on Chrome and your superuser logged in on Firefox (or similar), so that you can see how the site behaves for both kinds of users.

### Type checks

Running type checks with mypy:

    $ mypy cleaver

### Test coverage

To run the tests, check your test coverage, and generate an HTML coverage report:

    $ coverage run -m pytest
    $ coverage html
    $ open htmlcov/index.html

#### Running tests with pytest

    $ pytest

### Live reloading and Sass CSS compilation

Moved to [Live reloading and SASS compilation](https://cookiecutter-django.readthedocs.io/en/latest/2-local-development/developing-locally.html#using-webpack-or-gulp).

### Celery

This app comes with Celery.

To run a celery worker:

```bash
cd cleaver
celery -A config.celery_app worker -l info
```

Please note: For Celery's import magic to work, it is important _where_ the celery commands are run. If you are in the same folder with _manage.py_, you should be right.

To run [periodic tasks](https://docs.celeryq.dev/en/stable/userguide/periodic-tasks.html), you'll need to start the celery beat scheduler service. You can start it as a standalone process:

```bash
cd cleaver
celery -A config.celery_app beat
```

or you can embed the beat service inside a worker with the `-B` option (not recommended for production use):

```bash
cd cleaver
celery -A config.celery_app worker -B -l info
```

### Email Server

In development, it is often nice to be able to see emails that are being sent from your application. For that reason local SMTP server [Mailpit](https://github.com/axllent/mailpit) with a web interface is available as docker container.

Container mailpit will start automatically when you will run all docker containers.
Please check [cookiecutter-django Docker documentation](https://cookiecutter-django.readthedocs.io/en/latest/2-local-development/developing-locally-docker.html) for more details how to start all containers.

With Mailpit running, to view messages that are sent by your application, open your browser and go to `http://127.0.0.1:8025`

### Sentry

Sentry is an error logging aggregator service. You can sign up for a free account at <https://sentry.io/signup/?code=cookiecutter> or download and host it yourself.
The system is set up with reasonable defaults, including 404 logging and integration with the WSGI application.

You must set the DSN url in production.

## Deployment

The following details how to deploy this application.

### Docker

See detailed [cookiecutter-django Docker documentation](https://cookiecutter-django.readthedocs.io/en/latest/3-deployment/deployment-with-docker.html).

### Custom Bootstrap Compilation

The generated CSS is set up with automatic Bootstrap recompilation with variables of your choice.
Bootstrap v5 is installed using npm and customised by tweaking your variables in `static/sass/custom_bootstrap_vars`.

You can find a list of available variables [in the bootstrap source](https://github.com/twbs/bootstrap/blob/v5.1.3/scss/_variables.scss), or get explanations on them in the [Bootstrap docs](https://getbootstrap.com/docs/5.1/customize/sass/).

Bootstrap's javascript as well as its dependencies are concatenated into a single file: `static/js/vendors.js`.
