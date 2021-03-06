SlurmTemp
=========

Automatically create and send slurm scripts to the Cigene cluster. 
You can modify job name, log name and number and CPUs for the job with command line options.

### Help text
```bash
usage: SlurmTemp.py [-h] [-n CPUS] [-j JOBNAME] unix_command

positional arguments:
  unix_command          - command needs to be in "" if multiple arguments

optional arguments:
  -h, --help            show this help message and exit
  -n CPUS, --cpus CPUS  - number of CPUs as integer
  -j JOBNAME, --jobname JOBNAME
                        Custom SLURM job name
```
####Installation
*Make shure you have a bin folder in your HOME dir. `~/bin/`*
```bash
cd ~/
git clone git@github.com:timknut/bioinf_tools.git # Clone from github
cd ~/bin/
ln -s ~/bioinf_tools/Slurmtemp.py # Make symlink to Executable.
```

####Example:
The following bash command will reproduce the script below

`Slurmtemp.py "module load bamtools && bamtools merge $(for file in $(ls *RG.bam); do echo " -in "$file; done) -out outbam.merge.bam -forceCompression" 2 -j MySlurmJob`

```bash
#!/bin/bash -x
#SBATCH -J MySlurmJob
#SBATCH -N 1
#SBATCH -n 2
#SBATCH --output=MySlurmJob%j.out 
module load bamtools && bamtools merge $(for file in $(ls *RG.bam); do echo " -in "$file; done) -out outbam.merge.bam -forceCompression
```
