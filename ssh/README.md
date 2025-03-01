# ssh

OpenSSH notes.

## Dealing with host key type error

On some older gear, an error like this will appear:

`no matching host key type found. Their offer: ssh-rsa`

To get around this temporarily, add it to the runtime command, e.g. `ssh -oHostKeyAlgorithms=+ssh-rsa user@server`

Alternatively, add to `~/.ssh/config`:

    Host nas
      HostName server
      HostKeyAlgorithms=+ssh-rsa
