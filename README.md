## Generating SSH-KEYS on Windows

In order to generate a key, type `ssh-keygen` and hit Enter. This will automatically generate the SSH keys. 

On Windows 11, a 2048-bit RSA key is created. If you'd like to use a different algorithm — **GitHub recommends Ed25519**, for example — then you'd type `ssh-keygen -t ed25519`.

```powershell
C:\User> ssh-keygen -t ed25519
```

Switch to the specified directory where the key will be stored and run the following command to view its contents(Using git bash or bash for *convenience*):

```bash
$ cd /path/to/key && cat your-key.pub
```

## Authenticating via SSH
In case you are indeed using the SSH URL, but still are asked for username and password when git pushing:

```bash
git remote set-url origin git@github.com:<Username>/<Project>.git
```

Troubleshooting can be done by running the following command:

```bash
ssh -vT git@github.com
```

Sample output:

```bash
debug1: Trying private key: /c/Users/Username/.ssh/id_rsa
debug1: Trying private key: /c/Users/Username/.ssh/id_dsa
debug1: Trying private key: /c/Users/Username/.ssh/id_ecdsa
debug1: Trying private key: /c/Users/Username/.ssh/id_ed25519
debug1: No more authentication methods to try.
Permission denied (publickey).
```

**NOTE**: The following response will be generated if a key-value pair doesn't exist

* After generating a valid key-value pair, the following response will be genrated

```bash
debug1: Authentication succeeded (publickey).
Authenticated to github.com ([196.04.255.321]:22).
debug1: channel 0: new [client-session]
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: Sending environment.
debug1: Sending env LANG = C.UTF-8
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```
