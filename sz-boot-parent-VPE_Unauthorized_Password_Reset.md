## Product Vendor
https://github.com/feiyuchuixue/sz-boot-parent

## Affected Product Code Repository
sz-boot-parent <= v1.3.2-beta

## Vulnerability Type
Vertical Privilege Escalation - Reset Other Users' Passwords

## Vulnerability Description
For the API `/api/admin/sys-user/reset/password/{userId}`, users with ordinary permissions can reset the passwords of other users—a function that should only be executable by administrators. The passwords will be reset to the default value **sz123456**.

## Vulnerability Proof
Users with ordinary permissions cannot access the user management page.
<img width="2646" height="1266" alt="图片" src="https://github.com/user-attachments/assets/b9070bf0-0bcb-4a59-a60a-d5ceaf6bfa05" />

However, they can access the API and reset the passwords of any users to sz123456 at will.
<img width="2378" height="1086" alt="图片" src="https://github.com/user-attachments/assets/4ef9cd93-4c5d-47c2-bcc6-3e47e1553a71" />

