## Product Vendor
https://github.com/taoofagi/easegen-admin

## Affected Product Code Repository:
easegen-admin <= commit 8f87936

## Vulnerability Type
Arbitrary_File_Read


## Vulnerability Description

The `/admin-api/digitalcourse/courses/docparse` endpoint is vulnerable to **Arbitrary File Read**. This vulnerability is caused by the insecure usage of `Files.readAllBytes(Paths.get(new URL(fileUrl).getPath()))`. It can be exploited by any logged-in (authenticated) user.

## Vulnerability Proof

The vulnerability can be triggered using protocols that can be initialized by `new URL`, such as `file://` or `https://`. By crafting a `fileUrl` that ends with `.txt`, it is possible to read arbitrary files. 
<img width="2358" height="1232" alt="image" src="https://github.com/user-attachments/assets/cad38172-eeb7-4e26-9c8c-d4951c6d6f91" />


## Code Analysis

**File Location:** `yudao-module-digitalcourse/yudao-module-digitalcourse-biz/src/main/java/cn/iocoder/yudao/module/digitalcourse/controller/admin/courses/AppCoursesController.java`

The controller calls the `recognizeMarkdown` method: 
<img width="1462" height="502" alt="image" src="https://github.com/user-attachments/assets/61cfadbe-e338-45b9-99c9-eb2eea3f4dd4" />


When the `fileUrl` parameter ends with `.txt`, the application executes `Files.readAllBytes(Paths.get(new URL(fileUrl).getPath()))`. This logic extracts the path component from the URL and attempts to read the file from the filesystem. Therefore, submitting a payload like `http:///etc/passwd#.txt` (where `.txt` satisfies the check and the `#` acts as a fragment identifier to truncate the suffix during path processing in some contexts, or simply passing the path check while the URL parser extracts the path part `/etc/passwd`) allows reading arbitrary files on the server. 
<img width="1690" height="834" alt="image" src="https://github.com/user-attachments/assets/0bf1adf4-6ecf-4fd9-a8d8-05bc6d742f97" />
