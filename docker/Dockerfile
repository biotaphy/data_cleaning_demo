FROM conda/miniconda3:latest as data_cleaning

RUN conda update -n base -c conda-forge conda
RUN conda install -y -c conda-forge gdal libspatialindex rtree

RUN apt-get update && \
    apt-get install -y git

RUN mkdir git && \
    cd git && \
    git clone https://github.com/specifysystems/lmpy.git

# RUN cd git/lmpy && \
#     pip install .

RUN pip install specify-lmpy
