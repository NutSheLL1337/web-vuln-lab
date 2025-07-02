> ⚠️ **Disclaimer**  
> This project is for **educational and ethical hacking purposes only**.  
> Do **not** use the techniques shown here against any systems you do not own or have explicit permission to test (e.g. through a bug bounty program).

# bWAPP Web Pentesting Lab

> **Objective:** Demonstrate exploitation of OWASP Top 10 vulnerabilities using bWAPP on a local Kali Linux setup.

---
**Note:** This is done only for educational purposes and should not be used to exploit real sites without permission or a bug bounty program. 

## 🖥️ Lab Environment

- **Host OS:** Kali Linux VM (VirtualBox)
- **Target App:** bWAPP
- **Tools Used:** Burp Suite, OWASP ZAP, sqlmap, browser DevTools, curl

---

## 🔍 Overview of Findings

| OWASP Top 10 Category            | bWAPP Module Used           | Status     |
|----------------------------------|-----------------------------|------------|
| A1 – Injection                   | SQL Injection (GET)         | ✅ Exploited |
| A2 – Broken Authentication       | Brute Force (Login)         | ✅ Exploited |
| A3 – Sensitive Data Exposure     | Cleartext Passwords         | ✅ Observed  |
| A4 – XML External Entities (XXE) | XML Injection               | ✅ Exploited |
| A5 – Broken Access Control       | File Inclusion              | ✅ Exploited |
| A6 – Security Misconfiguration   | Default Credentials         | ✅ Exploited |
| A7 – Cross‑Site Scripting (XSS)   | Reflected & Stored XSS      | ✅ Exploited |
| A9 – Components with Known Vulnerabilities | Outdated PHP Modules | ✅ Exploited |

---

## 📝 Detailed Findings

### A1 – SQL Injection

1. **Attack Vector:** Injected `' OR '1'='1` into the `id` parameter  
2. **What happened:** Retrieved databases' information via UNION queries using SQLmap.  
3. **Screenshots:**  
![command_sqlmap](https://github.com/user-attachments/assets/3f6b5a25-11ce-466d-b00a-21a6bab845c2)
![Found_vuln_web_app](https://github.com/user-attachments/assets/8cf5cd1e-d4ca-4e31-8952-bf0ae1681436)
![test_on_site](https://github.com/user-attachments/assets/971ac420-d63f-4a9d-b992-efdfbc114941)

---

### A2 – Broken Authentication & A6 – Security Misconfiguration

1. **Attack Vector:** Automated username/password brute force using OWASP ZAP in a login page. 
2. **What happened:** Discovered valid credentials `admin:admin` by iterating the default creds list  
3. **Screenshots:**
![Brute_force_vulnerable_site_Fuzz](https://github.com/user-attachments/assets/7ac01187-2309-4ca6-baca-eedc71d63b5f)


---

<!-- Copy this block for each vulnerability you want to document -->

### A3 – Sensitive Data Exposure

1. **Attack Vector:** Plaintext transmission of credentials over HTTP  
2. **What happened:** Captured /etc/passwd directory and all credentials of a vulnerable web page. 
3. **Screenshots:**  
 ![Sens_data_exposure](https://github.com/user-attachments/assets/2823da95-b433-4bf5-8a79-c3ccc72087cb)
 

### A7 – Cross‑Site Scripting (XSS, Reflected, Stored, DOM)

1. **Attack Vector:** Exploitation of XSS injection into a vulnerable app. 
2. **What happened:** Manual Injection of JavaScript alert using available inputs and capturing requests with further automated injection via OWASP ZAP. 
3. **Screenshots:**  
![Stored_XSS_medium_lab1](https://github.com/user-attachments/assets/59284d7d-f705-4dde-bd7f-b9243607cd4d)
![Stored_XSS_lab1](https://github.com/user-attachments/assets/5f692e89-2cfb-4bb7-a3d1-606864e48ea4)
![Stored_XSS_Owasp_Zap](https://github.com/user-attachments/assets/1b15a5d2-ed84-403f-8e60-d748617a0774)
![Owasp_zap_XSS](https://github.com/user-attachments/assets/17fda384-b69a-4c68-8f38-19b91be6768a)


---

## 🔒 Mitigations & Recommendations

- **Use Prepared Statements and Input Validation** to prevent SQL injection 
- **Enforce Strong Password Policies** and implement account lock‑out for more than X requests
- **Enable HTTPS/TLS** to encrypt sensitive data in transit  
- **Sanitize and Validate All Input** to eliminate XSS and XXE  
- **Keep Components Up to Date** (PHP, Apache modules, dependencies)  

---

## 📂 Repository Structure

