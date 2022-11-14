# How to upgrade Frappe & ERPnext v13 to Frappe & ERPnext v14
In this I am trying to give the appropriate solution of how we can upgrade frappe v13 to frappe v14

### As there are 13 Steps to upgrade v13 to v14:-

1- Take backup.
2- Make sure you don't have any customization those are not committed.
3-Check python version
4-check node version.
5-Check pip or pip3 version ( needs to be upgrade to 22.x )
6- Upgrade python
sudo apt install software-properties-common -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.10 python3.10-dev python3.10-distutils

Make Python 3.10 the default.
sudo update-alternatives --install /usr/bin/python3 python3
/usr/bin/python3.10 1
Make sure python command executes python3
sudo apt install python-is-python3

7 - Upgrade PIP
curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10
pip install html5lib
pip3 install --upgrade pip
sudo apt-get remove python3-apt -y
sudo apt-get install python3-apt -y

At the Step 8 I am getting an error while upgrading the version of
node.Which is resolve by the command nvm install node.

Instead of following command :-

8- Upgrade Node
curl -sL https://deb.nodesource.com/setup_16.x | bash -
apt-get install nodejs redis-server -y

I am using the following commands:-
nvm install node
sudo apt-get install redis-server

9- Upgrade NPM
npm upgrade
sudo npm install 16
sudo npm install -g npm@8.19.1

10 -Move your old python env folder to env-archive, in-case anything
goes wrong, you can return to the original
/home/simran/frappe-bench/
mv env env-archive
(Please check your frappe bench path)

11- Create new virtual env for python-3.10
pip install virtualenv
virtualenv --python python3.10 env
env/bin/pip install -U pip

I was getting an error while running the second command so I created
the virtual environment by the following command:-
bench setup env

12- Change git upstream from V13 to V14
env/bin/pip install -e apps/frappe -e apps/erpnext
pip3 install frappe-bench
bench switch-to-branch frappe erpnext version-14
(This command take my half an hour and after that gave me an error so
I run the below command instead of this)

bench switch-to-branch version-14 frappe erpnext --upgrade

13-bench --site v13.erpgulf.com migrate
This command works only when the bench is start.

After completing all the steps I am facing the following problem:-
https://github.com/Simranjeet7860/Demo-Image/blob/main/pp.png

This error is resolved by removing the line
"maintenance mode":1
from common_site_config.json

After completing all the steps I get the following result.
https://github.com/Simranjeet7860/Demo-Image/blob/main/Screenshot%20from%202022-11-14%2014-39-51.png
