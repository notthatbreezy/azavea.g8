# $name$
An API project that uses http4s and doobie

## Requirements

- Vagrant 2.0+
- VirtualBox 4.3+

## Quick Setup
```
./scripts/setup
```

Then `ssh` into the machine when that is complete and start the server with `./scripts/server`. In another shell inside the VM you should be able to make a request:

`http :$api_port$/api/hello/world`

### VM rsync

In order to sync file changes to the Vagrant VM, you'll need to run `vagrant rsync-auto` in a separate terminal while developing. Otherwise files will only be copied into the VM when it boots. `rsync` is used because when compiling inside the VM traditional file-sharing can be slow and cumbersome.

## Developing

The VM includes [HTTPie](https://httpie.org/) and the
[HTTPie JWT Auth plugin](https://github.com/teracyhq/httpie-jwt-auth) in order to make
authentication with APIs as seamless as possible. All following commands should be run within the VM.

### Nexus Repository Manager

When developing at the Azavea office, strongly consider use of the Nexus proxy. This is automatically configured in project setup. If you are not connected to the `vpn` you will need to disable it by deleting or moving `app-backend/.sbtopts`.

### Project Organization

By default the backend is organized into 3 subprojects:
 - api: handles all routes, authentication, and services
 - datamodel: case classes for data the api operates on
 - database: handles database interaction with models

### Migrations
This project uses [flyway](https://flywaydb.org/) for migrations. The migrations are stored in the database subproject (`app-backend/database/src/main/resources/db/migrations`). For information on the naming and formatting conventions consult the [documentation](https://flywaydb.org/documentation/migrations#naming). Each migration should be `sql` and generally follows the format of `V<number>__<description>.aql`.

Running migrations and other tasks are managed through `./scripts/migrate`.

### Development workflow
Usually at least two terminals should be open for doing development. The first terminal is where `sbt` should be run (`./scripts/console sbt`). In this terminal tests can be run, projects compiled, and the server assembled.

The other terminal is where the server should be run `./scripts/server` or other one-off commands. To see changes you made to the API live you will need to first assemble the `jar` for the `api` server.
