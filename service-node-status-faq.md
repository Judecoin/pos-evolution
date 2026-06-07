# Judecoin Service Node Status and Common FAQ

## 【Description】

This FAQ explains common Judecoin Service Node status messages, operational checks, synchronization behavior, locked balance, and basic troubleshooting steps.

It is intended to help Judecoin Service Node operators better understand common node states, avoid operational mistakes, and follow safer troubleshooting practices.

## 【Q1: What does ./judecoind status show?】

The command:

`./judecoind status`

is used to check the running status of the Judecoin daemon.

It may show information such as:

- Current block height
- Synchronization status
- Network connection information
- Whether the daemon is running correctly
- Service Node status, if applicable

This command is mainly used to check whether the node software is running and syncing properly.

## 【Q2: What should I do if ./judecoind status does not show status immediately?】

If status does not show immediately, it may not mean the node has failed.

Common reasons include:

- The node has just started
- The daemon is still initializing
- The RPC service is not ready yet
- The blockchain is still synchronizing
- The old process was not fully stopped

You can wait 1-2 minutes and run again:

`./judecoind status`

If needed, restart the Service Node:

`./judecoind --service-node --service-node-public-ip $(curl -s ifconfig.me) --no-zmq --detach`

Then check again:

`./judecoind status`

## 【Q3: What does blockchain synchronization mean?】

Blockchain synchronization means the node is downloading and verifying blockchain data until it reaches the current network height.

A Service Node should complete synchronization before registration or before normal operation.

If synchronization is not complete, the node may not behave normally.

## 【Q4: Why should I wait for synchronization before registration?】

If the node is not fully synchronized, registration or status checking may be confusing.

Waiting for synchronization helps ensure:

- The node sees the latest blockchain state
- Registration information is generated correctly
- The node can communicate properly with the network
- Status checking is more reliable

## 【Q5: What does Service Node public key mean?】

The Service Node public key is the public identity of the node.

It can be displayed by running:

`./judecoind print_sn_key`

The public key can be used to search the node on the block explorer.

It is not the same as the private key.

## 【Q6: What is the Service Node private key?】

The Service Node private key is the node identity key.

It is usually stored as:

`/home/ubuntu/.bitjudecoin/key_ed25519`

This key is very important.

If the server is lost, damaged, reinstalled, or migrated, this key may be required to restore the original Service Node identity.

Do not disclose this key.

## 【Q7: What does locked balance mean?】

Locked balance usually means the coins are currently locked due to Service Node staking or other protocol rules.

Locked coins cannot be freely transferred until the relevant lock condition or release period is completed.

For Service Node staking, locked balance is expected behavior.

## 【Q8: Does restarting the node unlock the stake?】

No.

Restarting the node does not unlock the stake.

Restarting only affects the node software running on the server.

The staking transaction and locked balance are controlled by the blockchain rules.

## 【Q9: Does restoring the server create a new stake?】

No.

Restoring a Service Node server does not automatically create a new staking transaction.

If the original SN private key is used, the goal is to restore the original Service Node identity.

If a new key is used, the blockchain may treat it as a different node identity.

## 【Q10: What is the difference between restarting and restoring a Service Node?】

Restarting a Service Node means stopping and starting the node software again on the same server or environment.

Restoring a Service Node means using the original SN private key to recover the node identity on a new or reinstalled server.

Restarting is a normal maintenance action.

Restoring is usually needed when the original server is lost, damaged, reinstalled, or migrated.

## 【Q11: What should I check if the block explorer does not show my node?】

If the block explorer does not show your node, possible reasons include:

- The node registration transaction is not confirmed yet
- The node is still waiting for activation
- The block explorer has not updated
- The node public key was copied incorrectly
- The node was not registered successfully
- The node may have been deregistered
- The network or explorer may be temporarily delayed

You can check:

`./judecoind status`

and verify the Service Node public key with:

`./judecoind print_sn_key`

## 【Q12: What should I do if my node is not running?】

First check whether the daemon process is running:

`ps aux | grep judecoind`

If needed, stop the old process:

`pkill judecoind`

Wait a few seconds:

`sleep 5`

Then restart the Service Node:

