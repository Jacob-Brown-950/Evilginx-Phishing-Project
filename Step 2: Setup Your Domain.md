# 🌐 Step 2: Setup the Domain

In this step, I registered and configured the domain **Evilginxtest.shop** using **Namecheap**, pointing it to my VPS. This allows Evilginx2 to operate with custom SSL-secured phishing URLs and full DNS control.

---

## 🛒 Domain Registrar: Namecheap

The domain **Evilginxtest.shop** was purchased via [Namecheap](https://namecheap.com), which supports glue records and custom nameservers — both necessary for this lab setup.
![image](https://github.com/user-attachments/assets/2500c32f-f414-4532-9e28-9c91da984624)

---

## 📌 Domain Configuration Summary

- **Domain**: `Evilginxtest.shop`
- **Registrar**: Namecheap
- **Nameservers**: Custom (self-hosted)
- **DNS Records**: Glue records pointing to VPS

---

## 🧷 Glue Records & Custom Nameservers

To direct all DNS resolution through my VPS, I configured **glue records** on Namecheap that bind subdomains (`ns1` and `ns2`) to the public IP of the VPS.

### 🔧 Steps Performed in Namecheap:

1. **Navigate to**:  
   **Domain List → Manage → Advanced DNS**

2. **Create Host Records** (aka glue records):
   - `ns1.evilginxtest.shop` → VPS Public IP  
   - `ns2.evilginxtest.shop` → VPS Public IP *(same IP for both is fine for this lab)*
![image](https://github.com/user-attachments/assets/d44dd7ee-db8d-4393-b3ed-6f5d363bf3ac)
![image](https://github.com/user-attachments/assets/5f0e5bf9-4c94-4420-8670-c16927f4ae8f)

3. **Set Custom Nameservers**:
   - Go to **Domain → Nameservers**  
   - Select **Custom DNS**  
   - Enter:
     ```
     ns1.evilginxtest.shop
     ns2.evilginxtest.shop
     ```
![image](https://github.com/user-attachments/assets/7f970a78-0056-4652-b7f9-448d6ed730e6)



4. **Propagation Time**: Wait up to 10–15 minutes for changes to apply globally.

5. **Verification**:
   Use `dig` or `nslookup` to confirm:
   ```bash
   dig @ns1.evilginxtest.shop evilginxtest.shop
