FROM jupyter/base-notebook

# Check if cirq_version is designated
ARG cirq_version
RUN test -n "$cirq_version" || (echo "cirq_version is not set" && false)

# Install Linux packages that are needed when we install the Cirq 
USER root
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
 && apt-get install -yq --no-install-recommends \
    gcc \
    libc6-dev \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

USER $NB_UID
# Install Cirq
RUN pip install --no-cache-dir \
  cirq==${cirq_version} \
  'cirq-core[contrib]'==${cirq_version}

# Copy default notebooks
COPY --chown=${NB_UID}:${NB_GID} work /home/$NB_USER/work
