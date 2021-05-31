# JKS (Java Key Store)
When you are working with JAVA applications and JAVA based server, you may need to configure a **Java key store (JKS)** file. 
**In Salesforce** certificates are used to authenticate single sign-on with an external website.

## Create Salesforce Certificate By importing JKS
*If you have existing JKS you can create certificate by:*
 - Go to setup 
 - Search for "Certificate and Key Management"
 - Click on Import from Keystore

# Generate JKS

**Generate JKS file from .key and .cert file:**
- **Prerequisite**: [OpenSSL](https://www.openssl.org/source/) & [JDK](https://www.oracle.com/in/java/technologies/javase-downloads.html)
 - Change their file extension from .key to .pem & .cert to .pem and run below command from folder directory where .key & .cert files available in **OpenSSL command prompt.**
 ```
 openssl pkcs12 -export -in certificate_pub.pem -inkey private.pem -certfile certificate_pub.pem -out testkeystore.p12
 ```
 
 - Enter any password you can easily remember.
 - Now there will **testkeystore.p12** file generated in your directory.
 - Now will Create JKS file using **keytool** following commands in **cmd**.
 ```
 keytool -importkeystore -srckeystore testkeystore.p12 -srcstoretype pkcs12 -destkeystore wso2carbon.jks -deststoretype JKS
 ```
 Now the jks file will be created as **wso2carbon.jks**.
 **Note**: By default [current alias] is set to **“1”**
 
**To change keystore password:**
```
keytool -keypasswd -alias [Alias name for private key] -keystore [path to key store]
```
e.g:
```
keytool -keypasswd -alias "1" -keystore wso2carbon.jks 
```
**To change Alias Name of keyStore:**
```
keytool -changealias -keystore [path to key store] -alias [current alias]
```
e.g: 
```
keytool -changealias -keystore wso2carbon.jks -alias "1"
```

## Screenshots:
![To create .P12](https://raw.githubusercontent.com/shivamkapasia0/JKS-Salesforce/main/JKS%20SS/createP12.png)
![to create JKS](https://raw.githubusercontent.com/shivamkapasia0/JKS-Salesforce/main/JKS%20SS/createJKS.png)
**Thanks for reading …!!! Also you can find more details on creating self signed KeyStore from**  **[here](http://www.javasecurity.org/2015/09/how-to-create-self-signed-keystore-jks.html)**