`./judecoind --service-node --service-node-public-ip $(curl -s ifconfig.me) --no-zmq --detach`

After that, check status:

`./judecoind status`

## 【Q13: What should I do after a server reboot?】

After a server reboot, the node may need to be started again manually.

Enter the Judecoin CLI directory and run:

`./judecoind --service-node --service-node-public-ip $(curl -s ifconfig.me) --no-zmq --detach`

Then check:

`./judecoind status`

If the server has been restarted, make sure the key file still exists:

`/home/ubuntu/.bitjudecoin/key_ed25519`

## 【Q14: What should I do before upgrading CLI?】

Before upgrading CLI, it is recommended to:

- Check the community release information
- Confirm the latest version number
- Back up the Service Node private key
- Back up important node records
- Stop the old daemon process
- Download the correct new CLI version
- Verify the new version after installation

Do not upgrade from unknown download links.

## 【Q15: Why should CLI version numbers be updated in guides?】

CLI version numbers may change over time.

For example, a guide may use:

`v3.2.0`

But if the community version becomes:

`v3.1.3`

then users should update:

- Download file name
- Download link
- Extracted folder name
- Version check result

Always follow the latest official release.

## 【Q16: What is decommissioned status?】

Decommissioned generally means the Service Node is not currently meeting required conditions or has been temporarily removed from normal active operation.

Possible reasons may include downtime, failure to provide required proofs, network instability, or other protocol checks.

The exact behavior depends on chain rules and implementation.

Users should check community explanations and current on-chain status.

## 【Q17: What is deregistered status?】

Deregistered generally means the node has been removed from the active Service Node set.

A deregistered node may no longer participate in rewards.

If the stake is still locked, it may need to wait for the release period according to chain rules.

Users should check the current on-chain status and official documentation.

## 【Q18: Do deregistered nodes still receive rewards?】

Generally, a deregistered node should not be expected to receive normal Service Node rewards.

However, if the stake is still locked during the release period, the coins may still be unavailable for transfer until the release condition is met.

The exact behavior should be confirmed through community rules and on-chain status.

## 【Q19: If a node is deregistered, can I recover it by restoring the server?】

It depends on the on-chain state.

If the node still exists on-chain and the original SN private key is restored correctly, the node may be able to continue running.

If the node has already been fully deregistered and entered the release period, restoring the server may not reactivate the original node.

In that case, the locked stake may need to wait for the release period to end.

## 【Q20: Should I delete the .bitjudecoin directory when troubleshooting?】

No, do not delete it casually.

The directory:

`/home/ubuntu/.bitjudecoin`

may contain important node data, including:

`key_ed25519`

Deleting this file or directory without backup may cause loss of the Service Node identity.

Always back up important files before making changes.

## 【Q21: What should never be shared when asking for help?】

Never share:

- Wallet seed phrase
- Wallet private key
- Wallet password
- Wallet files
- Service Node private key
- `.pem` file or other server access key
- Server login credentials
- Verification codes
- Full backend screenshots containing sensitive information

When asking for help, remove or hide sensitive information first.

## 【Q22: What is the safest basic troubleshooting order?】

A safer basic order is:

1. Check whether the daemon is running
2. Check node status
3. Check synchronization
4. Confirm CLI version
5. Confirm Service Node public key
6. Check block explorer
7. Restart the node if needed
8. Avoid deleting key files
9. Back up before making changes
10. Ask for help only after removing sensitive data

## 【Security Reminders】

Service Node operators should follow strict security practices:

- Do not disclose wallet seed phrases.
- Do not disclose wallet private keys.
- Do not disclose wallet passwords.
- Do not disclose wallet files.
- Do not disclose the Service Node private key.
- Do not disclose `.pem` files or other server access keys.
- Do not expose server login credentials.
- Do not share backend screenshots containing sensitive information.
- Do not delete key files without backup.
- Always back up important files before troubleshooting.

## 【Conclusion】

Service Node operation involves both technical steps and security awareness.

Many issues can be checked by reviewing synchronization, CLI version, daemon status, Service Node public key, block explorer information, and uptime proof status.

Clear FAQ documentation can help operators reduce confusion, avoid common mistakes, and support the long-term stability of the Judecoin PoS Service Node network.
