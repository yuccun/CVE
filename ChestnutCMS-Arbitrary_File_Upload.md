## Product Vendor
https://github.com/liweiyi/ChestnutCMS

## Affected Product Code Repository:
ChestnutCMS <= v1.5.8

## Vulnerability Type
Arbitrary File Upload

## Vulnerability Description
In the `/dev-api/common/upload` endpoint, there is a flaw in the file extension extraction logic before the `FilenameUtils.getExtension` method is called. The system performs a special parsing operation on the file path to extract the suffix. If the filename contains specific characters (`://` and `wx_fmt=`), the logic extracts the value between `wx_fmt=` and `&` (or the end of the string) as the file extension. Attackers can manipulate this behavior to bypass file extension restrictions.

## Vulnerability Proof
1. Log in to the system to obtain a valid session/token, then access the `/dev-api/common/upload` endpoint.
2. Use the `multipart/form-data` format for the request.
3. Modify the `filename` parameter to `://?wx_fmt=txt.xxxxx` (e.g., `://?wx_fmt=txt.html`).
4. This payload allows the upload of arbitrary file types
<img width="1732" height="984" alt="image" src="https://github.com/user-attachments/assets/d24d61ca-132a-4a93-8fe8-97c5ca787cbb" />
<img width="1724" height="1030" alt="image" src="https://github.com/user-attachments/assets/2d54c4ed-3989-4628-87a2-47b752ec36f2" />
<img width="1358" height="341" alt="image" src="https://github.com/user-attachments/assets/45d7a7da-2323-4592-9b76-a95d1e5b8cdc" />
5. Additionally, directory traversal is partially possible. Although the file name is a randomly generated UUID—preventing the creation of files with arbitrary names in arbitrary locations—it allows creating empty directories with specified names in the target path.
<img width="1720" height="840" alt="image" src="https://github.com/user-attachments/assets/7e8688a5-999c-45c6-b8ae-57ea4406785b" />
<img width="1106" height="316" alt="image" src="https://github.com/user-attachments/assets/7654a8df-1538-4743-af83-6fdb4c2f73e6" />

## Code analysis
<img width="1772" height="1294" alt="image" src="https://github.com/user-attachments/assets/04591007-ed26-46a3-9558-57065ce34f71" />
1. The method responsible for extracting the file extension contains a special conditional check.
2. If the filename contains `://` AND `wx_fmt=`, the system extracts the substring between `wx_fmt=` and `&` as the file extension.
<img width="1772" height="1294" alt="image" src="https://github.com/user-attachments/assets/dba37d28-1540-4e53-a908-cbf3b2e10a39" />
<img width="1370" height="732" alt="image" src="https://github.com/user-attachments/assets/f9522cab-2953-4096-9bac-1b0e2c9dd128" />
3. The security check method `SysUploadTypeLimit.check` validates this extracted extension against the whitelist.
<img width="1664" height="852" alt="image" src="https://github.com/user-attachments/assets/3482f66f-26fe-45d1-8157-1b1c701a619d" />
<img width="1932" height="754" alt="image" src="https://github.com/user-attachments/assets/e47fefb8-6d4d-4093-a089-0daefe3ba7a8" />
4. By setting the filename to `://?wx_fmt=txt.xxxx`, the extracted extension is `txt`, which is in the whitelist. Consequently, the check is bypassed, allowing the upload of the actual file (e.g., `.xxxx`).
