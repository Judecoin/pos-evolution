# Judecoin Service Node Recovery Using SN Private Key

## 【Description】

This guide describes the process for restoring a Judecoin Service Node using the original SN private key.

This guide applies to situations where the original server is lost, reinstalled, damaged, migrated, or no longer available, but the original Service Node private key is still available.

It is intended to help Judecoin Service Node operators restore the original node identity on a new server more clearly, safely, and consistently.

## 【Important Notice】

The CLI version used in this example is v3.2.0. This is only for the current version reference.

If Judecoin releases a newer CLI version in the future, please always follow the latest version provided by the community website or GitHub, and update the download link, extracted folder name, and version number accordingly.

Restoring a Service Node requires the original SN private key.

Do not disclose the SN private key. Do not send it to anyone. Do not post it in any group chat. Do not take screenshots or screen recordings when entering the private key.

## 【Recovery Principle】

A Judecoin Service Node has its own node identity private key.

If the original server is lost or needs to be migrated, the original Service Node identity can be restored on a new server by restoring the original SN private key.

The core idea is:

Restore the original SN private key into a key file, place it at:

`/home/ubuntu/.bitjudecoin/key_ed25519`

Then restart the Service Node with the restored key.

## 【Judecoin Service Node Recovery Process】

### 1. Install Required Tools

Log in to the server terminal and run:

`sudo apt update`

`sudo apt install wget tar bzip2 curl -y`

### 2. Download Judecoin CLI

Run:

`wget https://github.com/Judecoin/judecoin/releases/download/v3.2.0/judecoin-linux-x64-v3.2.0.tar.bz2`

Note:

If a newer CLI version has been officially released, replace `v3.2.0` in the link above with the latest version number.

### 3. Extract the CLI File

Run:

`tar -jxvf judecoin-linux-x64-v3.2.0.tar.bz2`

### 4. Enter the Judecoin CLI Directory

Run:

`cd judecoin-x86_64-linux-gnu-v3.2.0`

### 5. Check the CLI Version

Run:

`./judecoind --version`

If it shows `v3.2.0`, the current CLI version is correct.

If the community version has been updated, please use the latest displayed version as the reference.

### 6. Stop the Old judecoind Process

Run:

`pkill judecoind`

Wait for 5 seconds:

`sleep 5`

Check whether there is still any `judecoind` process running:

`ps aux | grep judecoind`

If you only see the `grep judecoind` line, it usually means the old process has stopped.

### 7. Remove Any Temporary sn_key File

Run:

`rm -f sn_key`

This step avoids conflicts with any old temporary `sn_key` file in the current directory.

### 8. Restore the SN Private Key

Run:

`./judecoin-sn-keys restore sn_key`

The system will prompt you to enter the original Service Node private key.

Enter the original SN private key as prompted.

Important:

Make sure your environment is safe when entering the private key. Do not take screenshots, do not record the screen, and do not allow anyone else to see it.

### 9. Create the Judecoin Data Directory

Run:

`sudo mkdir -p /home/ubuntu/.bitjudecoin`

### 10. Copy the Restored sn_key to the Service Node Key Location

Run:

`sudo cp sn_key /home/ubuntu/.bitjudecoin/key_ed25519`

### 11. Set Directory and File Permissions

Run:

`sudo chown -R ubuntu:ubuntu /home/ubuntu/.bitjudecoin`

`chmod 700 /home/ubuntu/.bitjudecoin`

`chmod 600 /home/ubuntu/.bitjudecoin/key_ed25519`

### 12. Restart the Service Node

Run:

`./judecoind --service-node --service-node-public-ip $(curl -s ifconfig.me) --no-zmq --detach`

### 13. Wait for Node Initialization

Run:

`sleep 30`

### 14. Check Node Status

Run:

`./judecoind status`

If you can see block height, synchronization status, and network connection information, the node has started successfully.

If the node is still syncing, wait until synchronization is completed.

A recovered Service Node may first show:

`not registered`

while the node is still syncing.

After synchronization is close to completion, the Service Node status should become:

`active, proof: never`

After the node submits a new uptime proof, the status should become similar to:

`active, proof: x minutes ago`

## 【Full Command Reference】

The following is the full command sequence for reference:

`sudo apt update`

`sudo apt install wget tar bzip2 curl -y`

`wget https://github.com/Judecoin/judecoin/releases/download/v3.2.0/judecoin-linux-x64-v3.2.0.tar.bz2`

`tar -jxvf judecoin-linux-x64-v3.2.0.tar.bz2`

`cd judecoin-x86_64-linux-gnu-v3.2.0`

`./judecoind --version`

`pkill judecoind`

`sleep 5`

`ps aux | grep judecoind`

`rm -f sn_key`

`./judecoin-sn-keys restore sn_key`

`sudo mkdir -p /home/ubuntu/.bitjudecoin`

`sudo cp sn_key /home/ubuntu/.bitjudecoin/key_ed25519`

`sudo chown -R ubuntu:ubuntu /home/ubuntu/.bitjudecoin`

`chmod 700 /home/ubuntu/.bitjudecoin`

`chmod 600 /home/ubuntu/.bitjudecoin/key_ed25519`

`./judecoind --service-node --service-node-public-ip $(curl -s ifconfig.me) --no-zmq --detach`

`sleep 30`

`./judecoind status`

`ps aux | grep judecoind`

## 【Common Notes】

1. Restoring a node is not the same as registering a new node.

The purpose of this process is to allow a new server to continue using the original Service Node identity.

2. The original SN private key must be used.

If a new SN private key is used, the blockchain will treat it as a different node identity and it may not match the original Service Node.

3. Do not run the same SN private key on multiple servers at the same time.

Before starting the recovered node on a new server, stop the old `judecoind` process on the original server.

4. Do not delete the `key_ed25519` file.

The `key_ed25519` file is the node identity file and is required for the Service Node to operate with the restored identity.

5. Do not disclose the SN private key.

Anyone who obtains the SN private key may affect the security of the node identity.

6. If the node has already been fully deregistered on-chain and entered the release period, restoring the server may not reactivate the original node.

In that case, the locked stake may need to wait for the release period to end, depending on the on-chain state.

7. If `./judecoind status` does not show status immediately, the node may have just started and may not be fully initialized yet. Wait 1-2 minutes and check again.

## 【Security Reminders】

Please pay attention to the following:

- Do not disclose the Service Node private key;
- Do not disclose wallet seed phrases;
- Do not disclose wallet private keys;
- Do not disclose `.pem` files or other server access keys;
- Do not expose server IP addresses, login information, or backend screenshots;
- Do not send the SN private key through chat apps, emails, or public groups;
- Store SN private keys and server access files in secure encrypted storage;
- Keep at least two offline backups in separate safe locations.

## 【Conclusion】

This guide provides a recovery process for restoring a Judecoin Service Node when the original SN private key is still available.

Clear recovery procedures can help operators reduce operational mistakes, restore the original node identity on a new server, and support the long-term stability of the Judecoin PoS Service Node network.
