## Product Vendor
https://github.com/feiyuchuixue/sz-boot-parent

## Affected Product Code Repository
sz-boot-parent <= v1.3.2-beta

## Vulnerability Type
Arbitrary_File_Read/SSRF
## Vulnerability Description
For the API `/api/admin/common/files/download`, **Server-Side Request Forgery (SSRF)** and arbitrary file read vulnerabilities can be exploited when the value of `oss.accessMode` is not set to **"private"**.

## Vulnerability Proof
The value of `oss.accessMode` can be modified in the parameter management module to a value other than `private`.
<img width="2338" height="1352" alt="图片" src="https://github.com/user-attachments/assets/77aa8d16-f848-4855-9845-612e53a40ab0" />

At this point, the **file protocol** can be used in the `url` parameter to read arbitrary files on the server.
<img width="2430" height="1252" alt="图片" src="https://github.com/user-attachments/assets/6f815232-c3b2-471b-853d-c2f5562200df" />

In addition, arbitrary protocols such as **http** can be used, leading to **SSRF with response disclosure**.
<img width="2384" height="1196" alt="图片" src="https://github.com/user-attachments/assets/277208c6-d45c-470a-85cb-e279a87c5723" />

## Code Analysis
In the `urlDownload` method of `CommonServiceImpl.java`, the `url` parameter is assigned to the `fileUrl` variable and then directly passed into the `new URL(fileUrl).openStream()` method without any protocol validation or filtering. This improper handling allows the use of URLs with arbitrary protocols, resulting in SSRF and arbitrary file read vulnerabilities.
There is a conditional check in the code that retrieves the value of `oss.accessMode`. If the value is `private`, the code modifies `fileUrl` to a signed URL. Therefore, an attacker needs to construct a non-`private` value for `oss.accessMode` to bypass this validation check.
<img width="2228" height="766" alt="图片" src="https://github.com/user-attachments/assets/a311ab7a-88e0-4959-b424-8f8087217bc4" />




