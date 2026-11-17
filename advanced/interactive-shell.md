# Advanced: interactive shells with `srun`

You do not need this page to use an agent; the [quickstart](../README.md) is enough. It is for when you work from **Academic Shell Access** and want a compute node without starting JupyterLab or VS Code.

The cluster uses a **scheduler**, a program called Slurm. Slurm chooses which compute node runs your work and keeps each person's CPUs and memory separate. Every session you start from Open OnDemand is a Slurm job too; the website just fills in the request for you.

## Ask for a compute node

From Academic Shell Access:

```bash
srun --cpus-per-task=2 --mem=4G --time=01:00:00 --pty bash
```

The options say what you are asking for:

- `--cpus-per-task=2`: two CPUs;
- `--mem=4G`: 4 GB of memory;
- `--time=01:00:00`: at most one hour (hours:minutes:seconds); the shell is stopped after that;
- `--pty bash`: give me an interactive shell.

`srun` waits until a node is free, then your prompt returns on the compute node. Type `hostname` to check: it prints a compute node's name rather than the login node's.

The compute node has the scheduler's basic tools but not the course software. Run commands through the course launcher:

```bash
~/172566/course-env python my_script.py
~/172566/course-env claude
```

`~/172566/course-env` with nothing after it opens a shell where the course Python, `uv`, `claude` and `codex` are all available. Type `exit` to leave that shell.

## Leave the node

Type `exit` until the prompt shows the login node again. Leaving releases the node. If you forget, the node is released when the `--time` limit runs out.

## See what you have running

```bash
squeue -u "$USER"
```

lists your jobs, including any JupyterLab or VS Code sessions. To stop one job, use its number from the `JOBID` column:

```bash
scancel 12345
```

Always give `scancel` a job number. `scancel -u "$USER"` stops every job you have, including the JupyterLab or VS Code session you may be working in.

[Back to the quickstart](../README.md) · [Batch jobs](batch-jobs.md)
