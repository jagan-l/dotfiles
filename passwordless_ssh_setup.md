# SSH Logins (Passwordless Setup)
connect to remote servers without typing your password every time.

---

## Generate an SSH Key (if you don’t already have one)

Run this on your **Ubuntu local machine** (not the remote servers):

```bash
ls ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub 2>/dev/null || \
ssh-keygen -t ed25519 -C "$USER@$(hostname)"
```

Just hit **Enter** through the prompts; no need to set a passphrase if you truly want passwordless access.

---

##  Copy Your Public Key to Each Server

Replace with your server username and IPs:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub ubuntu@203.0.113.10
ssh-copy-id -i ~/.ssh/id_ed25519.pub ubuntu@198.51.100.25
```

This will:

- Ask for the password **once**
- Add your public key to `~/.ssh/authorized_keys` on the server

After that, passwordless SSH is ready.

If `ssh-copy-id` isn’t installed:

```bash
sudo apt install ssh-copy-id -y
```

---

## Confirm It Works

```bash
ssh ubuntu@203.0.113.10
```

You should connect **without being prompted for a password**.

---

## Add Shortcuts for Easy Access

Edit your `~/.ssh/config` file:

```bash
nano ~/.ssh/config
```

Example configuration:

```
Host prod
  HostName 203.0.113.10
  User ubuntu
  IdentityFile ~/.ssh/id_ed25519

Host dev
  HostName 198.51.100.25
  User ubuntu
  IdentityFile ~/.ssh/id_ed25519
```

Now you can simply run:

```bash
ssh prod
```

…and it will connect instantly without typing a username, IP, or password.

---

### Tip: Keep It Simple

Once configured, you can use the same setup for SCP, Rsync, and other tools — e.g.:

```bash
scp localfile.txt prod:/home/ubuntu/
rsync -avz ./project/ dev:/var/www/html/
```

---

