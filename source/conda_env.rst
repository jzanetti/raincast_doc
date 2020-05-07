Install RainCast
============================
It is recommended to create an conda environment first. Later this environment can be used either alone or being dockerized

Create the conda environment
^^^^^^^^^^^^^^^^^^^^
The env.yml file is provided with the software, the user can run::

    conda env create -f env.yml

All the required dependancies should come from the conda-forge channel. The environment can be started using::

    conda activate raincast

Build the package
^^^^^^^^^^^^^^^^^^^^
The package can be built through::

    conda build . --no-test

The built package shall be installed under the raincast environment using::

    conda install -f <package>

