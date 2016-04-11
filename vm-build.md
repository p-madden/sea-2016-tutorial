## VM Build Recipe

1. Install Debian 8.3 (32-bit, ssh server, no desktop components)
  - Problems were observed running 64-bit VMs on Windows
  - Create user jupyter w/ password jupyter
2. Set up VirtualBox port forwarding for new VM
  - Mandatory: host (e.g.) 8888 -> guest 8000
  - Optional: host (e.g.) 2222 -> guest 22
3. (as root) apt-get update && apt-get upgrade
4. (as root) apt-get install emacs24-nox git nodejs-legacy npm ruby sudo unzip
5. (as root) visudo, add jupyter with all privileges
6. (as root) Install Anaconda 3 (32-bit) to /opt/anaconda3
7. (as root) Add /opt/anaconda3 to PATH in /etc/bashrc.bashrc
8. (as root) pip install --upgrade pip
9. (as root) [Install jupyterhub](https://github.com/jupyter/jupyterhub/blob/master/README.md)
  - Do not install pip3: Anaconda provides it as 'pip'
10. (as root) Add to /etc/rc.local:
  `PATH=/opt/anaconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin jupyterhub --config=/etc/jupyterhub/jupyterhub_config.py &`
11. (as root) mkdir /etc/jupyterhub && cd /etc/jupyterhub
12. (as root) jupyterhub --generate-config
13. (as root) emacs juputerhub_config.py
  - c.JupyterHub.confirm_no_ssl = True
  - c.JupyterHub.extra_log_file = '/var/log/jupyterhub.log'
  - c.JupyterHub.pid_file = '/etc/jupyterhub/pid'
14. (as jupyter) cd && git clone https://github.com/p-madden/sea-2016-tutorial.git
15. Reboot
