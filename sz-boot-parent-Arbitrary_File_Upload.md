## Product Vendor
https://github.com/feiyuchuixue/sz-boot-parent

## Affected Product Code Repository
sz-boot-parent <= v1.3.2-beta

## Vulnerability Type
Arbitrary File Upload

## Vulnerability Description
The API endpoint `/api/admin/sys-file/upload` contains a critical arbitrary file upload vulnerability with insufficient file type validation and filtering mechanisms in place; this security flaw enables unauthorized actors to upload arbitrary file types—including HTML, EXE and other high-risk file formats—to the target server without any effective restrictions.

## Vulnerability Proof
<img width="2354" height="1140" alt="图片" src="https://github.com/user-attachments/assets/e49a8674-6134-4a55-9467-a3980ef46fb0" />
<img width="2370" height="1212" alt="图片" src="https://github.com/user-attachments/assets/410916a6-11cd-4f80-b83d-227c8b0a2e21" />




