# bulksign
bulksign is a Python3-based tool that will take a list of key fingerprints and
sign them with your GPG keypair. Then, it will sign each UID in that keypair
individually and create an encrypted email to that siggle UID. All emails will
be written to an mbox file that can be directly used in Thunderbird to send the
messages. This is particularly useful when you're on a desktop computer without
any MTA running in the background.

## Usage
```
usage: bulksign [-h] [--oneshot] -a email [-n realname] [-c lvl] [-f]
                [-o filename] [-v]
                fingerprint filename

positional arguments:
  fingerprint           Fingerprint of the secret key that does signing.
  filename              List of fingerprints that should be signed.

optional arguments:
  -h, --help            show this help message and exit
  --oneshot             Break after the first signature. Useful for debugging.
  -a email, --from-address email
                        Email address to fill in as the 'from' address.
  -n realname, --signer-name realname
                        Signer name. If not specified, take from getpwnam().
  -c lvl, --cert-level lvl
                        Specify the certification level from 0 to 3.
  -f, --force           Do not ask for confirmation.
  -o filename, --outfile filename
                        Output filename. Defaults to outbox.mbox.
  -v, --verbose         Increase verbosity and show all stderr output of gnupg
```

For example, if you have a file with fingerprints, one per line, that is called
"keylist.txt", you can simply:

```
$ ./bulksign -a foo@bar.com -c 3 b4cbbaedab4c84f05b832e00bb42b7582e72b807 keylist.txt
```

Where b4cbb... is your own key fingerprint and foo@bar.com is the "From"
address in the generated emails. If all goes well, it'll create a "outbox.mbox"
file which you can simply append to your Thundbird outbox:

```
$ cat outbox.mbox >>~/.thunderbird/abc1abcd.default/Mail/Local\ Folders/Unsent\ Messages
```

## Dependencies
Python3, mako, gpg.

## License
GNU GPL-3.
