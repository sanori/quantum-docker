# Qsharp-notebook

Qsharp-notebook is a Jupyter Docker Stack image for Microsoft QDK and Q# programming language.

This image includes the .NET SDK and the Q# kernel for Jupyter.
It also includes `pytest` and `matplotlib` to run Quantum Katas.


## How to use
After executing the following command, connect to `localhost:8888/?token=blahblah` through the link in the text that comes out.
```sh
docker run -it --rm -p 8888:8888 sanori/qsharp-notebook
```

You can save Jupyter notebooks in the current directory by attaching the current directory (`$PWD`) to work directory as follows:
```sh
docker run -it --rm -p 8888:8888 -v "$PWD":/home/jovyan/work sanori/qsharp-notebook
```

### How to Run the Quantum Katas
The [Quantum Katas](https://github.com/microsoft/QuantumKatas) is a good starting point for learning quantum computing and Q# language.

One can download the Katas and solve exercises locally with this docker image as follows:

1. Download Quantum Katas
```sh
git clone https://github.com/Microsoft/QuantumKatas.git
```

2. Run Docker container with mounting Quantum Katas directory
```sh
docker run --rm -it -p 8888:8888 -v "$PWD/QuantumKatas":/home/jovyan/QuantumKatas sanori/qsharp-notebook
```

## Alternatives
One may create a Docker image based on Microsoft's docker images:
  * mcr.microsoft.com/quantum/iqsharp-base
  * mcr.microsoft.com/quantum/samples