# Docker Stacks of Quantum Computing
Docker images of Quantum Computing frameworks with Jupyter notebooks

* qiskit-notebook: IBM Qiskit
* qsharp-notebook(TBD): Microsoft Q# and QDK
* circ-notebook(TBD): Google Cirq

## How to use
After executing the following command, connect to `localhost:8888/?token=blahblah` through the link in the text that comes out.
```sh
docker run -it --rm -p 8888:8888 sanori/qiskit-notebook
```

You can save Jupyter notebooks in current directory by attaching current directory (`$PWD`) to work directory as follows:
```sh
docker run -it --rm -p 8888:8888 -v "$PWD":/home/jovyan/work sanori/qiskit-notebook
```