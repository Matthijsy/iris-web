
<p align="center">
    <img src="source/app/static/assets/img/logo.ico" />
</p>

<p align="center">
  Incident Response Investigation System
  <br>
  <br>
</p>

# IRIS

[![License: LGPL v3](https://img.shields.io/badge/License-LGPL_v3-blue.svg)](./LICENSE.txt)   
IRIS is a web collaborative platform for incident response analysts allowing to share investigations at a technical level. 

![demo_timeline](img/timeline_speed.gif)

## Getting started
It is divided in two main parts, IrisWeb and IrisModules.   
 - IrisWeb is the web application which contains the core of
Iris (web interface, database management, etc). 
 - IrisModules are extensions of the core that allow third parties to process
data via Iris (eg enrich IOCs with MISP and VT, upload and injection of EVTX into Splunk). 
 
IrisWeb can work without any modules though defaults ones are preinstalled. Head to ``Manage > Modules`` in the UI 
to configure and enable them. 

### Run IrisWeb 
The app has 5 dockers: 
- `app - iriswebapp_app`: Core of IrisWeb 
- `db`: Postgres database 
- `rabbitmq`: Message broker handling modules tasks
- `worker`: Jobs handler relying on RabbitMq 
- `nginx`: Reverse proxy

**To run:**
1. Get the last release and cd into it
2. Copy `.env.model` into `.env`
3. [Optional for non-production] Change the default credentials in the .env file at 
the root of the project:
   1. Nginx: you might want to specify your own - A pair is provided  in the `./docker/dev_certs` repository, but you might want to change with your own certificate.
   2. Database credentials: **POSTGRES_PASSWORD** and **DB_PASS** (you can also customise the usernames)
   3. IRIS secrets: **SECRET_KEY** and **SECURITY_PASSWORD_SALT**
4. Build `docker-compose build`
5. Run `docker-compose up` 

A first account called **administrator** is created by default, the password is randomly 
created and **output in the docker `app` service**. The output is pretty verbose, you can look for the following string ``WARNING :: post_init :: create_safe_admin :: >>>``.  
If you want to define an admin password at the first start, you can also create and define the environment variable **IRIS_ADM_PASSWORD**
in the `app` docker instance (see [webApp Dockerfile](./docker/webApp/Dockerfile)).

Once it is up, go to ``https://<your_instance>:4433``, login as administrator, and start using IRIS!
We also recommend immediately changing your administrator's password, either on its profile page or in the *Users* management page.

## Showcase
For a more comprehensive overview of the case features, 
you can head to [tutorials](https://dfir-iris.github.io/operations/tutorials.html), we've put some videos there.  

## Upgrades
Please read the release notes when upgrading versions. Most of the time the migrations are handled automatically, but some
changes might require manual labor depending on the version. 

## Documentation
A comprehensive documentation is available on [dfir-iris.github.io](https://dfir-iris.github.io), or one can build 
the documentation available in [here](https://github.com/dfir-iris/iris-doc-src).

## API
The API reference is available in the [documentation](https://dfir-iris.github.io/operations/api.html#references) or [documentation repository](https://github.com/dfir-iris/iris-doc-src).

## Help
You can reach us on [Discord](https://discord.gg/fwuXkpBHGz) or by [mail](mailto:contact@dfir-iris.org) if you have any question, issue or idea !

## Considerations
Iris is in its early stage. It can already be used in production, but please set backups of the database and DO NOT expose the interface on the Internet. We highly recommend using a private dedicated and secured network.

## License
The contents of this repository is available under [LGPL3 license](LICENSE.txt).

