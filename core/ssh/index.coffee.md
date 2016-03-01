
# SSH

## Configuration

Configuration extends the configuration of the "masson/core/users" with
new properties "authorized\_keys", "rsa" and "rsa_pub" and also define
two new properties "sshd\_config" and "banner".

*   `users.[].authorized_keys` (string, array)
    A list of SSH public keys added to the "~/.ssh/authorized_keys" file, optional.
*   `users.[].rsa` (string)
    Private SSH key of the user, optional.
*   `users.[].rsa_pub` (string)
    Public SSH key of the user, optional.
*   `ssh.sshd_config` (object)
    Configure the SSH daemon by updating the "/etc/ssh/sshd_config" file with
    key/value properties, optional.
*   `ssh.banner` (object)
    Write a banner file in the system and register it with the "/etc/ssh/sshd_config" file, optional.


```json
{
  "users": [{
    "name": "root"
    "authorized_keys": [ "ssh-rsa AAAA...ZZZZ me@email.com" ],
    "rsa": "-----BEGIN RSA PRIVATE KEY-----\nMIIEpAIBAAKCA...PKToe4z7C9BqMT7Og==\n-----END RSA PRIVATE KEY-----"
    "rsa_pub": "ssh-rsa AAAA...YYYY user@hadoop"
  },{
    "name": "sweet"
    "home": "/home/sweet"
    "authorized_keys": [ "ssh-rsa AAAA...XXXX you@email.com" ]
  }]
  "ssh": {
    "sshd_config": {
      "UsePAM": "yes"
      "Port": 2222
    },
    "banner": {
      "destination": "/etc/banner",
      "content": "Welcome to Hadoop!"
    }
  }
}
```

    # exports.push 'masson/core/users'
    # exports.push 'masson/core/yum'

    module.exports = ->
      'configure': [
        'masson/core/users'
        'masson/core/ssh/configure'
      ]
      'install': 'masson/core/ssh/install'