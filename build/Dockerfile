FROM nvidia/cuda:11.0-runtime-ubuntu20.04
LABEL maintainer="dietrich.zinsou@hpe.com"

RUN apt-get update && apt-get install curl -y --no-install-recommends && cd /tmp/ && \
    curl -o /tmp/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash /tmp/miniconda.sh -b -p /opt/miniconda && \
    rm -rf /tmp/miniconda.sh && \
    rm -rf /var/lib/apt/lists/*

RUN /opt/miniconda/bin/conda create -y --name py2 python=2.7
COPY requirements.txt /tmp/requirements.txt
RUN /opt/miniconda/bin/conda install -y -c conda-forge -c pytorch --file /tmp/requirements.txt

COPY ./kubedirector/ /tmp/
RUN cd /tmp/ && tar czf appconfig.tgz appconfig/ && \
    mkdir /opt/configscripts && \
    cp appconfig.tgz /opt/configscripts/appconfig.tgz && \
    rm -rf appconfig*

ENV PATH=$PATH:/opt/miniconda/envs/py2/bin/

CMD ["sleep", "infinity"]
