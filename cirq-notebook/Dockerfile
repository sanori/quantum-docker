FROM jupyter/base-notebook

# Check if cirq_version is designated
ARG cirq_version
RUN test -n "$cirq_version" || (echo "cirq_version is not set" && false)

USER $NB_UID
# Install Cirq
RUN pip install --no-cache-dir \
  'cirq[contrib]'==${cirq_version}

# Copy default notebooks
COPY --chown=${NB_UID}:${NB_GID} work /home/$NB_USER/work
