foobar.tar.asc is an encypted tar archive that contains a GPG secret key and
SSH public and private keys. These can assist in recovering passwords when
all else is failing.

= Creation

  % KEYID=87392271845ECA084CF202242BFED8F6846F99B4
  % TARNAME=foobar.tar
  % gpg2 --export-secret-keys --armor $KEYID > $KEYID.priv.asc
    (entered passphrase for $KEYID)
  % tar cvf $TARNAME $KEYID.priv.asc $HOME/.ssh/id_ed25519.pub $HOME/.ssh/id_ed25519
  % gpg2 --symmetric --armor $TARNAME
    (entered encryption passphrase)
    (outputs file $TARNAME.asc)

= Recovery

Set up env variables.

  % KEYID=87392271845ECA084CF202242BFED8F6846F99B4
  % TARNAME=foobar.tar

Decrypt.

  % gpg2 --decrypt $TARNAME.asc > $TARNAME
    (enter encryption passphrase that you hopefully remember)

Extract tar files.

  % tar xv $TARNAME

Import and trust GPG secret key.

  % gpg2 --import $KEYID.priv.asc
    (enter passphrase for $KEYID)
  % gpg2 --edit-key $KEYID trust quit
    (at prompt: I trust ultimately)

Copy SSH public and private keys. (Take care to not overwrite any existing
keys.)

  % cp home/nishanthshanmugham/.ssh/{id_ed25519.pub,id_ed25519} $HOME/.ssh/

Now clone the private passwords repository (the SSH keys should make this
possible to do).

  % git clone git@github.com:nishanths/super-duper-meme.git $HOME/.password-store

Retrive passwords (the GPG key and GPG key passphrase should make this
possible to do).

  % pass show <pass-name>
