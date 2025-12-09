# **OIE 4.6 Documentation Master**

# **1\. Overview**

Open Integration Engine 4.6 introduces three new features: 
\
\
1: Support for TLS and mTLS with the TLS Manager plugin. 
\
\
The TLS Manager plugin provides

   - a web based administration portal for certificate management.
   - a configurable TLS section in the sender and listeners of the HTTP, TCP and Web Services connector types in OIE.  

2: Support for channel design version control with the Git Extension plugin.  

3: When searching messages or events, the Start Time and End Time fields now default to 24-hour clock.

# **2\. TLS Manager Administration**

#### **Admin: Login**

The administration page can be accessed using the following URL:
```
https://<servername>:port/tls-manager
```
For example:
```
https://oiedev:8443/tls-manager
```
Or locally:
```
https://localhost:8443/tls-manager
```
\
The HTTP URL is disabled by default but can be enabled by adding
```
server.http.enable = true
```
to the mirth.properties file and restarting the OIE service.

#### **Admin: Categories**

The administration is organised into three Categories:  
**![][image1]**
\
\
*Native Java Certificate Store*:	Read-only Java certificate store.  
*Additional Trusted Certificates*: 	Certificates of remote clients or remote servers.  
*Local Certificates:* 				Certificates with Private Keys. Typically representing the owner of the OIE instance.

#### **Admin: Panel Display**

In each category certificates are shown in a panel view containing these data items:

```
Alias
Type 
Subject
Issuer  
Valid From
Valid To 
Fingerprint (SHA-1)
```


Native Java Certificate Store panel display example:  
![][image2]  
	*Note: the Export button is not supported.*

#### 

#### **Admin: Certificate Details**

The *View Details* button shows:

```
Alias  
Type
Store
Has Private Key
Subject
Issuer
Valid From
Valid To 
SHA-1
basicContraints
keyUsage
Raw Certificate (Base64)
Certificate Verification
```
Certificate Details example:

![][image3]

Certificate Details example continued:

![][image4]  
![][image5]

The *Verify Certificate* button tasks TLS Manager with verifying the certificate against  using CA and OCSP resources. check  
It will display the result including chain validation details if relevant.

Verification Example:  
![][image6]

#### **Admin: Additional Trusted Certificates**

Options:

*Import Certificate (from file)*  
*Import From URL*  
*Add New*

*![][image7]*

##### **ATC: Import Certificate**

On clicking the *Import Certificate* button you can either paste a PEM Certificate Chain into the text box or click *Choose Certificate File* and select a file to import from disk:  
![][image8]

##### **ATC: Import From URL**

On clicking the *Import From URL* button you can paste an HTTPS URL into the field.  
![][image9]  
Click *Fetch Certificates* to show details of the certificates available.

##### **![][image10]**

Example:

##### **![][image11]**

##### **![][image12]**

##### **ATC: Certificate Management**

Additional Trusted Certificates Panel Display example:

*![][image13]*


###### **ATC: Certificate Edit**

A certificate alias can be edited, as illustrated below.  
**![][image14]**

###### **ATC: Certificate Removal**

A certificate can be removed, as illustrated below.  Please note this action cannot be undone.

![][image15]

#### **Admin: Local Certificates**

Options:

*Show Private Keys*  
*Import Certificate (from file)*  
*Add New*

*![][image16]*



##### **LC: Panel Display**

Local Certificates Panel Display example:

![][image17]



##### **LC: Import Certificate**

##### **LC: Show Private Keys**





 

# **3\. TLS Manager Configuration**

### **Senders**

The TLS Settings section is present in the **HTTP Sender**, **TCP Sender** and **Web Service Sender** connector types.

#### ***TLS Settings***

**Use TLS Manager**: Yes/No  
	*Enables the TLS section*  
	*![][image18]*  
