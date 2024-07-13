


By following these steps, you should be able to set up MPI on two virtual machines and run your MPI programs across them.

You: 

ssh-copy-id mpiuser@<IP_OF_OTHER_VM>
/user/bin/ssh-copy-id:ERROR: no identities found

ChatGPT: 

The error `no identities found` indicates that the SSH agent doesn't have any keys loaded. This typically happens if the SSH keys were not generated or added to the SSH agent correctly. Here’s how to resolve this issue:
### Step-by-Step Solution 

#### Step 1: Generate SSH Key Pair 

First, ensure you have an SSH key pair. If not, generate one:


```sh
ssh-keygen -t rsa
```
Press `Enter` to accept the default location and file name. When prompted, you can enter a passphrase or leave it empty for no passphrase.
#### Step 2: Start the SSH Agent 

Start the SSH agent and add the key:


```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```
If your SSH key is in a different location or has a different name, replace `~/.ssh/id_rsa` with the correct path.
#### Step 3: Copy the SSH Key to the Other VM 

Now, copy the SSH key to the other VM:


```sh
ssh-copy-id mpiuser@<IP_OF_OTHER_VM>
```
Replace `<IP_OF_OTHER_VM>` with the actual IP address of the other VM.
#### Step 4: Verify Passwordless SSH 

Test the SSH connection to ensure it works without a password:


```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```

### Detailed Steps Recap 
 
1. **Generate SSH Key Pair** :

```sh
ssh-keygen -t rsa
```
Follow the prompts and press `Enter` to accept the default file location.
 
2. **Start SSH Agent and Add Key** :

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```
 
3. **Copy SSH Key to Other VM** :

```sh
ssh-copy-id mpiuser@<IP_OF_OTHER_VM>
```
 
4. **Test Passwordless SSH** :

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```

### Example 

Here's an example with specific commands:
 
1. **Generate SSH Key Pair** :

```sh
ssh-keygen -t rsa
```
Follow the prompts and press `Enter`.
 
2. **Start SSH Agent and Add Key** :

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```
 
3. **Copy SSH Key to Other VM** :

```sh
ssh-copy-id mpiuser@192.168.1.2
```
 
4. **Test Passwordless SSH** :

```sh
ssh mpiuser@192.168.1.2
```

If you follow these steps, you should be able to set up passwordless SSH access between your VMs successfully.

You: 

ssh-add ~/.ssh/id_rsa
colud not open connection to your authentication agent

ChatGPT: 

The error `could not open connection to your authentication agent` typically means that the SSH agent is not running or not correctly started. Here’s how to ensure it is running and properly configured:
### Step-by-Step Solution 

#### Step 1: Start the SSH Agent 

Ensure the SSH agent is running:


```sh
eval "$(ssh-agent -s)"
```

This command starts the SSH agent and sets up the environment variables for the current session.

#### Step 2: Add the SSH Key 

Add your SSH key to the agent:


```sh
ssh-add ~/.ssh/id_rsa
```
If your SSH key is in a different location or has a different name, replace `~/.ssh/id_rsa` with the correct path.
### Troubleshooting 

If you still encounter issues, here are additional steps you can take:

#### Restart the SSH Agent 

Sometimes, restarting the SSH agent can resolve the issue:


```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

#### Verify the Key Exists 

Ensure that the SSH key exists at the specified location:


```sh
ls -l ~/.ssh/id_rsa
```

If the key is not present, you need to generate it:


```sh
ssh-keygen -t rsa
```
Follow the prompts and press `Enter` to accept the default file location.
#### Check Permissions 

Ensure the SSH key has the correct permissions:


```sh
chmod 600 ~/.ssh/id_rsa
chmod 700 ~/.ssh
```

### Example 

Here’s a full example with specific commands:
 
1. **Start the SSH Agent** :

```sh
eval "$(ssh-agent -s)"
```
 
2. **Add the SSH Key** :

```sh
ssh-add ~/.ssh/id_rsa
```
 
3. **Generate SSH Key (if not present)** :

```sh
ssh-keygen -t rsa
```
 
4. **Check Permissions** :

```sh
chmod 600 ~/.ssh/id_rsa
chmod 700 ~/.ssh
```
 
5. **Copy SSH Key to Other VM** :

