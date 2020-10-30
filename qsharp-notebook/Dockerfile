ARG python_version=3.7.6
FROM jupyter/base-notebook:python-${python_version}

ARG qsharp_version
RUN test -n "$qsharp_version" || (echo "qsharp_version is not set" && false)

USER root
ENV DEBIAN_FRONTEND noninteractive

# Install .NET SDK 3.1
RUN wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb \
    -O packages-microsoft-prod.deb \
  && dpkg -i packages-microsoft-prod.deb \
  && rm -f packages-microsoft-prod.deb .wget-hsts
RUN apt-get update \
  && apt-get install -yq --no-install-recommends \
    apt-transport-https \
    dotnet-sdk-3.1 \
    libgomp1 \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

USER $NB_UID

# Install Q# kernel
RUN conda install --quiet --yes -c quantum-engineering \
    qsharp=${qsharp_version} \
    pytest matplotlib \
  && conda clean --all -f -y \
  && fix-permissions "${CONDA_DIR}" \
  && fix-permissions "/home/${NB_USER}"

# generate __pycache__
RUN python -c "import qsharp"

# Copy default notebooks
COPY --chown=${NB_UID}:${NB_GID} work /home/$NB_USER/work
