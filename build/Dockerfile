FROM nvidia/cuda:11.0-runtime-ubuntu20.04
LABEL maintainer="dietrich.zinsou@hpe.com"

RUN apt-get update && apt-get install curl -y --no-install-recommends && cd /tmp/ && \
    curl -o /tmp/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash /tmp/miniconda.sh -b -p /opt/miniconda && \
    rm -rf /tmp/miniconda.sh && \
    rm -rf /var/lib/apt/lists/*

RUN /opt/miniconda/bin/conda install pytorch torchvision torchaudio cudatoolkit=11.0 -c pytorch -y

RUN /opt/miniconda/bin/conda install jupyterlab -c conda-forge -y

COPY ./kubedirector/ /tmp/
RUN cd /tmp/ && tar czf appconfig.tgz appconfig/ && \
    mkdir /opt/configscripts && \
    cp appconfig.tgz /opt/configscripts/appconfig.tgz && \
    rm -rf appconfig*

CMD ["sleep", "infinity"]
