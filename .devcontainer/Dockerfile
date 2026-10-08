FROM bitnamilegacy/spark:3.5
USER 0
RUN install_packages curl ca-certificates git \
 && pip install --no-cache-dir \
      "jupyterlab>=4.2" "pandas>=2.2" "numpy>=1.26" "matplotlib>=3.8" \
      "pyarrow>=15.0" "ipywidgets>=8.1" findspark
# /etc/profile overwrites PATH, so login shells (bash -l, VS Code terminals)
# lose every /opt/bitnami path. Put them back for login shells too.
RUN printf '%s\n' \
      'export PATH=/opt/bitnami/python/bin:/opt/bitnami/java/bin:/opt/bitnami/spark/bin:/opt/bitnami/spark/sbin:$PATH' \
      > /etc/profile.d/00-bitnami-path.sh \
 && chmod 0644 /etc/profile.d/00-bitnami-path.sh
ENV PYSPARK_PYTHON=python
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS="lab --ip=0.0.0.0 --no-browser --NotebookApp.token='' --NotebookApp.password=''"
WORKDIR /workspace
USER 1001
CMD ["bash", "-c", "jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --NotebookApp.token='' --NotebookApp.password=''"]
