# Getting your files onto the cluster

If your project is already in your cluster home folder, skip this page.

Your cluster home folder is separate from your laptop. Pick the way that matches where your files are now.

## Tell Git who you are (once)

Git records a name and email address with every commit, and it stops with an error at your first commit if they are not set. In VS Code the message is **Make sure you configure your "user.name" and "user.email" in git.** Set them once, in any terminal; they are kept for every session:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the email address of your GitHub account, so GitHub links the commits to you.

## Files on your laptop: upload them

In JupyterLab, open the file browser (the folder icon at the top of the left bar), go to the folder you want, and click the upload button (the arrow pointing up) above the file list. Choose your files. To upload a whole project, zip it on your laptop first, upload the zip, and unzip it in a terminal ([how to open one](jupyter.md#open-a-terminal)). If you uploaded `my-project.zip` to your home folder:

```bash
cd ~
unzip my-project.zip
```

## A public Git repository: clone it

A public repository can be downloaded with its HTTPS address, from any terminal (JupyterLab, VS Code or Academic Shell):

```bash
cd ~
git clone https://github.com/OWNER/REPOSITORY.git
```

This works without signing in. Pushing changes back needs a sign-in. In VS Code, the Source Control panel signs you in for you; see [Committing and pushing in VS Code](#committing-and-pushing-in-vs-code). Anywhere else, set up an SSH key (next section), then point your HTTPS clone at the SSH address, from inside the repository folder:

```bash
cd ~/REPOSITORY
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
```

## A private repository, or pushing changes: an SSH key

An **SSH key** is a pair of files that lets GitHub recognize your cluster account. The **private key** stays on the cluster and must never be shared or copied anywhere. The **public key** is the half you give to GitHub.

Do these steps in a **JupyterLab terminal** or in **Academic Shell Access**. The VS Code session does not have the `ssh` program, so Git over SSH fails there with `cannot run ssh: No such file or directory`.

Make a new key in a dedicated folder. The browser sessions replace the usual key folder, `~/.ssh`, with a fresh empty one each time, so a key stored there would not be found in your next session; `~/.config/git-key` is kept.

```bash
mkdir -p ~/.config/git-key
chmod 700 ~/.config/git-key
ssh-keygen -t ed25519 -f ~/.config/git-key/id_ed25519
```

`ssh-keygen` asks for a passphrase, a password that protects the key; you can press **Enter** twice for none. If it instead says the file already exists and asks **Overwrite (y/n)?**, answer **n**: you made a key earlier, and overwriting it would disconnect it from GitHub. Use the key you have and continue below.

Print the public key and copy the whole line it shows:

```bash
cat ~/.config/git-key/id_ed25519.pub
```

On GitHub, open **Settings** from your profile picture's menu, choose **SSH and GPG keys** in the left column, and click **New SSH key**. Paste the line into the **Key** box and click **Add SSH key**. Only ever paste the file ending in `.pub`.

Tell Git to use this key. You only do this once; it is remembered for every session:

```bash
git config --global core.sshCommand "ssh -i $HOME/.config/git-key/id_ed25519"
```

Now clone with the repository's SSH address (it starts with `git@github.com:`):

```bash
cd ~
git clone git@github.com:OWNER/REPOSITORY.git
```

The first time, Git asks whether to trust GitHub's host key. Check the fingerprint it shows against [GitHub's published fingerprints](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints) and answer **yes** if they match.

## Committing and pushing in VS Code

VS Code cannot use an SSH key, but its **Source Control** panel (the icon of three connected circles in the left bar) can commit and push over HTTPS, with its own GitHub sign-in.

1. Open your project folder in VS Code and click the Source Control icon.
2. If the folder is not a Git repository yet, click **Initialize Repository**.
3. Type a short message in the **Message** box and click **Commit**. If VS Code asks whether to stage all your changes, click **Yes**.
4. Click **Publish Branch** (for a folder that is not on GitHub yet) or **Sync Changes** (for one that is). The first time in each session, VS Code shows **The extension 'GitHub' wants to sign in using GitHub**. Click **Allow** and follow the steps on the GitHub page that opens in your browser, then come back to VS Code.
5. **Publish Branch** then asks whether to make a private or a public repository on your GitHub account. Choose **private** for course work.

After that sign-in, `git push` typed in VS Code's own terminal works too, because VS Code passes the sign-in to Git.

The sign-in lasts only for the current session. In a new session, the first push asks you to sign in to GitHub again. If you click **Cancel** instead, VS Code asks for a username, and the push ends with `remote: Repository not found.` and `fatal: Authentication failed` even though the repository exists. Push again and click **Allow**.

If files were changed outside VS Code and the panel does not list them, click the circular-arrow refresh button at the top of the panel.

You can also ask the agent to walk you through these steps. Never paste a private key, a password or a token into the agent's chat.

[Back to the quickstart](README.md)
