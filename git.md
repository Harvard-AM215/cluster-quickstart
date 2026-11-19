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

This works without signing in. Pushing changes back, or cloning a private repository, needs a sign-in; the next section sets one up.

## A private repository, or pushing changes: an access token

The cluster blocks outgoing SSH connections, so Git over SSH (addresses that start with `git@github.com:`) fails with `ssh: connect to host github.com port 22: Connection timed out`. Use the HTTPS address with a **personal access token**, a password that GitHub makes for you and that works only for the repositories you choose.

In VS Code, the Source Control panel signs you in without a token; see [Committing and pushing in VS Code](#committing-and-pushing-in-vs-code). The steps below are for a JupyterLab terminal or Academic Shell Access.

Make the token on GitHub, in your laptop's browser:

1. Open **Settings** from your profile picture's menu, then **Developer settings** at the bottom of the left column.
2. Choose **Personal access tokens → Fine-grained tokens** and click **Generate new token**.
3. Give it a name such as `am115-cluster` and an expiration date after the end of the term.
4. Under **Repository access**, choose **Only select repositories** and pick your project repository.
5. Under **Permissions**, find **Contents** and set it to **Read and write**.
6. Click **Generate token** and copy the token it shows. GitHub shows it only once.

If your repository belongs to the course organization or to a teammate and does not appear in the list in step 4, ask the owner to add you as a collaborator first, or use a **classic** token with the `repo` scope instead.

Tell Git to remember the token, once, in a cluster terminal:

```bash
git config --global credential.helper store
```

Clone with the HTTPS address:

```bash
cd ~
git clone https://github.com/OWNER/REPOSITORY.git
```

Git asks for **Username**: type your GitHub username. It then asks for **Password**: paste the token and press **Enter**. Nothing appears while you paste; that is normal. Git saves the token in `~/.git-credentials`, so later pushes and pulls in any session do not ask again. Anyone who can read that file can use the token, so never share it, and delete the token on GitHub when the term ends.

A repository uploaded from your laptop keeps your laptop's remote address, and that address may be an SSH one. Check with `git remote -v` inside the folder; if the address starts with `git@`, switch it to HTTPS:

```bash
cd ~/REPOSITORY
git remote set-url origin https://github.com/OWNER/REPOSITORY.git
```

For a repository on code.harvard.edu, make the token the same way on code.harvard.edu and use its `https://code.harvard.edu/...` address.

If Git says `Authentication failed`, the token is wrong, expired or lacks access to that repository. Make a new one, then remove the saved copy with `rm ~/.git-credentials` and push again.

## Committing and pushing in VS Code

VS Code's **Source Control** panel (the icon of three connected circles in the left bar) can commit and push over HTTPS, with its own GitHub sign-in.

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
