# ledger-ssh-add (authenticate once, use multiple times)
If you are a sysadmin and you are using your Ledger Nano device as your hardware ssh key (probably using [ledger_agent](https://pypi.org/project/ledger_agent/)) and you are tired of authorising every request using your device, then this tool is created for you.

Instead of using dedicated ssh agent for signing every request using private key stored in your hardware device it instead uses your hardware device to derive the private key for given identity and uses the system default ssh agent to store it for specified amount of time.

That way you can use the key from any shell in the system for specified amount of time without the need of signing every action separately.

When executed the tool adds the derived key to the default system ssh agent with given timeout and displays the public key which you should add to `.ssh/authorized_keys` on remote servers.

At any time you can remove the derived key from system ssh agent using:
```bash
ssh-add -D
```

## Usage

```
usage: ledger-ssh-add [-h] [--timeout TIMEOUT] [--salt SALT] [--nopass]
                      identity

positional arguments:
  identity           identity name for key derivation (e.g. user@host)

optional arguments:
  -h, --help         show this help message and exit
  --timeout TIMEOUT  set lifetime (in seconds) when adding identities (default
                     3600)
  --salt SALT        extra salt for key derivation
  --nopass           use empty password for key derivation
```

## Example

```bash
$ ledger-ssh-add example.com
Password:
ecdsa-sha2-nistp384 AAAAE2VjZHNhLXNoYTItbmlzdHAzODQAAAAIbmlzdHAzODQAAABhBAPCCcVGxehN7YCZg55EE2rssMGz1Fkc8/xdh5TV6bY1L3jDj2+zPOa5zXIMDLNFCVthmbhIYvpXTJkhTfxHaXzTiNuYrxyJCd8vqm8pDKi1kIZOMAPLIG3+qJ1KtsDzIA==
```

## Note

If you have problems with accessing your ledger nano device under Linux you should add proper udev rules using the `add_uder_rules.sh` script from [here](https://github.com/LedgerHQ/udev-rules).

## External links
1. [A Step by Step Guide to Securing your SSH Keys with the Ledger Nano S](https://thoughts.t37.net/a-step-by-step-guide-to-securing-your-ssh-keys-with-the-ledger-nano-s-92e58c64a005)
2. https://github.com/LedgerHQ/ledger-app-ssh-agent
3. https://github.com/romanz/trezor-agent
4. https://github.com/LedgerHQ/udev-rules
