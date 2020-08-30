# Cirq-notebook

Cirq-notebook is a Jupyter Docker Stack image for Google Cirq.

This image includes the contrib packages.

## How to use
After executing the following command, connect to `localhost:8888/?token=blahblah` through the link in the text that comes out.
```sh
docker run -it --rm -p 8888:8888 sanori/cirq-notebook
```

You can save Jupyter notebooks in the current directory by attaching the current directory (`$PWD`) to work directory as follows:
```sh
docker run -it --rm -p 8888:8888 -v "$PWD":/home/jovyan/work sanori/cirq-notebook
```

## Alternatives
One may create a Docker image based on Google's docker image:
  * [Installing on Docker](https://cirq.readthedocs.io/en/stable/install.html#installing-on-docker)
  * [quantumlib/cirq](https://hub.docker.com/r/quantumlib/cirq)

One can extend Tensorflow docker with jupyter extension by installing `tensorflow-quantum` package.
  * [Hello Many Worlds](https://www.tensorflow.org/quantum/tutorials/hello_many_worlds)
  * [tensorflow/tensorflow:*-jupyter](https://hub.docker.com/r/tensorflow/tensorflow)