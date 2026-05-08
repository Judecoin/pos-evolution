# Judecoin Service Node Security and Backup Checklist

## 【Description】

This guide provides a security and backup checklist for Judecoin Service Node operators.

The purpose of this guide is to help operators protect important files, private keys, wallet recovery information, server access files, and node identity keys.

It is intended to help Judecoin Service Node operators avoid common security mistakes and improve backup awareness.

## 【Why Security and Backup Are Important】

Running a Judecoin Service Node is not only about staking and starting a server.

A Service Node operator also needs to protect several important assets and files, including:

- Wallet seed phrase
- Wallet password
- Wallet files
- Service Node private key
- `.pem` files or other server access keys
- Server login information
- Node records
- CLI version and operation notes

If any of these are lost, leaked, or stored carelessly, the operator may face serious risks.

## 【1. Wallet Seed Phrase Backup】

The wallet seed phrase is one of the most important recovery tools.

Please follow these rules:

- Do not share the seed phrase with anyone
- Do not send the seed phrase through chat apps or email
- Do not store the seed phrase in plain text on an online computer
- Do not take screenshots of the seed phrase
- Do not upload the seed phrase to public cloud storage
- Do not paste the seed phrase into unknown websites or tools
- Keep at least one offline backup in a safe location

If the wallet seed phrase is lost, the wallet may not be recoverable.

If the wallet seed phrase is leaked, the wallet funds may be at risk.

## 【2. Wallet Password Backup】

The wallet password is also important.

Please remember:

- Use a strong password
- Do not use simple passwords
- Do not store the wallet password together with the seed phrase
- Do not send the wallet password to anyone
- Keep a secure offline backup if necessary

A good practice is to store the wallet seed phrase and wallet password separately.

## 【3. Service Node Private Key Backup】

The Service Node private key is used to identify the Service Node.

The key file is usually located at:

`/home/ubuntu/.bitjudecoin/key_ed25519`

This file is very important.

If the server is lost, damaged, reinstalled, or migrated, the Service Node private key may be needed to restore the original Service Node identity.

Please follow these rules:

- Do not share the Service Node private key
- Do not send it through chat apps or email
- Do not post it in public groups
- Do not upload it to public cloud storage
- Keep at least two offline backups
- Store backups in separate safe locations

## 【4. Server Access File Backup】

Server access files may be required to access and manage the server.

These may include `.pem` files, SSH keys, password records, or other server access credentials depending on the server provider and operating environment.

If server access files are lost, the operator may lose normal access to the server.

Please follow these rules:

- Do not share server access files with anyone
- Do not upload them to public storage
- Do not store them only on one computer
- Keep an encrypted offline backup
- Use clear file names to avoid confusion
- Store different server access files carefully when managing multiple nodes

Server access files should be treated as sensitive access files.

## 【5. Server Information Backup】

A Service Node operator should keep a basic record of server information.

Recommended records include:

- Server region
- Server provider
- Instance name
- Public IP address
- CLI version
- Service Node public key
- Wallet used for registration
- Registration date
- Current node status
- Notes about upgrades or restarts

Do not publish this full record publicly.

It is useful for private management and recovery.

## 【6. Recommended Backup Structure】

A safer backup structure may include:

1. Main encrypted USB drive

Used for daily backup of important files.

2. Offline backup encrypted USB drive

Stored separately and rarely connected to a computer.

3. Paper backup

Used for essential recovery information such as seed phrase.

4. Private node record file

Used to track node information, server region, and Service Node public key.

Important files should not exist in only one place.

## 【7. Hardware Encrypted USB Drive】

A hardware encrypted USB drive can be useful for storing sensitive files.

It may be used to store:

- Service Node private key backup
- Server access file backup
- Node record file
- Wallet recovery notes
- Important operation documents

Recommended practice:

- Use at least two encrypted USB drives
- Keep them in different safe locations
- Do not keep both backups in the same bag or same computer
- Test the USB drive before relying on it
- Keep the password safe
- Do not store the USB password together with the USB drive

## 【8. What Should Never Be Shared】

Never share the following information:

- Wallet seed phrase
- Wallet private key
- Wallet password
- View key
- Spend key
- Wallet files
- Service Node private key
- `.pem` files or other server access keys
- Server login credentials
- Verification codes
- Backend screenshots containing sensitive information

If anyone asks for these, treat it as a serious security risk.

## 【9. Email and Phishing Safety】

Be careful with emails or messages claiming to represent the project, community, or technical team.

Before responding, check:

- Is the sender using an official domain?
- Is the message asking for private keys or seed phrases?
- Is there a suspicious link?
- Is the message trying to create urgency?
- Can the identity be confirmed through official GitHub or official channels?

Never provide private keys, seed phrases, wallet files, or server access files through email.

A public receiving address may be safer than private information, but even wallet addresses should be shared carefully.

## 【10. GitHub and Contribution Safety】

When contributing to GitHub Discussions, Issues, Pull Requests, or documentation:

- Do not post wallet seed phrases
- Do not post Service Node private keys
- Do not post `.pem` files or other server access keys
- Do not post server login information
- Do not post full backend screenshots
- Remove personal information from screenshots before sharing
- Avoid exposing large holdings or node ownership details publicly

Contribution should be helpful, but it should not expose private operational information.

## 【11. Before Server Migration or Recovery】

Before migrating or restoring a node, check that you have:

- Service Node private key backup
- Server access file or new server access
- CLI version information
- Service Node public key
- Node records
- Wallet access
- Safe working environment

Do not start recovery work if you are unsure whether the SN private key is correct.

## 【12. Basic Backup Checklist】

Before running or maintaining a Service Node, make sure you have backed up:

- Wallet seed phrase
- Wallet password
- Wallet files if needed
- Service Node private key
- `.pem` files or other server access keys
- Server region and instance notes
- Service Node public key
- CLI version information
- Node operation notes

Recommended:

- One main encrypted backup
- One offline encrypted backup
- One separate paper backup for critical recovery information

## 【Conclusion】

Service Node security is as important as Service Node operation.

A node operator should not only know how to start, restart, or restore a node, but also know how to protect the keys and files behind the node.

Clear security and backup practices can help operators reduce avoidable risks, protect important credentials, and support the long-term stability of the Judecoin PoS Service Node network.
