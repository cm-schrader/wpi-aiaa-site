# wpi-aiaa-site
 This is a website and wiki for WPI AIAA.  It is written using Django.
 
 ## Development
 To develop the site on your computer, you must first have Python 3.6 or greater installed.
 
 The first step is to clone the repository using Github desktop or whatever your prefered cloning method is.  Following this, navigate to the project directory ```wpi-aiaa-site``` and open a command prompt or powershell window.
 
 First you must create a virtual environment.  This can be done with the following command.  
 ```
 python  -m venv env
 ```
 
 Next, start yoru virtual environment.  After you do this, you should see ```(env)``` at the start of each command line.  You will need to do this everytime you want to run the test server.  
 ### On Windows
 ```
 cd env/Scripts
 activate
 cd ../..
 ```
 ### On Linux or Mac
 ```
 source env/bin/activate
 ```
 
 Next install the python dependencies using the following command.
 ```pip install -r requirements.txt```
 

For essier debuging, enable DEBUG in the settings.  To do this, navigate to ```wpiaiaasite/wpiaiaasite/settings.py``` and set DEBUG to ```True```.  
**Do not push this change to the server as this would create a security issue.**
 
 You should now be able to run the test server.  This hosts the website on your local machine for development.
 ```python wpiaiaasite/manage.py runserver```

## Deploying To aiaa.wpi.edu
To deploy to aiaa.wpi.edu, you must virst be on a computer on WPI's network.  You can either use a physical on campus computer or use remote desktop to connect to a virtual machine like windows.wpi.edu.  Once on a computer, open powershell (command prompt does not work for this) and enter the following command to ssh into aiaa.wpi.edu.
```ssh administrator@aiaa.wpi.edu```
When prompted, enter the admin password.

Next, enter the website directory.
```cd wpi-aiaa-site```

From here, pull all of your changes from Github.
```git pull```
In some cases, there may have been changes on the server.  You can force pull using the following commands.  **Note, this overwrites anything on the server.  Save any changes you actually want to keep**
```
git fetch --all
git reset --hard origin/master
```

Next collect all static files that have been changed.  To do this, you must activate the virtual environment.
```
source env/bin/activate
python wpiaiaasite/manage.py collectstatic
```

Finally, restart the server to load your changes.
```
sudo service apache2 restart
```
