FROM jupyter/base-notebook

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
    dotnet-sdk-6.0 \
    libgomp1 \
    libzmq3-dev pkg-config gcc \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

USER $NB_UID

# Install Q# package
RUN pip install --no-cache-dir \
  qsharp==${qsharp_version}

# Install IQ# kernel
RUN dotnet tool install Microsoft.Quantum.IQSharp -g \
  --version ${qsharp_version}
RUN .dotnet/tools/dotnet-iqsharp install \
  --user --path-to-tool="${PWD}/.dotnet/tools/dotnet-iqsharp"

# generate cache files
RUN python -c "import qsharp"

# Copy default notebooks
COPY --chown=${NB_UID}:${NB_GID} work /home/$NB_USER/work
