# Data Loading Example

* Requirements: `SciDB 15.12`
* Usage: `./rec.sh`
* See: [The Power of Loading Data - Part 2](http://rvernica.github.io/2016/06/load-data-non-int)

Assumes SciDB is running on the localhost on the default port and no authentication is required. Running the script results in two new arrays, `rec` and `rec_letter`.

The [`Dockerfile`](Dockerfile) provided is used to test that the example runs successfully. The Dockerfile builds a Docker image. The build starts from a SciDB image, adds the example, and runs the example. Finally, it compares the produced output with the expected output (`test.gold`). The build fails if the two outputs differ. The build results can be viewed on [Docker Hub](https://hub.docker.com/r/rvernica/scidb-examples/builds/). On each particular build, the *Logs* section (mid-way) contains the output produced by the example.
