# HIGH risk vulnerabilities in Siemens PLCs —S7+:Crash

# Overview

On February 8, 2022, Siemens issued a new round of security advisories, among which 3 vulnerabilities related to SIMATIC products were submitted by me(@ic3sw0rd ). From August 2021, I submitted several vulnerabilities regarding SIMATIC products. After many in-depth and friendly conversations with Siemens, it finally issued a advisory including 3 vulnerabilities on February 8,2022 (the remaining vulnerabilities are still under investigation). These vulnerabilities, given the name **S7+:Crash**.
Currently the vulnerability is ranked HIGH with a CVSS3.1 score 7.5. These vulnerabilities may cause serious consequences, such as remote denial of service for SIMATIC controllers.



# Vulnerability Overview
Details related to **S7+:Crash** are described as follows:


**CVE-2021-37185**
Operation on a Resource after Expiration or Release (CWE-672)
An unauthenticated attacker could cause a denial-of-service condition in a PLC when sending specially prepared packets over port 102/tcp. A restart of the affected device is needed to restore normal operations.
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H/E:P/RL:O/RC:C



**CVE-2021-37204**
Operation on a Resource after Expiration or Release (CWE-672)
An unauthenticated attacker could cause a denial-of-service condition in a PLC when sending specially prepared packets over port 102/tcp. A restart of the affected device is needed to restore normal operations.
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H/E:P/RL:O/RC:C



**CVE-2021-37205**
Missing Release of Memory after Effective Lifetime  (CWE-401)
An unauthenticated attacker could cause a denial-of-service condition in a PLC when sending specially prepared packets over port 102/tcp. A restart of the affected device is needed to restore normal operations.
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H/E:P/RL:O/RC:C

It is worth noting that although these three vulnerabilities described in the official Siemens advisory, they result from different functions. There are more than ten categories of functions in S7CommPlus protocol, and different categories have corresponding operating objects. Each function can only be triggered in certain conditions.


# Affected products

Siemens is the world's leading company in the field of electrical engineering whose products is a mainstream in the field of industrial control equipment, widely used in electric power industry, petroleum and petrochemical, rail transportation, intelligent manufacturing, iron and steel metallurgy, and other critical infrastructures in the global scope. The market share of automation equipment ranked first. Multiple vulnerabilities discovered this time affect the following products:

 ![图片描述](https://bbs.pediy.com/upload/attach/202202/907750_3QUFU7H365GCEGQ.png) 
 
These products covers many Siemens industrial automation fields, such as drive controllers, S7-1200/S7-1500, PLC simulators, distributed controllers, soft PLCs, etc.




# Vulnerability details

Due to the leading position in the market, Siemens PLCs have been major research targets, which result in many vulnerabilities being found over the years. Historical ones like CVE-2010-2772(used in Stuxnet), CVE-2019-10943(used in Rogue7 attack), CVE-2019-13945(physically attacks SIMATIC 1200 to achieve code execution), CVE-2020-15782(sandbox escape, can be used to directly access memory and lead to code execution). These vulnerabilities although can cause code execution, but with multiple preconditions. CVE-2020-15782 will require a PLC download permission, otherwise the attack cannot be achieved. CVE-2019-13945 has to enable physical access and cannot be exploited remotely. S7+:Crash have the following characteristics compared with previous vulnerabilities:

## 1. Multiple vulnerabilities in OMS+ communication protocol stack

The previous Siemens PLC vulnerabilities are found independently whereas this time they are discovered in batch. Up to now, there have been 5 vulnerabilities repaired and several more will be addressed in the future. These 5 vulnerabilities are found in OMS+， the core component of Siemens S7 communication protocol, which is used in several Siemens products to implement its private protocol. The following screenshot displays the OMS+ information used in the S7-1200 series V4.5.1 firmware. The updated version is V4.5.2 and the OMS+ version is 12.35.8.

 ![图片描述](upload/attach/202202/907750_7S472HA42HKS6C6.png)
OMS+ information used in V4.5.1 firmware

 ![图片描述](upload/attach/202202/907750_DDF8U25B6FMXT82.png)
OMS+ information used in V4.5.2 firmware


## 2.Even with the access protection policy enabled, the PLC can still be remotely attacked which will cause the device to crash

Two of the vulnerabilities disclosed this time can still lead to a remote attack even with the PLC access protection strategy enabled. The purpose of the access protection policy is to prevent unauthorized sensitive operations and there are multiple levels of access control protection in Siemens SIMATIC PLC series, as shown in the screenshot below:

 ![图片描述](upload/attach/202202/907750_PM8HXSS3R8F8H3C.png)
Even with the highest level enabled (complete protection), the attack can still succeed.

## 3.	These vulnerabilities can be exploited regardless the secure communication function(TLS encryption communication) is enabled or not
In May 2021, Siemens released the firmware version V4.5.0 (S7-1200) and TIA V17, which introduced the secure communication mechanism, aiming to make the communication in the industrial scenario more secure and reliable. Even with this new secure mode enabled, the vulnerability will cause the PLC ending up in a critical failure state. Currently, traditional security products like firewalls or other intrusion detection systems do not support this Siemens secure communication protocol, which means most of the attacks cannot be identified. The best countermeasure is to upgrade the firmware to the latest version.

 ![图片描述](upload/attach/202202/907750_ZCUZ5YFXP3T2RNX.png)

# Mitigations and solutions

The following suggestions are given by Siemens:

1.For affected products with the latest firmware version already released, upgrade the firmware to the latest version.

2.For affected products with the latest firmware version not released yet, apply Siemens general safety recommendations(https://cert-portal.siemens.com/operational-guidelines-industrial-security.pdf)


# Summary

The three vulnerabilities disclosed this time are critical with wide impact, low exploitation difficulty and high protection difficulty. Users and companies should be alerted and take necessary measures to avoid industrial production being affected.
Research on Siemens S7 communication protocol will continue, facing more and more complicate attack scenarios. Not only should the end users strengthen key equipment in industrial control system, manufacturers should also start from the origin to improve the security of their products. 
Siemens is a company which attaches great importance to its product security. During the communication with Siemens, its responsible and professional attitude sets a great example which are worth learning by all manufacturers in the whole industry.


# Appendix

1.	Siemens CERT :
https://new.siemens.com/global/en/products/services/cert.html#SecurityPublications
2.	Links to security advisory：
https://cert-portal.siemens.com/productcert/pdf/ssa-838121.pdf 

# Vulnerability demos

Demonstration video of a password-protected S7-1500 PLC affected by the vulnerability.

https://www.youtube.com/watch?v=XNDo0iAaT14 

