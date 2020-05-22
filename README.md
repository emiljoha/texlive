# Basic TeX Live enviroment container.

## What is this?

Simply a docker container with texlive-full and make installed.

## Why to use this?

My use case is I want to compile TeX documents in a CI enviroment and want to
make sure I have the same result running locally.


## How to use this?

Create a Dockerfile in you LaTeX projects root. If you do not use make to
build you can replace it with your own build command. The only important thing
is that it creates the output pdfs in a seperate directory. I use the
directory name `pdf`.

``` Dockerfile
FROM emijoh/texlive

COPY / /

RUN make
```

Then build the dockerfile, create the container, and copy out the build
directory.

``` bash
#!/bin/bash
docker build . -t cv
CID=$(docker create cv)
docker cp ${CID}:/pdf .
docker rm ${CID}

```

Now the resulting pdf will be available in the project root in a folder `pdf`.
