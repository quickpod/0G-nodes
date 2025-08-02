# 0G Storage Node
## 1. Getting Started
1. Log into the [QuickPod console](https://console.quickpod.io/), then set the search type to CPU and filter for 8X+ offers only.
   <img width="2153" height="1381" alt="image" src="https://github.com/user-attachments/assets/b2b7f588-4c39-4e19-8982-78d45f0d1eb7" />
3.  Find any machine with at least 500GB of storage, 32GB RAM, and 8 threads. Machines with more threads will have better performance, especially during initial compilation.
4.  Click "Create Pod", then use the **Ubuntu 22.04 VM** template. Make sure to set the storage between 500GB and 1TB.
  <img width="1406" height="1044" alt="image" src="https://github.com/user-attachments/assets/c9cc37b2-625e-44f0-a4e0-ce9371132159" />
5.  Navigate to the [Pods page](https://console.quickpod.io/pods) . The pod will take up to 5 minutes to intialize. Once the Connect button becomes enabled, click it.
6. Find the port forwarded to 5900, then click the link to open the VNC terminal. Once the terminal loads, click "Connect" to open the session.
   <img width="1391" height="451" alt="image" src="https://github.com/user-attachments/assets/382f8133-c03f-49ca-97a3-3870e896353a" />
7. The server may perform some setup tasks. Wait until you are prompted for a username and password.
   > The default username and password is "quickpod"/"abcd1234". If desired, these credentials may be changed by editing the template before creating the pod. 

## 2. Compiling the node
1. Type the following commands into the terminal to install the prerequisite libraries.
   ```
   sudo apt update
   sudo apt install -y clang cmake build-essential pkg-config libssl-dev protobuf-compiler
   ```
2. Navigate to [the 0G Labs GitHub Repo](https://github.com/0glabs/0g-storage-node), then find the latest release on the right side. Take note of the release number. As of writing, the number is `v1.1.0`.
   <img width="2794" height="1517" alt="image" src="https://github.com/user-attachments/assets/0ab75a46-f759-4f12-a085-e0adf8bfdc5e" />
3. Go back to the VNC terminal, then type the following command, replacing `<latest-tag>` with the current release.
   ```
   git clone -b <latest_tag> https://github.com/0glabs/0g-storage-node.git
   ```
4. Type the following code to compile the node software. This process will take a while.
   ```
    cd 0g-storage-node
    cargo build --release
   ```
## 3. Configuring your node
> [!NOTE]
> If you have a custom configuration file already on GitHub or elsewhere, use `curl` or `wget` to download it to the pod. The destination folder should be `$HOME/0g-storage-node/run/`
1. Navigate to the config file directory by typing `cd run`.
> [!NOTE]
> To edit files on the pod, use `vi` or `nano`. For example, `nano config.toml`
2. (Optional) To copy the default "Turbo" values, run the following command:
  ```
  mv config-testnet-turbo.toml config.toml
  ```
3. Edit your template configuration as desired.
## 4. Running your node
> [!IMPORTANT]
> Remember to replace your private key before running or the node will fail to start. If your toml file has a different name, also replace it.

Your node can be started by typing `cd $HOME/0g-storage-node/run && ../target/release/zgs_node --config config.toml --miner-key <your_private_key>`.

Your node should now connect and receive participation rewards. 
