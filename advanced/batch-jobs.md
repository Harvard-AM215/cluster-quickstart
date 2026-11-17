# Advanced: batch jobs

You do not need this page to use an agent. It is for a calculation that should run on its own, without a browser tab open: a long simulation, or the same script for many parameter values.

A **batch job** is a script you hand to the scheduler. The scheduler runs it on a compute node when one is free, writes everything the script prints to a file, and stops it at the time limit. Your terminal is free in the meantime, and you can close the browser.

Submit batch jobs from **Academic Shell Access** ([Working from a plain terminal](../terminal.md)). The JupyterLab and VS Code sessions do not have the `sbatch` command.

## A batch script

Save this as `run.sbatch` in your project folder, next to the Python script it runs:

```bash
#!/bin/bash
#SBATCH --job-name=am115-demo
#SBATCH --cpus-per-task=1
#SBATCH --mem=2G
#SBATCH --time=00:10:00
#SBATCH --output=slurm-%j.out

cd "$SLURM_SUBMIT_DIR"
~/172566/course-env python model.py
```

The `#SBATCH` lines are the request: one CPU, 2 GB of memory, at most ten minutes, and output written to `slurm-<job number>.out`. The last two lines are the work. `cd "$SLURM_SUBMIT_DIR"` moves into the folder you submitted from, and `~/172566/course-env` runs the script with the course Python.

## Submit it and check on it

From the project folder:

```bash
sbatch run.sbatch
```

`sbatch` prints `Submitted batch job` and the job's number. While it waits or runs, `squeue -u "$USER"` lists it. When it is gone from that list, it has finished. That does not mean it succeeded, so check:

```bash
cat slurm-12345.out
sacct -j 12345 --format=JobID,State,ExitCode,Elapsed
```

A job that worked shows `COMPLETED` and exit code `0:0`. Then read the output file and check that the numbers make sense; a script can finish without errors and still compute the wrong thing.

## Asking the agent to help

An agent can write a batch script for your project. Tell it the command that runs your calculation, how long one run takes when you run it in a session, and how much memory it needs, and ask it for a script like the one above. Read the `#SBATCH` lines before you submit: they set what you reserve.

[Back to the quickstart](../README.md) · [Interactive shells](interactive-shell.md)
