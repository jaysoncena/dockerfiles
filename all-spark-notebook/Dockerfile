FROM jupyter/all-spark-notebook


RUN conda create --quiet --yes -p $CONDA_DIR/envs/python2 python=2.7 ipython ipykernel kernda && \
    conda clean -tipsy

RUN $CONDA_DIR/envs/python2/bin/python -m ipykernel install --prefix $CONDA_DIR && \
$CONDA_DIR/envs/python2/bin/kernda -o -y $CONDA_DIR/share/jupyter/kernels/python2/kernel.json

USER $NB_USER
