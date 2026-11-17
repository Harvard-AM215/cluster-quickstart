# Getting your files onto the cluster

If your project is already in your cluster home folder, skip this page.

Your cluster home folder is separate from your laptop. Pick the way that matches where your files are now.

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

This works without signing in. Pushing changes back needs a sign-in. The next section sets up an SSH key; after that, point your HTTPS clone at the SSH address, from inside the repository folder:

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

You can also ask the agent to walk you through these steps. Never paste a private key, a password or a token into the agent's chat.

[Back to the quickstart](README.md)
