= Creation

  % KEYID=87392271845ECA084CF202242BFED8F6846F99B4
  % gpg2 --export-secret-keys --armor $KEYID > $KEYID.priv.asc
    (entered passhprase for $KEYID)
  % tar cvf $KEYID.priv.asc.tar $KEYID.priv.asc
  % gpg2 --symmetric --armor $KEYID.priv.asc.tar
    (entered encryption passphrase)
    (outputs file $KEYID.priv.asc.tar.asc)

= Recovery

  % KEYID=87392271845ECA084CF202242BFED8F6846F99B4
  % gpg2 --decrypt $KEYID.priv.asc.tar.asc > $KEYID.priv.asc.tar
    (enter encryption passphrase that you hopefully remember)
  % tar xvf $KEYID.priv.asc.tar
  % gpg2 --import $KEYID.priv.asc
    (enter passhprase for $KEYID)
  % gpg2 --edit-key $KEYID trust quit
    (at prompt: I trust ultimately)
