# More about the JupyterLab session

This page covers what the [quickstart](README.md) skips: opening a plain terminal, choosing a notebook kernel, and what is kept after the session ends.

## Open a terminal

A terminal lets you type commands, such as `git`, `uv` or `python`, on the compute node your session runs on. In the **Launcher**, scroll to the **Other** section and click **Terminal**.

![The JupyterLab Launcher scrolled down to the Other section, with the Terminal tile boxed.](images/jupyter-terminal-tile.png)

The terminal starts in your home folder and already uses the course Python, so `python`, `uv`, `git`, `claude` and `codex` all work without any setup. To start an agent from the terminal instead of from its tile, move into your project folder and type its name:

```bash
cd ~/your-project-folder
claude
```

Replace `your-project-folder` with your folder's name. If you do not have a project folder yet, make one first with `mkdir ~/am115-project` and use that name. If `cd` prints `No such file or directory`, fix the name before you start the agent; otherwise the agent starts in your whole home folder.

The tiles do the same thing; they also let you pick the folder with the mouse.

## Resume an earlier Claude Code conversation

When you click the **Claude Code** tile, the window **Claude Code terminal session** lists your earlier conversations. Click one to continue it, or click **New Session** to start fresh.

![The Claude Code terminal session window. The New Session button is boxed.](images/jupyter-claude-new-session.png)

## Choose the course kernel for notebooks

A **kernel** is the Python program that runs a notebook's cells. The Launcher's **Notebook** section offers several kernels. Choose **Python 3 (APMTH 115)**. It has the course packages, such as NumPy, SciPy and pandas. The kernel labeled **System Default — no course packages** is a bare Python, and course code that imports those packages fails there. If your account also shows a kernel marked **STAGING**, leave it alone; staff use it to test changes.

## What is kept and what is not

Your home folder is shared by every session and by Academic Shell Access. Files you save there are still there in your next session. The agents also save their sign-in there, which is why a later JupyterLab session should not ask you to sign in again.

Everything running stops when the session ends: notebooks' kernels, terminals and the agent. A long calculation that is still running when the hours run out is stopped partway. See [How many hours and CPUs to ask for](resources.md).

Which tabs were open in JupyterLab may not be restored in your next session, so save your work in files.

[Back to the quickstart](README.md)
