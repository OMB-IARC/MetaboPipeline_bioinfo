
# 1 - Convert .d to .mzML files with dockerised msconvert

This folder contains a shell script (<code>slurm_msconvert.sb</code>) and a python script (<code>dtomzML.py</code>).

The shell script (extension _.sb_) contains slurm options and two commands.

Slurm is the job scheduler of IARC's HPC. It allows to launch and monitor jobs, manage job parallelisation, allocate specific resources (computer nodes) to users. The first few lines of the file _slurm_msconvert.sb_ (starting with <code>#</code>) specify slurm options (job name, number of nodes, memory, ...). Then, the other lines are linux commands :
- the first one pulls <a href="https://hub.docker.com/r/chambm/pwiz-skyline-i-agree-to-the-vendor-licenses" target="_blank">Proteowizard docker image</a> and converts the __Docker__ image to a __Singularity__ image. Singularity is a container runtime, like Docker, and is the one deployed on IARC's HPC. The Singularity image will be created and can be seen in the subfolder <code>img_msconvert</code>;
- the second one launches the python script (<code>dtomzML.py</code>), which will convert all _.d_ files in the folder (and its subfolders) passed as argument.

For example, the data is organised as follows :

    data
    ├── Batch1
    │   ├── Blanks
    │   │   ├── Blank_1.d
    │   │   ├── Blank_2.d
    │   ├── MSMS
    │   │   ├── MSMS_1.d
    │   │   ├── MSMS_2.d
    │   ├── QCs
    │   │   ├── QC_1.d
    │   │   ├── QC_2.d
    │   ├── Samples
    │   │   ├── Sample_1.d
    │   │   ├── Sample_2.d

In this case, the command to launch to convert all _.d_ files is <code>sbatch slurm_msconvert.sb <absolute_or_relative_path>/data/Batch1</code>.

The <code>sbatch</code> command submits a slurm job with a shell script (<code>slurm_msconvert.sb</code> here), which will (as mentioned above) create the Singularity image for _msconvert_ and launches the python script with the path to data as argument.

The waiting time between the moment the job is submitted and the moment it is launched hugely depends on the queue size. Once the job is launched, it should take less than 5 minutes to create the Singularity image, and about 10 seconds per file for conversion. The logs can be seen in the <code>slurm-<job_ID>.out</code>.

In the example above, the path to data passed as argument was <code>data/Batch1</code>, then the created folder to store the _.mzML_ files will be called <code>Batch1_mzML</code> and will be stored in the current working directory. The subfolder organisation of the input data folder is preserved.


:white_check_mark: The _.d_ files are now converted to _.mzML_ !

