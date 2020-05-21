# ttl2virtuosodb

Load RDF-Turtle format data in parallel to the RDF triplestore [Virtuoso docker conatiner](https://hub.docker.com/r/openlink/virtuoso-opensource-7) and generate `virtuoso.db` file for migration.

## Requirement

- Docker-compose (Compose file version 3)

## Usage

```
$ git clone https://github.com/intuano/ttl2virtuosodb
$ cd ttl2virtuosodb
```

### Load turtle data

Place your ttl files in the `data` directory, otherwise test data will be loaded:

```
$ mv /path/to/*ttl data
```

Initialize loading process, may take time depending on the file size:

```
$ ./bin/ttl2virtuosodb add
```

After the process finished successfully, the Virtuoso DB file will be in the db directory:

```
$ ls db
virtuoso-temp.db virtuoso.db      virtuoso.ini     virtuoso.lck     virtuoso.log     virtuoso.pxa     virtuoso.trx
```

### Parameters

Set Virtuoso port number (default: 8890):

```
$ export T2V_VIRTUOSO_PORT=1234
$ ./bin/ttl2virtuosodb add
```

Set maximum memory usage (in KB, default: system max memory). For 8GB:

```
$ export T2V_VIRTUOSO_MAX_MEMORY=8000000
$ ./bin/ttl2virtuosodb add
```

Set number of threads for loading (default: 4). For 16 threads:

```
$ export T2V_NUMBER_OF_THREADS=16
$ ./bin/ttl2virtuosodb add
```

Set RDF graph name (default: http://bio.cow/graph):

```
$ export T2V_RDF_GRAPH_NAME=http://fantastic.graph.name/yeah
$ ./bin/ttl2virtuosodb add
```

### Other commands

Run Virtuoso docker container with an existing `virtuoso.db` file:

```
$ ./bin/ttl2virtuosodb up
```

Run SPARQL queries stored in the `sparql` directory for testing:

```
$ ./bin/ttl2virtuosodb test
```

Show status of docker-compose and docker containers:

```
$ ./bin/ttl2virtuosodb status
```

Stop Virtuoso docker container:

```
$ ./bin/ttl2virtuosodb down
```

Remove `virtuoso.db` file and `docker-compose.yml` file generated by the script:

```
$ ./bin/ttl2virtuosodb clean
```

Show usage:

```
$ ./bin/ttl2virtuosodb help
```

Show version information:

```
$ ./bin/ttl2virtuosodb version
```

To access the Virtuoso SPARQL endpoint via web browser, open [`localhost:8890/sparql`](https://localhost:8890/sparql):