\
**Server Certificate Validation**: Enabled/Disabled  
***I**f you want the receiving endpoint to prove its identity?*
*![][image19]*  
\
**Subject DN Validation Mode**: None/Partial/Exact  
*To check the receiving endpoint certificate matches specific Distinguished Name attributes.  **Use with caution.***  
*Example for illustration purposes only:*  
*![][image20]*
\
\
**CRL Mode**: Disabled/Soft Fail/Hard Fail  
*To have the endpoint certificate? automatically checked against a Certificate Revocation List (CRL) service.*  
*The service used is defined within each certificate. It will typically be the Issuing Authority.*  
*Protocol: TCP; Port 80 or 443\**  
*\*Note: is possible for a certificate to specify a different port.*  
***Soft Fail** will allow the connection to proceed in the event that the CRL service does not respond.*  
***Hard Fail** will only allow the connection if the CRL service responds and the certificate is confirmed as not revoked.*
\
\
**OCSP Mode**: Disabled/Soft Fail/Hard Fail  
*To have the endpoint certificate? automatically checked against an Online Certificate Status Protocol service (OSCP).*  
*The service used is defined within each certificate. This is typically the Certificate Authority (CA) that issued it.*  
*Protocol: TCP; Port 80 or 443\**  
*\*Note: It is possible for a certificate to specify a different port*  
***Soft Fail** will allow the connection to proceed in the event that the OSCP service does not respond.*  
***Hard Fail** will only allow the connection if the OSCP service responds and the certificate is confirmed as not revoked.*
\
\
**Trusted Server Certificates**:  
*If Server Certificate Validation is Enabled (above).*  
*Select from **Additional Trusted Certificates.***  
***![][image21]***  
***![][image22]***
\
\
**Hostname verification**: Enabled/Disabled  
To verify hostname matches? (matches what?)  
***![][image23]***
\
\
**Client Certificate**:  
*Your client certificate to present to the endpoint if requested or required.  Select from **Local Certificates.***  
***![][image24]***
\
\
**Enabled Protocols**:  
*Select the acceptable protocol or protocols.*  
*The list is defined in mirth.properties as https.server.protocols*  
*![][image25]*
\
\
**Enabled Ciphers**:  
*Select the ciphers associated with the selected protocol(s).*  
*The list is defined in  mirth.properties as https.ciphersuites*  
*![][image26]*  
	

#### ***Sender GUI Examples***

##### **Connector Type: HTTP Sender**

![][image27]

##### **Connector Type: TCP Sender** 

![][image28]

##### 

##### **Connector Type: Web Service Sender**

### **![][image29]**

### **Listeners**

The TLS Settings section is present in the **HTTP Listener**, **TCP Listener** and **Web Service Listener** connector types.

#### ***TLS Settings***

**Use TLS Manager**: Yes/No  
	*Enables the TLS section*  
	*![][image18]*
\
\
**Server Certificate**:  
*Select from **Local CertifIcates***  
***![][image30]***  
\
**Client Authentication Mode**: None/Requested/Required  
I*f you want the client to prove their identity you can **Request** (provide the option) or **Require** (mandate) that they supply a certificate.*  
***![][image31]***  
\
**Trusted Client Configuration**:  
*If you are Requesting or Requiring a Client Certificate (above).*  
*Select from **Additional Trusted Certificates.***  
***![][image32]***  
***![][image33]***  
\
**Subject DN Validation Mode**: None/Partial/Exact  
*If you want to accept Client Certificates that match specific Distinguished Name attributes.  **Use with caution.***  
*Example for illustration purposes only:*  
*![][image20]*  
\
**CRL Mode**: Disabled/Soft Fail/Hard Fail  
*To have a Client Certificate automatically checked against a Certificate Revocation List (CRL) service.*  
*The service used is defined within each certificate. It will typically be the Issuing Authority.*  
*Protocol: TCP; Port 80 or 443\**  
*\*Note: is possible for a certificate to specify a different port.*  
***Soft Fail** will allow the connection to proceed in the event that the CRL service does not respond.*  
***Hard Fail** will only allow the connection if the CRL service responds and the certificate is confirmed as not revoked.*  
*![][image34]*
\
\
**OCSP Mode**: Disabled/Soft Fail/Hard Fail  
*To have a Client Certificate automatically checked against an Online Certificate Status Protocol service (OSCP).*  
*The service used is defined within each certificate. This is typically the Certificate Authority (CA) that issued it.*  
*Protocol: TCP; Port 80 or 443\**  
*\*Note: It is possible for a certificate to specify a different port*  
***Soft Fail** will allow the connection to proceed in the event that the OSCP service does not respond.*  
***Hard Fail** will only allow the connection if the OSCP service responds and the certificate is confirmed as not revoked.*  
*![][image35]*
\
\
**Enabled Protocols**:  
*Select the server protocol or protocols.*  
*The list is defined in mirth.properties as https.server.protocols*  
*![][image25]*
\
\
**Enabled Ciphers**:  
*Select the ciphers associated with the selected protocol(s).*  
*The list is defined in  mirth.properties as https.ciphersuites*  
*![][image26]*  
	

