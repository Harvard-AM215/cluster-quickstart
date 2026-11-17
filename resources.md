# How many hours and CPUs to ask for

When you launch a session you choose two numbers. Both apps (JupyterLab and VS Code) use the same form.

- **Number of hours**, from 1 to 8. The session stops when this time runs out, and anything still running in it stops too. Your saved files are kept.
- **Number of CPUs**, from 1 to 4. These processors are held for you for the whole session, whether you use them or not.

You do not choose memory. The sessions we started had 4 GB, with either 1 or 2 CPUs.

**For a first session, keep the defaults: 4 hours and 2 CPUs.** That is enough to run the agent and ordinary course code. Ask for more CPUs only when your code runs several calculations at the same time, for example with a process pool; most simple scripts use only one CPU however many you reserve.

The agent runs inside your session. It shares your CPUs and memory with everything else you run there, and it cannot reach more than the session has.

When you finish early, cancel the session ([step 5 of the quickstart](README.md#5-stop-the-session-when-you-finish)), so the CPUs go back to other students.

If your session stays in **Starting** for a long time, the cluster may be busy; asking for fewer CPUs may help it start sooner. See [Troubleshooting](troubleshooting.md#starting-a-session).

[Back to the quickstart](README.md)
