# Create Server Key Store
keytool -genkey -v -alias jbossalias -keyalg RSA -keysize 1024 -keystore jbossServer.keystore -validity 3650 -keypass JBossPassword -storepass JBossPassword -dname "CN=localhost, OU=JBoss Unit, O=JBoss, L=Pune, S=Maharashtra, C=IN"

# Exporting Server's Public Key
keytool -export -keystore jbossServer.keystore -alias jbossalias -file serverPublicKey.cer -keypass JBossPassword -storepass JBossPassword


# Create Client Key Store
keytool -genkey -v -alias clientalias -keyalg RSA -keysize 1024 -keystore jbossClient.keystore -validity 3650 -keypass clientPassword -storepass clientPassword -dname "CN=localhost, OU=Client Unit, O=JBoss, L=Pune, S=Maharashtra, C=IN"


# Exporting Client's Public Key
keytool -export -keystore jbossClient.keystore -alias clientalias -file clientPublicKey.cer -keypass clientPassword -storepass clientPassword


# Importing Client's Public key into server's truststore
keytool -import -v -trustcacerts -alias clientalias -file clientPublicKey.cer -keystore jbossServer.keystore -keypass JBossPassword -storepass JBossPassword


# Importing Server's Public key into client's truststore
keytool -import -v -trustcacerts -alias jbossalias -file serverPublicKey.cer -keystore jbossClient.keystore -keypass clientPassword -storepass clientPassword


++++++++++++++++++
More Details: http://middlewaremagic.com/jboss/?p=2176