#### ***Listener GUI Examples***

##### **Connector Type: HTTP Listener**

![][image27]

##### **Connector Type: TCP Listener**

![][image36]

##### 

##### **Connector Type: Web Service Listener**

![][image37]



# **4\. Version Control**

The GIT Extension plugin provides the Edit Channel view with an extra tab: *Version History*

![][image38]

#### ***Version History***

Shown here is the version history of the channel.  The latest version is at the top of the list.

![][image39]

#### 

#### ***Channel Tasks: Refresh History*** 

The Version History is automatically refreshed when a user enters the Edit Channel view.   
If a user wishes to see a change reflected in the Version History tab without leaving the Edit Channel view, the GIT Extension provides a *Refresh History* option in the Channel tasks section.

![][image40]             ![][image41]

#### ***Show Diff***

To view the differences between two versions, click on one version to highlight it and then **Ctrl** \+ **click**  (*check Mac, Linux*) on the other version to highlight it as well.  
Right-click one of the highlighted versions to reveal a dropdown menu.    
Select *Show Diff* from the dropdown.

#### ***![][image42]***

#### ***Channel Diff: Object View***

Displays a side-by-side illustration on the channel’s defined properties and data items with differences highlighted.

![][image43]

#### 

#### ***Channel Diff: XML View***

Displays a side-by-side illustration on the channel XML with differences highlighted.

![][image44]

#### 

#### ***Revert***

To revert the channel design to an alternative version right-click the chosen alternative and select *Revert to this version* from the dropdown.  This action creates a new version of the channel based on the selected version.

# **![][image45]**

# 

# **5\. Search Time Format**

When searching in *Channel Messages* or *Events*, the *Start Time* and *End Time*  fields now default to 24-hour clock.

\<Channel Message screenshot\>  
\<Events screenshot\>

If the AM/PM time format is preferred it can be selected by going into Settings \> Administrator \> User Preferences and setting  "Message searches use 24-hour format" to "No."

# 

# **Appendix A**

### **TLS Exceptions**

HTTP Sender with no client cert and client authentication is Required:
```
SSLHandshakeException: Received fatal alert: certificate\_required  
SocketException: Connection reset by peer
```
HTTP Listener Subject DN Validation Exact/Partial match fail cases (on incoming client certs):
```
SSLHandshakeException: Received fatal alert: certificate\_unknown  
SocketException: Broken pipe
```
TCP Listener client auth OCSP unreachable Hard Fail mode:  
```
SSLHandshakeException: Received fatal alert: certificate\_unknown  
SocketException: Broken pipe
```
TCP Listener Subject DN Validation Exact/Partial match fail cases (on incoming client certs):  
```
SSLHandshakeException: Received fatal alert: certificate\_unknown  
SocketException: Broken pipe
```
WebService Sender with no client cert and client authentication is  Required:
```
SSLHandshakeException: Received fatal alert: certificate\_required  
SocketException: Connection reset by peer
```
Most WebService Listener client authentication failure cases:
```
SocketException: Connection reset  
SocketException: Broken pipe  
\[listener\_url\] failed to respond
```

All Senders with unreachable CRL in Hard Fail mode: 
```
SSLHandshakeException: Validation error: Could not determine revocation status  
SSLHandshakeException: Validation error: Unable to determine revocation status due to network error  
```

# **Document History**

| Version | Notes | Author | Date |
| :---- | :---- | :---- | :---- |
| 0.5 | TLS Exceptions Appendix A | ETR | 09-Dec-25 |
| 0.4 | Search and Event Time Format | ETR | 08-Dec-25 |
| 0.3 | TLS Manager: Configuration  | ETR | 08-Dec-25 |
| 0.2 | TLS Manager: Administration | ETR | 05-Dec-25 |
| 0.1 | GIT Extension | ETR | 04-Dec-25 |
