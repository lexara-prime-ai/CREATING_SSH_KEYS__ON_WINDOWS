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


* The following command generates an SSH key named ssh-key in the  `$HOME/.ssh`  location with username  `vagrant`  with -C flag and passphrase  `mysecret`  with  `-q -P`  flag.

```sh
ssh-keygen -t rsa -f ~/.ssh/ssh-key -C vagrant -b 4096 -q -P "mysecret"
```

Let’s understand the flags.

1.  **-t rsa**: It is the ssh key algorithm. It is the default algorithm used by  `ssh-keygen`.
2.  **-f :**  keyfile name.
3.  **-q -P:** To add passphrase without prompt
4.  **-b:**  Key Encryption Level. The default is 2048 bits
5.  **-C:**  To set the comment in the last line of the public key. It is typically used to replace the default username set by the command. You can also use this flag to set the server username.

If you add the Linux username to the key file with  `-C`  , you can directly perform SSH without specifying the username in the SSH command.

For example,

```sh
ssh -i ~/.ssh/ssh-key 192.81.209.247
```

If you don’t want a passphrase and create the keys without a passphrase prompt, you can use the flag  `-q -N`  as shown below.

```sh
ssh-keygen -t rsa -f ~/.ssh/ssh-key -C vagrant -b 2048 -q -N ""
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
