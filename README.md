# Pangea Django Example

An example of Django project integration with Audit Log and File Intel Services.

In this example, you will see: How to integrate Pangea’s python SDK, Secure Audit Log, and File Intel service and also a File Upload feature in Python’s Django web framework.

Sample App is takn from [egorsmkv](https://github.com/egorsmkv/simple-django-login-and-register-dynamic-lang)

## Prerequisites
* Python 3
* A Pangea account - [sign up here](https://console.pangea.cloud/)
* [Create an API token](https://console.pangea.cloud/project/tokens) in Pangea Console for Secure Audit Log and File Intel Services
* Clone [this repo](https://github.com/pangeacyber/pangea-django-example)

## Installing Pangea Python SDK

The Pangea Python Django Sample contains separated logic for user accounts and app  modules. source/accounts specifically contain login and registration flows, which this tutorial will focus on.

First, add Pangea Python SDK as a dependency on the project. Open Pipfile in the project and add the lines below: 

```bash
pangea-sdk = "*"
django-environ = "*"
```

You are adding the `pangea-python-sdk` and `django-environ` latest packages to the project. 

Run the commands below to install pipenv (a python packaging & environment manager), install python dependencies, and activate the pipenv environment.

```bash
pip install pipenv
 
pipenv install
pipenv shell
```

Run the below commands to start the app and create a new user account. 

```bash
python source/manage.py migrate
 
python source/manage.py runserver
```


> Note:

* Python 3 is the default version for this project.
* Instead of modifying the Pipfile, you can install the package by running pipenv install python-pangea

## Configuring Pangea’s API Keys 

> Note: You generated API tokens to communicate with Pangea’s services in the previous section.Remember, API tokens are sensitive and should not be checked into your code. django-environ is being used to manage the environment variables through which the API tokens are accessed in the project. 

Rename the `source/app/conf/development/.env.example` file to `.env` and fill in the details below by going to the Pangea Console.

```bash
PANGEA_DOMAIN=
PANGEA_AUDIT_TOKEN=
PANGEA_FILE_INTEL_TOKEN=
```

Domain is the region where your application's services are hosted and consumed. The tokens give access to the respective services you enable in the Pangea Console. 

Add the code below to `source/app/conf/development/settings`.py to import and configure the `django-environ` package. 

```bash
import environ
 
env = environ.Env()
environ.Env.read_env()
```

Below the constants in your code, add the Pangea API token and make it accessible in the entire application.

```bash
#Pangea
PANGEA_DOMAIN = env('PANGEA_DOMAIN')
PANGEA_AUDIT_TOKEN = env('PANGEA_AUDIT_TOKEN')
PANGEA_FILE_INTEL_TOKEN = env('PANGEA_FILE_INTEL_TOKEN')
```


> Note: You can configure a different domain and API token configuration for a production environment. In this tutorial, you are configuring everything for development. 

Adding [Secure Audit Log Integration ->](https://github.com/pangeacyber/pangea-django-example/tree/2-secure-audit-log)

