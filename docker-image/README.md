# Docker Image Example

The provided [Dockerfile](Dockerfile) builds a [Docker](https://www.docker.com) image for SciDB `15.12`. The Dockerfile follows, step by step, the instructions provided in the official documentation, [SciDB Community Edition Installation Guide](https://paradigm4.atlassian.net/wiki/display/ESD/SciDB+Community+Edition+Installation+Guide).

The image is space *inefficient* (its size is `6GB`) and does *not* follow the Dockerfile best practices. This image is just an example.

## Building the Image

The image is built automatically on [Docker Hub]() and can be downloaded using:

```python
# docker pull rvernica/scidb-examples:15.12
```

The image can also be built locally using:

```python
# docker build --tag scidb:15.12 .
```

The image installs SciDB dependencies, downloads the SciDB source code, and builds and installs SciDB. The official location for SciDB source code is on [Google Drive](https://drive.google.com/folderview?id=0B7yt0n33Us0rT1FJdmxFV2g0OHc&usp=drive_web#list), but because Google Drive does not provide direct access to files (for example using `wget`), a [mirror](https://bintray.com/rvernica/generic) of the SciDB source in Bintray is used.

## Using the Image

The image contains an [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#/entrypoint) script which starts the SSH, PostgeSQL and SciDB servers. Upon exit, the script stops the SciDB and PostgreSQL servers. A container can be started from this image using:

```python
# docker run --tty --interactive --name scidb rvernica/scidb-examples:15.12
 * Starting OpenBSD Secure Shell server sshd                             [ OK ]
 * Starting PostgreSQL 9.3 database server                               [ OK ]
scidb.py: INFO: Found 0 scidb processes
scidb.py: INFO: start((server 0 (127.0.0.1) local instance 0))
scidb.py: INFO: Starting SciDB server.
scidb.py: INFO: start((server 0 (127.0.0.1) local instance 1))
scidb.py: INFO: Starting SciDB server.
scidb.py: INFO: start((server 0 (127.0.0.1) local instance 2))
scidb.py: INFO: Starting SciDB server.
scidb.py: INFO: start((server 0 (127.0.0.1) local instance 3))
scidb.py: INFO: Starting SciDB server.
root@132b6b44786f:/usr/src/scidbtrunk# iquery --afl --query "list('libraries')"
{inst,n} name,major,minor,patch,build,build_type
{0,0} 'SciDB',15,12,1,80403125,'Debug'
{1,0} 'SciDB',15,12,1,80403125,'Debug'
{2,0} 'SciDB',15,12,1,80403125,'Debug'
{3,0} 'SciDB',15,12,1,80403125,'Debug'
root@132b6b44786f:/usr/src/scidbtrunk# exit
exit
scidb.py: INFO: stop(server 0 (127.0.0.1))
scidb.py: INFO: Found 0 scidb processes
 * Stopping PostgreSQL 9.3 database server                               [ OK ]
# docker rm scidb
```