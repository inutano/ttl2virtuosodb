# ttl2virtuosodb

Load RDF-Turtle format data in parallel to the RDF triplestore [Virtuoso docker conatiner](https://hub.docker.com/r/openlink/virtuoso-opensource-7) and generate `virtuoso.db` file for migration.

## Requirement

- Docker-compose (Compose file version 3)

## Usage

```
$ git clone https://github.com/intuano/ttl2virtuosodb
$ cd ttl2virtuosodb
```

Place your ttl files in the `data` directory, otherwise test data will be loaded:

```
$ mv /path/to/*ttl data
```

Initialize loading process, may take time depending on the file size:

```
$ ./bin/ttl2virtuosodb up
```

After the process finished successfully, the Virtuoso DB file will be in the db directory:

```
$ ls db
virtuoso.db
```

Note: If the `virtuoso.db` file exists in the `db` directory, `ttl2virtuosodb up` will not load data and just launch the SPARQL endpoint.

To access the Virtuoso SPARQL endpoint after the load, access `localhost:8890/sparql`:

```
$ open -a Google\ Chrome https://localhost:8890/sparql
```

Shutdown the virtuoso server and remove container:

```
$ ./bin/ttl2virtuosodb down
```
