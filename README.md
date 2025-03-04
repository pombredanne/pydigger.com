# PyDigger

Source code of [PyDigger](https://pydigger.com/)

See the [about page](https://pydigger.com/about) on the web site for some explanation.

See the [Video recording series](https://code-maven.com/pydigger) following the development of the application.
Specifically in the first episode you can see an explanation about it.

## Setup a development environment

* Clone the repository.
* [Install Docker](https://docs.docker.com/get-docker/).
* [Install docker-compose](https://docs.docker.com/compose/install/).
* Copy `config-skeleton.yml` to `dev.yml`.
* Sign up to [GitHub](https://github.com/)
* Create a [Personal access token](https://github.com/settings/tokens) with a name that you can easily recognize, e.g. "PyDigger Development Token" using the following rights:

```
repo
   x public_repo

user
   x read:user
   x user:email
```
* Save the token it in the `dev.yml` file in the `github-token` field.
* Copy `docker-compose.override.yml.example` to `docker-compose.override.yml` and personalize it if necessary.

In one terminal:
```
docker-compose up --build
```

Visit the web page at http://localhost:6001 At this point the database is empty.

### In another terminal connect to the shell of the Docker container

```
docker exec -it pydiggercom_cron_1 bash
```

To run the tests type in

```
pytest --cache-clear --flake8 -vs
```

To collect data from a single GitHub repository:

```
python fetch_recent.py --update url --url https://github.com/szabgab/pydigger.com --log DEBUG --screen
```

To collect data for a single PyPI package:

```
python fetch_recent.py --update package --package <PyPI package name> --log DEBUG --screen
```

Fetch data of recently uploaded packages using the RSS feed of PyPI:

```
python fetch_recent.py --update rss --screen --log DEBUG
python fetch_recent.py --update deps --screen --log DEBUG
```

### Connect to the shell of the MongoDB server

```
$ docker exec -it pydiggercom_mymongo_1 bash
# mongo -u root -p Secret # to login to mongodb
> use pydigger # pydigger is our database name
> db.dropDatabase() # To drop the pydigger database
> db.packages.find() # To list all the entries
```

Cleaning up database (during development)

```
docker exec pydiggercom_web_1 python remove_db.py
```

## Deployment

ssh to the server and run

```
./deploy.sh
```

Copyright and LICENSE
======================

Copyright 2021 Gábor Szabó

The source code in this repository is licensed under the MIT License.

The content of the site as collected from the various sources
are copyright the respective parties.

## Contributors

* Upasana Shukla
* Ed Sabol
* Greg Lawrance

