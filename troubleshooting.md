# Troubleshooting

Find the message or situation you see, then follow the steps under it.

## Starting a session

**The card stays on Starting for several minutes.** Either the cluster is busy and your session is waiting for a free compute node, or the node has been found and JupyterLab or VS Code is still starting on it. Leave the page open; the card changes to **Running** on its own. If it is still on **Starting** after about ten minutes, ask a TF.

**The session disappeared, or the card says Completed.** The session's hours ran out, or it was canceled. Files you saved are still in your home folder. Launch a new session.

## Signing in

**Claude Code says `OAuth error: Invalid code`.** Something other than the sign-in code was pasted or typed at **Paste code here if prompted**. This happens if you start typing a command while that prompt is waiting. Claude Code shows **Press Enter to retry**; press **Enter** and repeat the sign-in, this time pasting only the code.

**Ctrl+C does not leave the sign-in screen.** Close the terminal instead. In JupyterLab, close the terminal's tab, then open the **Running Terminals and Kernels** panel (the circle with a square inside, in the left bar) and shut the terminal down. In VS Code, click the trash-can icon on the terminal panel.

**VS Code asks "Do you want code-server to open the external website?"** Click **Cancel**, then open the link that Claude Code printed in the terminal. See [Using VS Code](vscode.md#run-an-agent-in-a-terminal-instead).

**Clicking the sign-in link does nothing.** Press **c** while Claude Code shows the link to copy it, then paste it into a new browser tab. If that does not copy anything, hold **Shift**, select the whole link with the mouse, and copy it with **Ctrl+C** (**Cmd+C** on a Mac).

**Codex: the first option, Sign in with ChatGPT, does not finish.** Close the terminal, start Codex again, and choose **2. Sign in with Device Code**.

## Commands

**`claude: command not found` (or `codex` or `uv`).** You are on the login node in Academic Shell Access. Follow [Working from a plain terminal](terminal.md): get a compute node with `srun`, then run `~/172566/course-env claude`.

**`error: cannot run ssh: No such file or directory` from Git.** You are in a VS Code terminal, which has no `ssh` program. Run the Git command in a JupyterLab terminal or in Academic Shell Access instead; see [Getting your files onto the cluster](git.md).

**`ModuleNotFoundError: No module named 'numpy'` in a notebook.** The notebook uses the wrong kernel. Open the **Kernel** menu, choose **Change Kernel**, and pick **Python 3 (APMTH 115)**.

## The agent

**The agent asks permission before most commands.** That is its normal setting. Read each command and answer **Yes** for commands that only read files or print information. Answer **No** when you do not understand what a command changes, and ask the agent to explain.

**The agent's work stopped partway.** If the session's hours ran out, the agent stopped with it. Launch a new session, start the agent in the same folder, and ask it what state the project is in. With Claude Code you can also pick the earlier conversation from the list in **Claude Code terminal session**.

[Back to the quickstart](README.md)
