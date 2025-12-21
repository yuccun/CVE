## Product Vendor
https://github.com/xnx3/wangmarket

## Affected Product Code Repository:
wangmarket <= v6.4

## Vulnerability Type
Stored XSS

## Vulnerability Description
The /sits/uploadImage.do endpoint allows the uploading of XML files by default. Stored XSS can be achieved by uploading a malicious XML file.

## Vulnerability Proof
Upload an XML file with the following content: <svg xmlns="http://www.w3.org/2000/svg" onload="alert(1);"/>
<img width="1740" height="1244" alt="image" src="https://github.com/user-attachments/assets/0ec9a881-c388-41be-a3a6-ae939e770556" />

Access the uploaded XML file. The specified JavaScript statement is executed, resulting in XSS.
<img width="2332" height="1420" alt="image" src="https://github.com/user-attachments/assets/e81fbe96-4c9e-4abb-8eef-54fc51067c97" />


## Code analysis
In the uploadImage function, the file extension is validated via the isAllowUpload function.
<img width="1582" height="1264" alt="image" src="https://github.com/user-attachments/assets/d4c510f2-a712-4bdf-86f5-3ba2ecf01577" />

The isAllowUpload function allows the uploading of XML files by default.
<img width="2076" height="92" alt="image" src="https://github.com/user-attachments/assets/7ebdf01f-1a61-4abb-8bac-1f303b32b290" />

<img width="1634" height="1110" alt="image" src="https://github.com/user-attachments/assets/35897e0e-759d-4fa3-8346-092edd959644" />
