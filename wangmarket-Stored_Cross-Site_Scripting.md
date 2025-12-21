## Product Vendor
https://github.com/xnx3/wangmarket

## Affected Product Code Repository:
wangmarket <= v6.4

## Vulnerability Type
Stored XSS

## Vulnerability Description
The /siteVar/save.do endpoint is vulnerable to XSS. After logging in with the credentials wangzhan/wangzhan, injecting an XSS payload into the 'Remark' or 'Variable Value' fields during the 'Add Global Variable' operation and saving it results in Stored XSS upon subsequent access.

## Vulnerability Proof
<img width="2330" height="1286" alt="image" src="https://github.com/user-attachments/assets/11b6bcbc-f865-4995-9a33-db55c562a2bf" />
<img width="2326" height="1326" alt="image" src="https://github.com/user-attachments/assets/7a03cf34-d6b0-4739-bc4e-340a5eeb739f" />
<img width="2338" height="1334" alt="image" src="https://github.com/user-attachments/assets/efdf1398-45e3-4210-983b-1d879d4e7c63" />




