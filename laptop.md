## Setting up a laptop
https://helpdesk.it.helsinki.fi/en/instructions/computer-and-printing/workstation-administrator-rights

# cubbli managed Ubuntu laptop
Login and ask for administrative rights with [this](https://elomake.helsinki.fi/lomakkeet/42471/lomake.html) form.

# Lenovo T480
Physical device for installation found in the lab drawer.
[Here](https://download.lenovo.com/pccbbs/mobiles_pdf/thinkpad_p43s_p53s_ubuntu_installation_whitepaper_v1.0.pdf) is guide for the installation and setting up the graphics card.

- Before you can download and setup the graphics you need to setup [eduroam](cat.eduroam.org). Download the `.py` file and run it in terminal with command
``` python3 ~/Downloads/eduroam-linux-UoH-Username_and_password_authentication-py```
- Setup graphics drivers following the guide. (GeForce MX150)
- Install updated as prompted by the window. 
- Connect to Nextcloud datacloud (username no @anything)
- Install code and other software
```
sudo snap install --classic code
sudo apt-get install wget # what else might you desire
```


