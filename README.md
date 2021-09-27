# Establish SFTP connection with Fury applications

> SFTP is similar to FTPS in that both offer additional protection for files and changes made to the hosting. However, SFTP uses SSH (Secure Shell) technology to authenticate the contact and establish a secure connection between machines.

I'll leave you a link if you want to study more on the subject:
* https://www.hostinger.com.br/tutoriais/como-usar-sftp-ssh-file-transfer-protocol

We have 2 ways to establish an SFTP connection with Fury applications:

* External SFTP: The SFTP service is provided by a provider.
* Internal SFTP: The SFTP service is provided by MELI.

----------------------------------------------
## 1) Connection to an external SFTP

> The provider must share with us the URL of the SFTP service and the connection will be made by means of keys, one public and one private. We must share the public one with the provider and the private one will be hosted by the Secrets service in order to establish the connection. The steps required to perform this operation are as follows:

#### 1. The first step is to generate the public and private SSH keys from the terminal of your own machine by executing the following command:

-> ssh-keygen -t rsa -m PEM (using this command will generate the keys and encrypt in Base64)
![1 ssh-keygen -t rsa -m PEM](https://user-images.githubusercontent.com/81833300/134931157-613bafea-4e3c-4b01-8522-1f83ecd6d733.png)

-> Then it will ask you for the names of the files to be created. We use the name sftp_id_rsa:
![2 Generating Puplic:Privat](https://user-images.githubusercontent.com/81833300/134931460-854daa71-5706-46be-aec5-034632d3a8b2.png)

— > No es necesario ingresar una contraseña, si no desea ingresar presione enter dos veces:
 ![3 Senha](https://user-images.githubusercontent.com/81833300/134931666-6265384c-4b6a-41a7-a8e4-d31094a28d80.png)

-> After that, you will see that it was created successfully:
![4 Key](https://user-images.githubusercontent.com/81833300/134931759-391a5651-5675-4052-9d39-20ca1df86440.png)

-> Confirm that the 2 files were created with the name that you entered the Private and Public keys:
![5 pu:pri](https://user-images.githubusercontent.com/81833300/134931856-3868a9e4-b15c-4263-bc30-50dc021e0708.png)


#### 2. Once the keys have been generated, we will have to send the generated file with a .pub extension to the SFTP service provider, this will allow the validation of the public key with the private one.



#### 3. The next step we need to do is add both generated keys to Fury's SECRETS service. On the app side, we will use the private key to establish the connection, but we will add both keys to the service to ensure that the public key is protected by us and we have it available in case we have to share it with the provider again.
> IMPORTANT: The keys must be added to the secrets service encrypted in Base64, and then they will be decrypted from the APP code. This is necessary to avoid formatting problems.



-> Enter the name that the secret will have in key, the description and the keys.
![6 Create Secret Key](https://user-images.githubusercontent.com/81833300/134932009-49c60f59-87fd-48ab-925c-ce1757ef8ee7.png)

In itself setting secrets is very simple. From the team they provide us with a very clear user manual on how to manage it. Secrets service user manual.
In these cases, the best thing we can do if we want to bring those secrets to a code environment is to use the snippets that we can see in each of the secrets.

![7 Snippets](https://user-images.githubusercontent.com/81833300/134932157-aa8a48d8-7a85-4b4c-98a2-8708d42857d5.png)

The snippets are adapted according to the technology we use!
![8 Config Snippets](https://user-images.githubusercontent.com/81833300/134932264-e0d38cfb-9c29-4cd3-bd2c-2cf4125e6f8a.png)
  * This step must be repeated for each of the keys.

#### 4. In order to guarantee the connection between the SFTP service and our Fury app, it will also be necessary for the provider to have all the MELI public IPs allowed in its whitelist. The complete list of IPs is available at the following link:
https://mercadolibre.cloud.answerhub.com/articles/3767/ips-cuales-son-las-ips-de-nat-en-aws-y-gcp.html

#### 5. Once all the previous steps have been carried out, we can validate the connection from the app instances with the following steps:

-> We connect via Alfred to any of the instances of the app.
![9 alfred](https://user-images.githubusercontent.com/81833300/134933446-2b0c1d6d-9565-4392-a92a-12f115331437.png)

-> Inside the instance we can test the connection by executing the following command:
sftp -i key.pem user_name @ url_server_ftp (USER_NAME and URL_SERVER_FTP - They are reported by the provider)
![10 conexão alfred](https://user-images.githubusercontent.com/81833300/134933581-88a9e798-c263-4740-9542-8b1c2ad03e6b.png)
  * In the print of this tutorial we have established the connection with a public SFTP: demo@test.rebex.net

----------------------------------------------
## 2) Connection to an internal MELI SFTP

The steps for the connection will be the same as those established in the previous points, but what we must add is the request for the SFTP service, for this, all we have to do is create a ticket via shield "Request for SFTP Registration for supplier"

![11 meli](https://user-images.githubusercontent.com/81833300/134933843-78b13e3d-5775-4501-92d0-0c7e30c22b44.png)

