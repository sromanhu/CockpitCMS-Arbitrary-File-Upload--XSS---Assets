# Cockpit CMS 2.7.0 File Upload - XSS

## Author: (Sergio)

**Description:** File upload vulnerability in Cockpit CMS 2.7.0 allows a local attacker to upload a pdf file with hidden XSS.

**Attack Vectors:** AV:N/AC:L/PR:H/UI:N/S:U/C:L/I:L/A:L

---

### POC:

This is the software version.

![Version](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/9b5ae2e1-bf8c-4794-9cdb-fd2e76488ee7)

This is the content of the XSS injected in the PDF file.

![Datos maliciosos de XSS parte 2](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/a463d3d8-7c0d-47f0-a33b-f96adda71d4a)



When logging into the panel, we will go to the "Assets." section off General Menu and click on Upload Asset.

![Upload Asset](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/5ef2f5af-c017-40ca-9f87-3502065dc855)


We upload the injected PDF file:

![Upload Asset PDF](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/2854b82a-c3e3-4013-a17b-b9c60ffc8970)


In the following evidence we can see that it has been uploaded correctly:

![Upload asset complete](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/8be71211-6731-4aea-b7b2-7dcc7c90dfd0)


To access the Injected PDF we click on the file as shown below:

![XSS Edit Asset](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/be8e3a09-de5c-4789-80b9-bfbe349122f3)


And we copy the link of the server path and the ID of the file where it is stored:

![XSS Edit Asset y copiar link](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/0dd184a7-b4fb-4ba6-b638-904ad552359b)


We access the copied URL and the XSS pop-up appears

![XSS Result](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/8027f558-1723-4f9b-8f4e-7810183b2aae)



### Next, I have developed another PoC where I explain how I created the malicious PDF file and took advantage of the vulnerability to obtain the XSS:

The first thing is to generate the malicious PDF with hidden XSS.

To do this, we create a .js file with the Javascript code that we want to inject for the XSS in the PDF file.

![Fichero js](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/83a0c2c7-4736-4b06-b663-3304082f56bb)


Then we create an empty PDF file (pdf2go) and inject the payload of the .js file using the JS2PDFInjector tool

![Injectar payload del fichero js en PDF vacio](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/29b37616-f70f-47de-b91f-9c68b078508a)

We can analyze the content of the injected PDF using the Peepdf tool.

![Revisión codigo Javascipt en fichero injectado](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/2d7db472-701f-45d9-8538-7e43959501ce)


There is an object with javascript code in object[3] and we can check it using pdf-parser tool from Peepdf toolkit.
![Código Javascipt](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/ff1c87fb-8fd1-4d25-950a-e32317b47257)


I have renamed the file to have it more at hand.

![Renombrado PDF injectado](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/65fa1026-790b-486d-bd94-32970d0d6b3f)


We upload the file in Assets:

![Subir PDF en Assets](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/19ce93bf-d8ac-400e-ac6e-e245d4da07cc)


And when we open it we have the XSS of the PDF file stored on the server.

![Resultado XSS cockpit](https://github.com/sromanhu/CockpitCMS-File-Upload--XSS---Assets/assets/87250597/f3ae8c01-2eee-416c-bba4-13b4c3e6c342)


</br>

### Additional Information:
https://getcockpit.com/
