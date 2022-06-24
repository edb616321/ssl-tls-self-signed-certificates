
## Proxmox SSL-TLS Self-signed certfificate process.
---

###  1) General information


This script is based on the openssl standard. The OpenSSL library is the openssl binary, and is usually located in the **/usr/bin/openssl** folder.

OpenSSL can be used interactively. Please refer to the documentation at the openssl.org website for further information. 

**Important Note:**

Please take time to verify your certificates with an online decoder site. It is important to verify the CN,(Container) and chain of trust information. 

Cert Logik: [https://certlogik.com/decoder/]


`openssl verify -CAfile ca.pem -verbose cert.pem`


The openssl general syntax is as follows:

 `openssl command [ command_options ] [ command_arguments ]`

### Certificate Formats

X.509 Certificates exist in Base64 Formats **PEM (.pem, .crt, .ca-bundle)**, **PKCS#7 (.p7b, p7s)** and Binary Formats **DER (.der, .cer)**, **PKCS#12 (.pfx, p12)**.

### Convert Certs

COMMAND | CONVERSION
---|---
`openssl x509 -outform der -in cert.pem -out cert.der` | PEM to DER
`openssl x509 -inform der -in cert.der -out cert.pem` | DER to PEM
`openssl pkcs12 -in cert.pfx -out cert.pem -nodes` | PFX to PEM

---
---

### Create the certs necessary to be your own CA (Certificat Authoriry)
1. Generate RSA
```bash
openssl genrsa -aes256 -out ca-key.pem 4096
```
2. Generate a public CA Cert
```bash
openssl req -new -x509 -sha256 -days 365 -key ca-key.pem -out ca.pem
```

You are using the ca-key.pem file to generate a openssl request. 

**You should now have two files ca-key.pem and ca.pem**


---
---

### Generate Certificate
1. Create a RSA key
```bash
openssl genrsa -out cert-key.pem 4096
```
2. Create a Certificate Signing Request (CSR)
```bash
openssl req -new -sha256 -subj "/CN=yourcn" -key cert-key.pem -out cert.csr
```
3. Create a `extfile` with all the alternative names
```bash
echo "subjectAltName=DNS:your-dns.record,IP:257.10.10.1" >> extfile.cnf
```
4. Create the certificate
```bash
openssl x509 -req -sha256 -days 365 -in cert.csr -CA ca.pem -CAkey ca-key.pem -out cert.pem -extfile extfile.cnf -CAcreateserial
```

---
---

### Combine and copy/paste certs into the Proxmox GUI.

`cat cert.pem > fullchain.pem`

`cat ca.pem >> fullchain.pem`

>In the proxmox Gui, 
-click on your node 
-click on certificates
-click on Upload Custom Certificates

**Copy/Paste the cert.pem into the Private key section.** 
**Copy/Paste the fullchain.pem into the Certificate Chain section.** 

Click upload.

### Install the CA Cert as a trusted root CA on your windows desktop.


### Windows

>Note: (You must be logged into powershell as admin. The command below will not work in the cmd terminal.) 

Assuming the path to your generated CA certificate as `C:\ca.pem`, run:
```powershell
Import-Certificate -FilePath "C:\ca.pem" -CertStoreLocation Cert:\LocalMachine\Root
```
- Set `-CertStoreLocation` to `Cert:\CurrentUser\Root` 
- in case you want to trust certificates only for the logged in user.

---
---

You are done!! You may need to reboot both the proxmox server and your windows workstation to see the results. 