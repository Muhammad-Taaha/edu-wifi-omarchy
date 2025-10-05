2. Add this template inside

Paste this (replace identity and password with your university login):

[Security]
EAP-Method=PEAP
EAP-Identity=yourstudenremail
EAP-PEAP-Phase2-Method=MSCHAPV2
EAP-Password=yourpassword

3. Set correct permissions

iwd is strict about file permissions. Run:

sudo chmod 600 /var/lib/iwd/eduroam.8021x
sudo chown root:root /var/lib/iwd/eduroam.8021x