```sh
ssh-copy-id mpiuser@<IP_OF_OTHER_VM>
```
 
6. **Test Passwordless SSH** :

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```

### Additional Tips 
 
- If you are using a terminal multiplexer like `tmux` or `screen`, make sure you start the SSH agent inside the session.
 
- If the SSH agent is already running and you start a new terminal, you might need to source the environment variables from the existing agent. This can be done with the following command:

```sh
source ~/.ssh-agent-thing
```

Following these steps should help you successfully set up the SSH agent and add your key for passwordless SSH access between your VMs.

You: 

how to do this If you are using a terminal multiplexer like tmux or screen, make sure you start the SSH agent inside the session.
If the SSH agent is already running and you start a new terminal, you might need to source the environment variables from the existing agent. This can be done with the following command:
sh
Copy code
source ~/.ssh-agent-thing

ChatGPT: 

When using a terminal multiplexer like `tmux` or `screen`, you need to ensure the SSH agent is properly started within the session, and its environment variables are correctly set. Here’s how to do it:Using `tmux` or `screen`Step 1: Start `tmux` or `screen` Session 
1. **Start `tmux`** :

```sh
tmux new-session -s mysession
```
or ****Start `tmux`** :

```sh
tmux new-session -s mysession
```
or start `screen`** :

```sh
screen -S mysession
```

#### Step 2: Start the SSH Agent Inside the Session 
 
1. **Start the SSH agent**  inside the `tmux` or `screen` session:

```sh
eval "$(ssh-agent -s)"
```

#### Step 3: Add Your SSH Key 
 
1. **Add your SSH key** :

```sh
ssh-add ~/.ssh/id_rsa
```

#### Step 4: Save SSH Agent Variables 
 
1. **Save the SSH agent environment variables**  to a file. This allows new terminals to source these variables and connect to the running SSH agent:

```sh
echo "export SSH_AUTH_SOCK=${SSH_AUTH_SOCK}" > ~/.ssh-agent-thing
echo "export SSH_AGENT_PID=${SSH_AGENT_PID}" >> ~/.ssh-agent-thing
```

#### Step 5: Source the Variables in New Terminals 
 
1. **Source the environment variables**  in new terminal sessions:

```sh
source ~/.ssh-agent-thing
```

### Putting It All Together 

Here’s a complete example of the process:
 
1. **Start a `tmux` or `screen` session** :

```sh
tmux new-session -s mysession
```

or


```sh
screen -S mysession
```
 
2. **Start the SSH agent inside the session** :

```sh
eval "$(ssh-agent -s)"
```
 
3. **Add your SSH key** :

```sh
ssh-add ~/.ssh/id_rsa
```
 
4. **Save the SSH agent environment variables** :

```sh
echo "export SSH_AUTH_SOCK=${SSH_AUTH_SOCK}" > ~/.ssh-agent-thing
echo "export SSH_AGENT_PID=${SSH_AGENT_PID}" >> ~/.ssh-agent-thing
```
 
5. **In new terminal sessions** , source the environment variables:

```sh
source ~/.ssh-agent-thing
```

### Example Workflow 
Inside `tmux` or `screen`:

```sh
tmux new-session -s mysession
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
echo "export SSH_AUTH_SOCK=${SSH_AUTH_SOCK}" > ~/.ssh-agent-thing
echo "export SSH_AGENT_PID=${SSH_AGENT_PID}" >> ~/.ssh-agent-thing
```

#### In a new terminal: 


```sh
source ~/.ssh-agent-thing
```
By following these steps, you ensure that the SSH agent is running within your `tmux` or `screen` session, and you can access it from new terminal sessions by sourcing the saved environment variables.

You: 

eval `ssh-agent`
ssh-add ~/.ssh/id_rsa
"output how to check it is properly don or not"

ChatGPT: 

To check if the SSH agent is running correctly and if the key has been added properly, you can follow these steps:

### Step 1: Verify SSH Agent is Running 

Run the following command to verify that the SSH agent is running and the environment variables are set correctly:


```sh
echo $SSH_AGENT_PID
```

If the SSH agent is running, this command should output a process ID (a number). If it's empty, the SSH agent is not running.

### Step 2: List Added SSH Keys 

To verify that the SSH key has been added to the agent, use:


```sh
ssh-add -l
```

This command lists the fingerprints of all the keys currently managed by the SSH agent. If your key is listed, it means the key has been added correctly.

### Step 3: Test Passwordless SSH 

Finally, test if you can SSH into the other machine without being prompted for a password:


```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```
Replace `<IP_OF_OTHER_VM>` with the actual IP address of the other VM. If everything is set up correctly, you should be logged in without needing to enter a password.
### Example Workflow 
 
1. **Start the SSH agent and add the key** :

```sh
eval `ssh-agent`
ssh-add ~/.ssh/id_rsa
```
 
2. **Verify the SSH agent is running** :

```sh
echo $SSH_AGENT_PID
```
Expected output: A process ID (e.g., `12345`).
 
3. **List added SSH keys** :

```sh
ssh-add -l
```
Expected output: The fingerprint of your SSH key (e.g., `2048 SHA256:... /home/mpiuser/.ssh/id_rsa (RSA)`).
 
4. **Test passwordless SSH** :

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```

