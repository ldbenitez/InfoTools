# Java Keytool Commands for Creating and Importing

These commands allow you to generate a new Java Keytool keystore file, create a CSR, and import certificates. 
Any root or intermediate certificates will need to be imported before importing the primary certificate for your domain.

### Commands for key generation and import

```shell
### Generate a Java keystore and key pair
keytool -genkey -alias mydomain -keyalg RSA -keystore keystore.jks -keysize 2048

### Generate a certificate signing request (CSR) for an existing Java keystore
keytool -certreq -alias mydomain -keystore keystore.jks -file mydomain.csr

### Import a root or intermediate CA certificate to an existing Java keystore
keytool -import -trustcacerts -alias root -file rootorintermediate.crt -keystore keystore.jks

### Import a signed primary certificate to an existing Java keystore
keytool -import -trustcacerts -alias mydomain -file mydomain.crt -keystore keystore.jks

### Generate a keystore and self-signed certificate
keytool -genkey -keyalg RSA -alias selfsigned -keystore keystore.jks -storepass password -validity 360 -keysize 2048

###Import New CA into Trusted Certs
keytool -import -trustcacerts -file /path/to/ca/ca.pem -alias CA_ALIAS -keystore $JAVA_HOME/jre/lib/security/cacerts
```

### Commands for Checking

```shell
### Check a stand-alone certificate
keytool -printcert -v -file mydomain.crt

### Check which certificates are in a Java keystore
keytool -list -v -keystore keystore.jks

### Check a particular keystore entry using an alias
keytool -list -v -keystore keystore.jks -alias mydomain

### List Trusted CA Certs
keytool -list -v -keystore $JAVA_HOME/jre/lib/security/cacerts
```

### Other  Commands

```shell
### Delete a certificate from a Java Keytool keystore
keytool -delete -alias mydomain -keystore keystore.jks

### Change a Java keystore password
keytool -storepasswd -new new_storepass -keystore keystore.jks

### Export a certificate from a keystore
keytool -export -alias mydomain -file mydomain.crt -keystore keystore.jks

```
