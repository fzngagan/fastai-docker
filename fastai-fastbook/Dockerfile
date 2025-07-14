# Paperspace base image is located in Dockerhub registry: paperspace/gradient_base
# Paperspace Fast.ai image is located Dockerhub registry: paperspace/fastai

# ==================================================================
# Initial Setup
# ------------------------------------------------------------------
    
    FROM paperspace/gradient-base:pt211-tf215-cudatk120-py311-20240202


# ==================================================================
# Directories & Tools
# ------------------------------------------------------------------

    RUN mkdir /content && \
        apt-get update -y && \
        apt-get install -y graphviz


# ==================================================================
# Mambaforge
# ------------------------------------------------------------------

    # Based on https://github.com/conda-forge/miniforge
    ENV CONDA_OVERRIDE_CUDA="12.8"
    RUN wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh" && \
        bash Miniforge3-$(uname)-$(uname -m).sh -b && \
        ~/miniforge3/bin/conda init && \
        ~/miniforge3/bin/conda install jupyter jupyterlab ipython py-xgboost=*=cuda* -c conda-forge -y && \
        rm Miniforge3-$(uname)-$(uname -m).sh
    ENV PATH=$PATH:~/miniforge3/bin/conda


# ==================================================================
# Fast.ai
# ------------------------------------------------------------------

    RUN python3 -m pip install --upgrade pip && \
        python3 -m pip install --upgrade fastai >=2.8.2 && \
        python3 -m pip install --upgrade fastbook && \
        python3 -m pip install --upgrade xgboost && \
        python3 -m pip install --upgrade jupyterlab-git


# ==================================================================
# Config & Startup
# ------------------------------------------------------------------

    ENV USER fastai
    WORKDIR /notebooks
    RUN chmod -R a+w /notebooks
    WORKDIR /notebooks

    COPY run.sh /run.sh
    RUN chmod +x /run.sh

    CMD ["/run.sh"]