Expected outcome: You should log in without being prompted for a password.

### Troubleshooting 
 
- **If `echo $SSH_AGENT_PID` is empty** : 
  - Make sure you have started the SSH agent with `eval \`ssh-agent``.
 
- **If `ssh-add -l` shows "The agent has no identities"** : 
  - Ensure you have added the correct key with `ssh-add ~/.ssh/id_rsa`.
 
  - Check the permissions of your SSH key (`chmod 600 ~/.ssh/id_rsa`).
 
- **If you are prompted for a password when SSHing** : 
  - Ensure the SSH key was copied to the other VM with `ssh-copy-id mpiuser@<IP_OF_OTHER_VM>`.
 
  - Verify that the SSH key is listed in the `~/.ssh/authorized_keys` file on the other VM.

By following these steps, you can confirm that the SSH agent is running correctly, the key is added, and passwordless SSH is working.

You: 

i need to enter pasword who to chek it is correctly done or not

ChatGPT: 

If you still need to enter a password when attempting to SSH into the other VM, you should check a few things to ensure the setup was done correctly:

### Step 1: Verify SSH Agent and Key 
 
1. **Start the SSH agent and add the key**  (if not already done):

```sh
eval `ssh-agent`
ssh-add ~/.ssh/id_rsa
```
 
2. **Verify the SSH agent is running** :

```sh
echo $SSH_AGENT_PID
```
Expected output: A process ID (e.g., `12345`). If it is empty, the SSH agent is not running.
 
3. **List added SSH keys** :

```sh
ssh-add -l
```
Expected output: The fingerprint of your SSH key (e.g., `2048 SHA256:... /home/mpiuser/.ssh/id_rsa (RSA)`). If the list is empty, the key was not added correctly.

### Step 2: Verify Key on the Other VM 
 
1. **Check if the SSH key is copied to the other VM** :

```sh
ssh mpiuser@<IP_OF_OTHER_VM> 'cat ~/.ssh/authorized_keys'
```
Replace `<IP_OF_OTHER_VM>` with the actual IP address of the other VM. The output should contain the contents of your `id_rsa.pub` file.
 
2. **If the key is not present** : 
  - Copy the SSH key again:

```sh
ssh-copy-id mpiuser@<IP_OF_OTHER_VM>
```

### Step 3: Check Permissions on the Other VM 
 
1. **Ensure the permissions are correct**  on the `.ssh` directory and `authorized_keys` file on the other VM:

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Step 4: Test Passwordless SSH Again 
 
1. **Attempt to SSH into the other VM** :

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```
You should be able to log in without being prompted for a password.

### Example Workflow 
 
1. **On your local machine** :

```sh
eval `ssh-agent`
ssh-add ~/.ssh/id_rsa
ssh-add -l
```
 
2. **Verify the key is copied**  to the other VM:

```sh
ssh-copy-id mpiuser@<IP_OF_OTHER_VM>
```
 
3. **Check permissions**  on the other VM:

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
 
4. **Test passwordless SSH** :

```sh
ssh mpiuser@<IP_OF_OTHER_VM>
```

### Common Issues and Solutions 
 
