

### Vulnerability details


**9.1 (Critical). CVSS string: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N**



TDSEE is a mobile application for managing Tenda smart cameras. At the time of writing the review (06.06.2025), the application has been downloaded more than 500,000 times.

In the TDSEE app, I found there was no rate limit in the confirmation code requests in the password reset functionality, resulting in account takeover.

Knowing the victim's email, the attacker could change the account password by going through the 6-digit password reset confirmation code.

![](https://raw.githubusercontent.com/k3vg3n/researches/refs/heads/main/attachments/Account_takeover_in_TDSEE_app/burp_check_code_success_wm.png)

### PoC



https://github.com/user-attachments/assets/9b45d47d-b75b-4f8f-b402-77f9266482b0



### Patch

**The vendor has been notified of the vulnerability. The vulnerability has already been fixed.**
In the application version 1.7.15, the vendor released a patch, setting a limit on the number of requests per second.

### Author

[@k3vg3n](https://t.me/k3vg3n)

[blog.kevgen.ru](https://blog.kevgen.ru/posts/account_takeover_in_tdsee_app/)















