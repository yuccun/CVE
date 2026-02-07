## Product Vendor
https://github.com/feiyuchuixue/sz-boot-parent

## Affected Product Code Repository
sz-boot-parent <= v1.3.2-beta

## Vulnerability Type
Arbitrary_Resource_File_Read

## Vulnerability Description
The API `/api/admin/common/download/templates?templateName=../application.yml` is vulnerable to **directory traversal**, which allows attackers to read arbitrary resource files on the server.

## Vulnerability Proof
<img width="2374" height="1174" alt="图片" src="https://github.com/user-attachments/assets/9f83176f-71f4-4136-8bfe-52096643dea2" />

## Code Analysis
In the `CommonServiceImpl.java` file, the `templateName` parameter is directly concatenated to the `templatePath` that starts with `classpath:/templates/` for resource acquisition. This improper parameter handling enables attackers to use the `../` sequence to break out of the `templates` directory, thereby gaining unauthorized access to and reading any resource file on the server.
<img width="1716" height="618" alt="图片" src="https://github.com/user-attachments/assets/4401c6cc-a98e-43c4-89af-d77973354171" />



