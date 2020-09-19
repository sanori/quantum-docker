# Qiskit-notebook

Qiskit-notebook is a Jupyter Docker Stack image for IBM Qiskit.

This image includes the visualization package.

## How to use
After executing the following command, connect to `localhost:8888/?token=blahblah` through the link in the text that comes out.
```sh
docker run -it --rm -p 8888:8888 sanori/qiskit-notebook
```

You can save Jupyter notebooks in the current directory by attaching the current directory (`$PWD`) to work directory as follows:
```sh
docker run -it --rm -p 8888:8888 -v "$PWD":/home/jovyan/work sanori/qiskit-notebook
```
