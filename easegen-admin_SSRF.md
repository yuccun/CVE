## Product Vendor
https://github.com/taoofagi/easegen-admin

## Affected Product Code Repository
easegen-admin <= commit 8f87936

## Vulnerability Type
SSRF


## Vulnerability Description
The `/admin-api/digitalcourse/courses/docparse` endpoint is vulnerable to Server-Side Request Forgery (SSRF). This vulnerability is caused by the direct usage of `new URL(wordFileUrl).openStream();`. It can be exploited by any logged-in user.

## Vulnerability Proof
Include the target URL within the `fileUrl` parameter. The URL is required to end with `.docx`; this check can be bypassed by appending `#.docx` to the URL. Since the source code utilizes the standard Java `URL` class, various protocols (e.g., http, file, jar) can be used. The parameter `"type": "text"` is optional (it can be included or omitted). 
<img width="1462" height="502" alt="image" src="https://github.com/user-attachments/assets/ddd498b6-6c60-435c-88df-80a0acbbcfd2" />
<img width="2440" height="1580" alt="image" src="https://github.com/user-attachments/assets/428a9bfd-896f-4aac-b290-c79bdabb3738" />


## Code Analysis

**File Location:** `yudao-module-digitalcourse/yudao-module-digitalcourse-biz/src/main/java/cn/iocoder/yudao/module/digitalcourse/controller/admin/courses/AppCoursesController.java`

The controller calls the `recognizeMarkdown` method: 
<img width="1768" height="1034" alt="image" src="https://github.com/user-attachments/assets/1e2f23f7-2e73-48f2-aa0b-80749add1264" />


When `fileUrl` ends with `.docx`, the code proceeds to call `extractTextFromWord(fileUrl)` (if `type` is set to "text") or `convertWordToPdf(fileUrl)`. Both of these functions internally execute `new URL(wordFileUrl).openStream();`, which triggers the request. 
<img width="2442" height="1580" alt="image" src="https://github.com/user-attachments/assets/daed0bfd-d8f6-46af-91b7-ef7ed6903422" />
<img width="1736" height="304" alt="image" src="https://github.com/user-attachments/assets/8b870238-44ab-47bb-a07e-f3bad938cf26" />
<img width="1468" height="1128" alt="image" src="https://github.com/user-attachments/assets/62d14c62-15df-4bbe-842a-4f697b110c71" />
