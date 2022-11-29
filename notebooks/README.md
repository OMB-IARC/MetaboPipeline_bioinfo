# 3 - Jupyter notebooks to identify potential biomarkers


Now that we have our peak table, identification and the associated metadata, we can apply various machine learning methods to identify potential biomarkers.

In the available notebooks, the point is to explore the data we got from _metaboigniter_, apply statistical analysis, visualisations and machine learning models.


This folder contains 3 scripts :
- <code>run_commands_docker.sh</code>
- <code>run_commands_singularity.sh</code>
- <code>slurm_notebooks.sb</code>

The first two scripts (<code>run_commands_docker.sh</code> and <code>run_commands_singularity.sh</code>) contain the command to pull the docker image from the DockerHub, and convert it to a Singularity image if Singularity is chosen. These two scripts also contain the command to run the image, which will create an URL to paste in a browser to access notebooks in a JupyterLab environment.

The script with the _.sb_ extension contains slurm options and commands to use the above scripts via Slurm.
Slurm is the job scheduler of IARC's HPC. It allows to launch and monitor jobs, manage job parallelisation, allocate specific resources (computer nodes) to users. The first few lines (starting with <code>#</code>) of a slurm file (here <code>slurm_msconvert.sb</code>) specify slurm options (job name, number of nodes, memory, ...). Then, the other lines are linux commands, here to launch <code>run_commands_docker.sh</code> or <code>run_commands_singularity.sh</code>.


## Tutorial

First, open a terminal on your local machine and connect to IARC's HPC with _ssh_ using the following command :
```bash
ssh <user>@10.120.1.20 -L 8888:127.0.0.1:8888
```
The <code>-L</code> option specifies which port on client (local) will be forwarded to which host and port on remote ([cf doc](https://explainshell.com/explain?cmd=ssh+-L)).


Next, go to the directory where you previsouly cloned this repository, inside <code>notebooks</code> subfolder :
```bash
cd <path_to_repo>/MetaboPipeline_bioinfo/notebooks
```


At this point you have four options to use the notebooks :
- option 1 : Use Docker
- option 2 : Use Singularity
- option 3 : Launch notebooks with Slurm
- option 4 : Launch each notebook in Binder (still in development)


## Option 1 - Use Docker

The first option is to use the notebooks with Docker.

The only command to run is :

```bash
./run_commands_docker.sh
```

First, it will pull and build the Docker image based on the image on [DockerHub](https://hub.docker.com/r/maxvin/data_science_img).

Then, it will clone the repository containing the notebooks [link](https://github.com/OMB-IARC/MetaboPipeline_notebooks).

Finally, it will run the Docker image, launching a JupyterLab environment to use the notebooks. On your terminal will appear a URL of this form <code>http://127.0.0.1:8888/lab?token=TOKEN</code> that you will have to paste in a browser to launch the JupyterLab session.



## Option 2 - Use Singularity

The second option is to use the notebooks with Singularity.

The only command to run is :

```bash
./run_commands_singularity.sh
```

First, it will pull the Docker image from [DockerHub](https://hub.docker.com/r/maxvin/data_science_img) and build the Singularity image from it.

Then, it will clone the repository containing the notebooks [link](https://github.com/OMB-IARC/MetaboPipeline_notebooks).

Finally, it will run the Singularity image, launching a JupyterLab environment to use the notebooks. On your terminal will appear a URL of this form <code>http://127.0.0.1:8888/lab?token=TOKEN</code> that you will have to paste in a browser to launch the JupyterLab session.





## Option 3 - Launch notebooks with Slurm

The third option is to launch the notebooks using Slurm.

The only command to run is :

```bash
sbatch slurm_notebooks.sb <container_choice>
```

The argument <code>container_choice</code> is either "docker" or "singularity", depending on which framework you want to use.

Depending on the container choice, it will run either the file <code>run_commands_docker.sh</code> or <code>run_commands_singularity.sh</code>. In the <code>.out</code> file of your slurm job, you will see a URL of this form <code>http://127.0.0.1:8888/lab?token=TOKEN</code> that you will have to paste in a browser to launch the JupyterLab session.






## Option 4 - Launch each notebook in Binder (still in development)

The notebooks and their links to Binder can be found on this repository : [maxvincent24/metabopipeline_notebooks](https://github.com/OMB-IARC/MetaboPipeline_notebooks)




