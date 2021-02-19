If you are experiencing an issue, please read through this list first before contacting our team.

We have compiled this FAQ from the most common problems. If you are running into an issue that is not on this page, please feel free to [reach out to our team][1].

## General questions

**Q. Why am I getting a message saying `"_tkinter.TclError: no display name and no $DISPLAY environment variable"`?**

**A.** This may be due to logging into Biowulf without enabling X11 forwarding.

X11 is needed to instantiate Pipeliner's tkinter-based graphical user interface. To enable X11 forwarding, please use the `-Y` flag when logging into Biowulf:

```bash
# Enable X11 forwarding
ssh -Y $USER@biowulf.nih.gov
```

After re-logging into Biowulf with `-Y`, we can check if enabling X11 solved the problem. You can check this by running `xeyes` after logging into Biowulf. If everything is properly setup, you will be greeted by a set of cartoon eyes that follows position of your mouse.

If you are still receiving error messages, this is an indication that you do not have X-windows software installed on your local machine.  Here are instruction to install an X11 client.

!!! Install-X11 "Install X11 client"

    === "macOS"

        _XQuartz_

        As of OS X `10.6`, X11 is no longer included with the mac's OS. The X11 server and client libraries for OS X are available from the [XQuartz project](http://xquartz.macosforge.org). Please download the latest available version of XQuartz that is compatible with your operating system.

    === "Windows"

        _NoMachine (NX)_

        Windows users can install the X-window client NoMachine (NX). Graphical applications can display within the NoMachine window, and terminal sessions can be saved and reconnected in a persistent manner. Please [download the latest NX](https://www.nomachine.com/) client.

        Here are some more details from HPC staff to help you getting started with NoMachine:
        ```
        # Configuration for Helix or Biowulf
        To set up a new connection:

        Click 'New' from the top menu.
        Protocol: Set the Protocol to SSH.
        Host: Set the Host to either helix.nih.gov or biowulf.nih.gov. The port must be 22.
        Authentication: Choose Use the system login.
        Authentication: Choose Password.
        Proxy: Choose Don't use a proxy.
        Save as: Any choice is a good choice.
        Once the connection is set, double click on the connection and enter your username and password.
        NOTE: Never check the "Save Your Password" button.

        Once the login is successful and a connection has been established, a session must be chosen or created.
        If this is the first time, or no previous sessions are available, click "Create a new virtual desktop".
        Save the setting in the connection file. Otherwise, choose the previous session to open.
        ```
        Please see NoMachine's [documentation](https://www.nomachine.com/getting-started-with-nomachine) for more information.

## Job Status

**Q. How do I know if Pipeliner finished running successfully?**

**A.** There are several different ways of checking the status of each job submitted to the cluster.  
Here are a few suggestions:

!!! Job-status "Check Job Status"

    === "HPC Dashboard"

        You can check the status of Biowulf jobs through the your [user dashboard](https://hpc.nih.gov/dashboard/).

        Each job that Pipeliner submits to the cluster starts with the `pl:` prefix.

    === "Snakemake Log"

        [Snakemake](https://snakemake.readthedocs.io/en/stable/) generates the following file, `Reports/snakemake.log`, in each pipeline's working directory. This file contains information about each job submitted to the job scheduler. If there are no problems, snakemake will report 100% steps done in those last few lines of the file.

        You can take a peek of the end of the file by running the following command:
        ```bash
        tail -n30 Reports/snakemake.log
        ```
        
        Or more specifically, you can pull out the timestamps of the last few completed jobs like this:
        ```bash
        grep -A 1 done Reports/snakemake.log | tail
        ```
        

    === "Query Job Scheduler"

        SLURM has built-in commands that allow a user to view the status of jobs submitted to the cluster.

        **Method 1:** To see what jobs you have running, run the following command:
        ```bash
        squeue -u $USER
        ```

        **Method 2** You can also run this alternative command to check the status of your running jobs:
        ```bash
        sjobs
        ```

        Each job that Pipeliner submits to the cluster starts with the `pl:` prefix.


**Q. How do I identify failed jobs?**

**A.** If there are errors, you'll need to identify which jobs failed and check its corresponding SLURM output file. 
The SLURM output file may contain a clue as to why the job failed.

!!! Failed-jobs "Find Failed Jobs"

    === "HPC Usage Table"
        Pipeliner gathers runtime statistics for each job submitted to the cluster.

        This information is aggregated in a file called `HPC_usage_table.txt`. The fourth column of this tab-delimited file contains the job state. If the job successfully finished, it will be listed as **COMPLETED**.

        ```bash
        awk -F '\t' '(NR==1) || ($4=="COMPLETED") {print}' HPC_usage_table.txt
        ```

        This file also contains information about memory usage and other resources allocated at submission. This file can be used to determine if the job needs to be re-submitted with higher memory or an increased walltime.


    === "SLURM output files"

        Quick and dirty method to search for failed jobs by looking through each job's output file:

        ```bash
        grep -i 'fail' slurmfiles/slurm-*.out
        ```

    === "Snakemake Log"

        [Bash script]( https://github.com/CCBR/Tools/blob/master/Biowulf/get_slurm_file_with_error.sh) identify the SLURM ID of the first failed job and check if the output file exists.


Many failures are caused by filesystem or network issues on Biowulf, and in such cases, simply re-starting the Pipeline should resolve the issue. Snakemake will dynamically determine which steps have been completed, and which steps still need to be run. If you are still running into problems after re-running the pipeline, there may be another issue. If that is the case, please feel free to [contact us][1].


**Q. How do I cancel ongoing Pipeliner jobs?**

**A.** Sometimes, you might need to manually stop a Pipeliner run prematurely, perhaps because the run was configured incorrectly or if a job is stalled.  Although the walltime limits will eventually stop the workflow, this can take up to 5 or 10 days depending on the pipeline.

To stop Pipeliner jobs that are currently running, you can follow these options.

!!! Cancel-jobs "Cancel running jobs"

    === "Manual Inspection"
        You can use the `sjobs` tool [provided by Biowulf](https://hpc.nih.gov/docs/biowulf_tools.html#sjobs) to monitor ongoing jobs.

        Examine the `NAME` column of the `sjobs` output, one of them should match what you entered as the 'Project Id' in the Pipeliner GUI. This is the "primary" job that coordinates secondary job submissions as steps are completed.
        
        You can [manually cancel](https://hpc.nih.gov/docs/userguide.html#delete) the primary job using `scancel`.
        
        However, secondary jobs that are already running will continue to completion (or failure).  To stop them immediately, you will need to run `scancel` individually for each secondary job. See the next tab for a bash script that tries to automate this.

    === "Bash Script"
        When there are lots of secondary jobs running, or if you have multiple Pipeliner runs ongoing simultaneously, it's not feasible to manually cancel jobs based on the `sjobs` output (see previous tab).
        
        We provide [a script](https://github.com/CCBR/Tools/blob/master/Biowulf/cancel_snakemake_jobs.sh) that will parse the snakemake log file and cancel all jobs listed within.

        ```bash
        ## Download the script (to the current directory)
        wget https://raw.githubusercontent.com/CCBR/Tools/master/Biowulf/cancel_snakemake_jobs.sh
        
        ## Run the script
        bash cancel_snakemake_jobs.sh /path/to/snakemake.log
        ```
        
        The script accepts one argument, which should be the path to the snakemake log file.  This will work for any log output from Snakemake version `5.1.3`.
        
        This script will NOT cancel the primary job, which you will still have to identify and cancel manually, as described in the previous tab.

Once you've ensured that all running jobs have been stopped, you need to unlock the working directory (see [below](https://pipeliner-docs.readthedocs.io/en/latest/troubleshooting/#job-errors)), and re-run Pipeliner to continue the workflow.

## Job Errors

**Q. Why am I getting `sbatch: command not found error`?**

**A.** Are you running the `ccbrpipeliner/4.0` on `helix.nih.gov` by mistake. [Helix](https://hpc.nih.gov/systems/) does not have a job scheduler. One may be able to fire up the ccbrpipeliner module, initial working directory and perform dry-run on `helix`. But to submit jobs (Run button), you need to log into `biowulf` using `ssh -Y username@biowulf.nih.gov`.


**Q. Why am I getting a message saying `Error: Directory cannot be locked. ...` when I do the dry-run?**

**A.** This is caused when a run is stopped prematurely, either accidently or on purpose.  This can be remedied easily by running `snakemake --unlock`, but the version of snakemake needs to match what Pipeliner uses (which is no longer the default on Biowulf).

```bash
## Navigate to working directory
cd /path/to/working/dir

## Load the right version of snakemake
modue load snakemake/5.1.3

## Unlock
snakemake --unlock
```


<!-- Relative links -->
  [1]: contact-us.md