- **Incorrect Permissions** : Ensure the `.ssh` directory and `authorized_keys` file have the correct permissions (`700` for `.ssh` and `600` for `authorized_keys`).
 
- **SSH Key Not Added to Agent** : Verify the key is added to the agent with `ssh-add -l`.
 
- **Key Not in `authorized_keys`** : Ensure the public key is correctly copied to the `authorized_keys` file on the other VM.

By following these steps, you can confirm that everything is set up correctly and resolve any issues preventing passwordless SSH.

You: 

what is Setting up NFS

ChatGPT: 

Setting up NFS (Network File System) allows you to share directories and files over a network, enabling multiple machines to access and modify the same data as if they were on the local filesystem. Here's a step-by-step guide to setting up NFS between two virtual machines.

### Step-by-Step Guide to Setting Up NFS 

### Step 1: Install NFS Packages 
**On the NFS Server (Manager Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-kernel-server
```
**On the NFS Client (Worker Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-common
```

### Step 2: Configure the NFS Server 
**1. Create a directory to share:** 

```sh
mkdir -p /home/mpiuser/cloud
```
**
Setting up NFS (Network File System) allows you to share directories and files over a network, enabling multiple machines to access and modify the same data as if they were on the local filesystem. Here's a step-by-step guide to setting up NFS between two virtual machines.

### Step-by-Step Guide to Setting Up NFS 

### Step 1: Install NFS Packages 
**On the NFS Server (Manager Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-kernel-server
```
**On the NFS Client (Worker Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-common
```

### Step 2: Configure the NFS Server 
**1. Create a directory to share:** 

```sh
mkdir -p /home/mpiuser/cloud
```
2. Edit the `/etc/exports` file to share the directory:** 

```sh
sudo nano /etc/exports
```

Add the following line:


```sh
/home/mpiuser/cloud *(rw,sync,no_root_squash,no_subtree_check)
```

This configuration means:
 
- `rw`: Read and write permissions.
 
- `sync`: Changes are written to disk immediately.
 
- `no_root_squash`: Root on the client has the same privileges as root on the server.
 
- `no_subtree_check`: Disables subtree checking for speed.
**3. Export the shared directory:** 

```sh
sudo exportfs -a
```
**4. Start the NFS server:** 

```sh
sudo systemctl restart nfs-kernel-server
```

### Step 3: Configure the NFS Client 
**1. Create a directory to mount the shared directory:** 

```sh
mkdir -p /home/mpiuser/cloud
```
**2. Mount the NFS share:** 

```sh
sudo mount <NFS_SERVER_IP>:/home/mpiuser/cloud /home/mpiuser/cloud
```
Replace `<NFS_SERVER_IP>` with the IP address of the NFS server.**3. Verify the mount:** 

```sh
df -h
```

You should see an entry for the NFS mount.

### Step 4: Make the 

### Step 4: Make the Mount Permanent 
To ensure the NFS mount persists across reboots, you need to add an entry to the `/etc/fstab` file on the client.**
Setting up NFS (Network File System) allows you to share directories and files over a network, enabling multiple machines to access and modify the same data as if they were on the local filesystem. Here's a step-by-step guide to setting up NFS between two virtual machines.

### Step-by-Step Guide to Setting Up NFS 

### Step 1: Install NFS Packages 
**On the NFS Server (Manager Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-kernel-server
```
**On the NFS Client (Worker Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-common
```

### Step 2: Configure the NFS Server 
**1. Create a directory to share:** 

```sh
mkdir -p /home/mpiuser/cloud
```
**
Setting up NFS (Network File System) allows you to share directories and files over a network, enabling multiple machines to access and modify the same data as if they were on the local filesystem. Here's a step-by-step guide to setting up NFS between two virtual machines.

### Step-by-Step Guide to Setting Up NFS 

### Step 1: Install NFS Packages 
**On the NFS Server (Manager Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-kernel-server
```
**On the NFS Client (Worker Node):** 

```sh
sudo apt-get update
sudo apt-get install nfs-common
```

### Step 2: Configure the NFS Server 
**1. Create a directory to share:** 

```sh
mkdir -p /home/mpiuser/cloud
```
2. Edit the `/etc/exports` file to share the directory:** 

```sh
sudo nano /etc/exports
```

Add the following line:


```sh
/home/mpiuser/cloud *(rw,sync,no_root_squash,no_subtree_check)
```

This configuration means:
 
- `rw`: Read and write permissions.
 
- `sync`: Changes are written to disk immediately.
 
- `no_root_squash`: Root on the client has the same privileges as root on the server.
 
- `no_subtree_check`: Disables subtree checking for speed.
**3. Export the shared directory:** 

```sh
sudo exportfs -a
```
**4. Start the NFS server:** 

```sh
sudo systemctl restart nfs-kernel-server
```

### Step 3: Configure the NFS Client 
**1. Create a directory to mount the shared directory:** 

```sh
mkdir -p /home/mpiuser/cloud
```
**2. Mount the NFS share:** 

```sh
sudo mount <NFS_SERVER_IP>:/home/mpiuser/cloud /home/mpiuser/cloud
```
Replace `<NFS_SERVER_IP>` with the IP address of the NFS server.**3. Verify the mount:** 

```sh
df -h
```

You should see an entry for the NFS mount.

### Step 4: Make the 

### Step 4: Make the Mount Permanent 
To ensure the NFS mount persists across reboots, you need to add an entry to the `/etc/fstab` file on the client.1. Edit the `/etc/fstab` file:** 

```sh
sudo nano /etc/fstab
```
**2. Add the following line to the file:** 

```sh
<NFS_SERVER_IP>:/home/mpiuser/cloud /home/mpiuser/cloud nfs defaults 0 0
```
Replace `<NFS_SERVER_IP>` with the IP address of the NFS server.
### Example 

Here’s an example of setting up NFS between two virtual machines:

#### On the NFS Server (Manager Node) 
 
1. **Install NFS server package:** 

```sh
sudo apt-get update
sudo apt-get install nfs-kernel-server
```
 
2. **Create a shared directory:** 

```sh
mkdir -p /home/mpiuser/cloud
```
 
3. **Edit `/etc/exports` file:** 

```sh
sudo nano /etc/exports
```

Add the following line:


```sh
/home/mpiuser/cloud *(rw,sync,no_root_squash,no_subtree_check)
```
 
4. **Export the shared directory:** 

```sh
sudo exportfs -a
```
 
5. **Restart the NFS server:** 

```sh
sudo systemctl restart nfs-kernel-server
```

#### On the NFS Client (Worker Node) 
 
1. **Install NFS client package:** 

```sh
sudo apt-get update
sudo apt-get install nfs-common
```
 
2. **Create a mount directory:** 

```sh
mkdir -p /home/mpiuser/cloud
```
 
3. **Mount the NFS share:** 

```sh
sudo mount <NFS_SERVER_IP>:/home/mpiuser/cloud /home/mpiuser/cloud
```
 
4. **Verify the mount:** 

```sh
df -h
```

You should see an entry for the NFS mount.
 
5. **Make the mount permanent:** 

```sh
sudo nano /etc/fstab
```

Add the following line:


```sh
<NFS_SERVER_IP>:/home/mpiuser/cloud /home/mpiuser/cloud nfs defaults 0 0
```

### Summary 

By following these steps, you set up NFS to share a directory from the manager node (NFS server) and mount it on the worker node (NFS client). This setup allows you to share data between machines over the network, which is especially useful for cluster computing environments like those using MPI (Message Passing Interface).

You: 

mpiuser is not in sudoers file

ChatGPT: 

To add `mpiuser` to the `sudoers` file so that they can use `sudo` commands, you will need to temporarily use a user with sudo privileges. Here’s how you can do it:
### Step 1: Log in as a User with Sudo Privileges 

Log in to your system as a user who already has sudo privileges. For example, this could be the default user created during the installation of the operating system.
Step 2: Add `mpiuser` to the `sudoers` File 
1. **Open the `sudoers` file for editing:** 

```sh
sudo visudo
```
The `visudo` command safely edits the `sudoers` file, checking for syntax errors before saving.
 
2. **Add the following line:** 

```sh
mpiuser ALL=(ALL:ALL) ALL
```
This line gives `mpiuser` sudo privileges.
 
3. **Save and exit:**  
  - If using `nano` as the editor (default for `visudo` on some systems), press `Ctrl+X`, then `Y`, then `Enter`.
 
  - If using `vi` or `vim`, press `Esc`, type `:wq`, and press `Enter`.

### Step-by-Step Example 
 
1. **Log in as a user with sudo privileges**  (e.g., `yourusername`):

```sh
ssh yourusername@<IP_ADDRESS>
```
 
2. **Add `mpiuser` to the `sudoers` file:** 

```sh
sudo visudo
```

Add the following line:


```sh
mpiuser ALL=(ALL:ALL) ALL
```
 
3. **Save and exit the editor** .
Alternative: Add `mpiuser` to the `sudo` GroupAnother way to give `mpiuser` sudo privileges is to add them to the `sudo` group (on Debian-based systems) or the `wheel` group (on Red Hat-based systems). 
1. **Log in as a user with sudo privileges** .
 
2. **Add `mpiuser` to the `sudo` group** :

```sh
sudo usermod -aG sudo mpiuser
```
 
3. **Log out and log back in as `mpiuser`**  to apply the changes:

```sh
su - mpiuser
```

### Example 
 
1. **Log in as a user with sudo privileges**  (e.g., `yourusername`):

```sh
ssh yourusername@<IP_ADDRESS>
```
 
2. **Add `mpiuser` to the `sudo` group** :

```sh
sudo usermod -aG sudo mpiuser
```
 
3. **Log out and log back in as `mpiuser`** :

```sh
su - mpiuser
```
By following these steps, `mpiuser` should now have sudo privileges, allowing them to perform administrative tasks on the system.

You: 

copy file using ssh from another machine

ChatGPT: 

To copy files from one machine to another using SSH, you can use the `scp` (secure copy) command. Here’s a guide on how to do this.Syntax of `scp`

```sh
scp [options] source_file user@hostname:destination_path
```

### Copy a File from Local Machine to Remote Machine 
**1. Copy a file from the local machine to the remote machine:** 

```sh
scp /path/to/local/file mpiuser@remote_host:/path/to/remote/directory
```
**Example:** 

```sh
scp /home/mpiuser/localfile.txt mpiuser@192.168.1.100:/home/mpiuser/
```

### Copy a File from Remote Machine to Local Machine 
**2. Copy a file from the remote machine to the local machine:** 

```sh
scp mpiuser@remote_host:/path/to/remote/file /path/to/local/directory
```
**Example:** 

```sh
scp mpiuser@192.168.1.100:/home/mpiuser/remotefile.txt /home/mpiuser/
```

### Copy a Directory Recursively 
To copy directories, use the `-r` (recursive) option.**1. Copy a directory from the local machine to the remote machine:** 

```sh
scp -r /path/to/local/directory mpiuser@remote_host:/path/to/remote/directory
```
**Example:** 

```sh
scp -r /home/mpiuser/localdir mpiuser@192.168.1.100:/home/mpiuser/
```
**2. Copy a directory from the remote machine to the local machine:** 

```sh
scp -r mpiuser@remote_host:/path/to/remote/directory /path/to/local/directory
```
**Example:** 

```sh
scp -r mpiuser@192.168.1.100:/home/mpiuser/remotedir /home/mpiuser/
```
Additional `scp` Options 
- `-P port`: Specify a port number to connect to on the remote host.
 
- `-i identity_file`: Select the file from which the identity (private key) for public key authentication is read.
 
- `-C`: Enable compression.
**Example Using Port and Identity File:** 

```sh
scp -P 2222 -i ~/.ssh/id_rsa /path/to/local/file mpiuser@192.168.1.100:/path/to/remote/directory
```

### Example Workflow 
 
1. **Copy a file from local to remote:** 

```sh
scp /home/mpiuser/file.txt mpiuser@192.168.1.100:/home/mpiuser/
```
 
2. **Copy a file from remote to local:** 

```sh
scp mpiuser@192.168.1.100:/home/mpiuser/file.txt /home/mpiuser/
```
 
3. **Copy a directory from local to remote:** 

```sh
scp -r /home/mpiuser/localdir mpiuser@192.168.1.100:/home/mpiuser/
```
 
4. **Copy a directory from remote to local:** 

```sh
scp -r mpiuser@192.168.1.100:/home/mpiuser/remotedir /home/mpiuser/
```

By following these steps, you can securely copy files and directories between machines using SSH.
