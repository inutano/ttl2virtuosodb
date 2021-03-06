# ttl2virtuosodb

Load RDF-Turtle format data in parallel to the RDF triplestore [Virtuoso Open-Source](http://vos.openlinksw.com/owiki/wiki/VOS) running in a [docker conatiner](https://hub.docker.com/r/openlink/virtuoso-opensource-7) and generate `virtuoso.db` file for migration.

## Requirement

- [`docker-compose`](https://docs.docker.com/compose/install/) (compose file version 3)

## Usage

A bash script `ttl2virtuosodb` does: run and stop virtuoso docker container, validate turtle files, load your turtle files to virtuoso to make `virtuoso.db` file, create text index for loaded RDF data.

### Install

Clone this repository

```
$ git clone https://github.com/intuano/ttl2virtuosodb
```

or download the script and make it executable

```
$ curl -sLO "https://github.com/inutano/ttl2virtuosodb/raw/master/bin/ttl2virtuosodb"
$ chmod +x ./ttl2virtuosodb
```

### Learn

The author is kind enough to provide these subcommands to show help message:

```
$ ttl2virtuosodb help
$ ttl2virtuosodb -h
$ ttl2virtuosodb --help
```

### Load RDF

Place your ttl files in `./data` directory, then use `load` command:

```
$ ls ./data
DRA000001.experiment.ttl DRA_Accessions.100.ttl   SAMD00016353.ttl
$ ./ttl2virtuosodb load
```

Once the process finished successfully, the Virtuoso DB file will be created in the `./db` directory:

```
$ ls ./db
virtuoso-temp.db virtuoso.db      virtuoso.ini     virtuoso.lck     virtuoso.log     virtuoso.pxa     virtuoso.trx
```

### Options

Specify turtle file directory path with `-d` or `--data-dir` (default: `./data`):

```
$ ttl2virtuosodb load -d /path/to/ttl-file-dir
```

Specify virtuoso db file directory path with `-db` or `--database-dir` (default: `./db`):

```
$ ttl2virtuosodb load -db /path/to/virtuoso-database-dir
```

Specify SPARQL query directory path with `-rq` or `--sparql-dir` (default: `./sparql`):

```
$ ttl2virtuosodb load -rq /path/to/sparql-query-dir
```

Set Virtuoso port number with `-p` or `--port` (default: 8890):

```
$ ttl2virtuosodb load -p 1234
```

Set maximum memory usage with `-m` or `--max-memory` (in KB, default: system max memory). For 8GB:

```
$ ./ttl2virtuosodb load -m 8000000
```

Set number of threads for parallel loading with `-t` or `--threads` (default: 4). For 16 threads:

```
$ ./ttl2virtuosodb load -t 16
```

Set RDF graph name for loading with `-g` or `--graph` (default: http://bio.cow/graph):

```
$ ./ttl2virtuosodb load -g http://fantastic.graph.name/yeah
```

### Other commands

Run Virtuoso docker container with an existing `virtuoso.db` file:

```
$ ./ttl2virtuosodb up
```

Validate turtle files by [`ttl-validator`](https://github.com/IDLabResearch/TurtleValidator):

```
$ ./ttl2virtuosodb validate
```

Create text index for the purpose to enable text search by `bif:contains` query:

```
$ ./ttl2virtuosodb index
```

Run SPARQL queries stored in the `sparql` directory for testing:

```
$ ./ttl2virtuosodb test
```

Show status of docker-compose and docker containers:

```
$ ./ttl2virtuosodb status
```

Stop Virtuoso docker container:

```
$ ./ttl2virtuosodb down
```

Remove `virtuoso.db` file and `docker-compose.yml` file generated by the script:

```
$ ./ttl2virtuosodb clean
```

Show usage:

```
$ ./ttl2virtuosodb help
```

Show version information:

```
$ ./ttl2virtuosodb version
```

To access the Virtuoso SPARQL endpoint via web browser, open [`localhost:8890/sparql`](http://localhost:8890/sparql):
