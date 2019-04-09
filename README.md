# Certificate

## Prefecture Trust store (MIAT)

To send documents to the Prefecture, you need to trust its certificate and the Prefecture needs to trust yours.

For the first point, you need to create a trustore with the Prefecture certificate and its trust chain (cf `application.miat.truststorepath` and `application.miat.truststorepasswd`).

Similarly, create a keystore and import into it the certificate (and its certificate chain) you provided to the Prefecture. Then fill the required configuration properties `application.miat.keystorepath` and `application.miat.keystorepasswd`.

### Some useful commands to create the Prefecture truststore

* Convert PKCS7 to certificate

```
openssl pkcs7 -inform der -print_certs -in serveur.silsir.sas.interieur.gouv.fr.p7b -out certificate_chain.cer
```

* Put each certificate in a file `certificat_chain_X` (cf sample files in `certificates` directory)

* Remove old certificates (if any) from the trust store

```
keytool -delete -alias cert_pref_X -keystore truststore.jks
```

* Import the prefecture certificates chain

```
keytool -import -trustcacerts -alias cert_pref_X -file certificate_chain_X.crt -keystore truststore.jks
```

## STELA2 migration

* The SSH keys in `ssh-keys` are used for migrations from STELA2

If you don't have any running STELA2 instance or do not bother migrating data from it, you can simply ignore this configuration.

If not, just put the SSH keys needed to connect to the VM hosting your STELA2 instance and configure the names and passphrases in application.yml (cf `application.migration.privateKeyPath`, `application.migration.publicKeyPath` and `application.migration.keystorepath`).

