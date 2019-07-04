**Python Development Environment Setup: **

**Windows 10, Windows Subsystem for Linux, Ubuntu, VS Code**

<u>Why this setup?</u>

I use computers running Microsoft Windows 10 as my primary machines.  I'm currently enrolled in the RMOTR Python / Django training program (it's great by the way).  In that program you are provided an interesting remote development environment (Notebooks.io).  However, I wanted to go ahead and get a proper local development environment setup.  I also wanted that environment to work well with the normal tooling RMOTR uses (such as make files etc).  

Getting all that to behave directly on my Windows 10 machine proved to be a bit of a pain.  So, I decided to see if I could setup an environment that would let me leverage Linux (Ubuntu 18.04 in my case) running under Windows Subsystem for Linux (WSL) to leverage some of the new [remote code](https://code.visualstudio.com/docs/remote/wsl) features of VS Code.



<u>Did it work?</u>

Yes, for my purposes, what is outlined below seems to be working fine for me.



<u>How did you set things up?</u>

I'm glad you asked.  I'm writing this 99% for myself...but if it helps someone else that is awesome!



<u>*Windows Setup:*</u>

- Click start - type "Turn Windows", click on "Turn Windows features on or off".
- Scroll to the bottom and click the check box for Windows Subsystem for Linux.
- Click Ok.
- Reboot as prompted.
- After you reboot, open the Windows Store.
- Search for Ubuntu and install the 18.04 LTS version.
- Click launch set your username and password etc.
- [Reference](https://docs.microsoft.com/en-us/windows/wsl/install-win10)



<u>*VS Code Setup:*</u>

- Download and install [VS Code](https://code.visualstudio.com/).
- Install the [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension.
- Install the [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) extension.



<u>*Linux Housekeeping:*</u>

- This section needs work.
  - Update
  - Install / verify needed packages.



<u>*Virtual Environments / Code Storage:*</u>

This next section assumes you are going to follow some configuration conventions I have decided to embrace.  They are:

- All code is going to be stored in a subdirectory of my home directory `(/home/dwinslow`) named `code`.
- All virtual environments are going to be stored in a subdirectory of my home directory `(/home/dwinslow`) named `envs`.
- The name of the subdirectory for my virtual environment and the subdirectory for my code will be stored in folder names that match the GitHub repo name for that code.  So, if my GitHub repo was named `test-project`...
  - My virtual environment for that project would be stored at: `/home/dwinslow/envs/test-project`
  - My repo would be cloned locally into `/home/dwinslow/code/test-project`

Make sense?  If so, here is how to set this up.

- Open your WSL / Ubuntu environment
  - You should have a Ubuntu icon in your start menu at this point.
- Type: `cd` 
  - This will change directory to your home directory.  For example, mine is `/home/dwinslow`
  - You can verify this by running `pwd`.  Pwd prints your working (current) directory.  Mine shows /home/dwinslow

- Type: `mkdir code` 
  - This is the folder we will store all our code in.
- Type: `mkdir envs` 
  - This is the folder we will store virtual environments in.

That sets up the shell we need.  The next sections deal with how to setup and work on a project.



*<u>Per Project: Virtual Environment Setup:</u>*

This section can be completed once per project to get it setup with a virtual environment etc.

- cd into your envs folder.  In my case I would type `cd /home/dwinslow/envs` 
  - This gets us into our top level envs directory.
- Type `python3 -m venv test-project`.  Replace test-project with your project name.  If you are following my convention, this will match the name of the GitHub repo you are about to clone.
  - This makes a new Python virtual environment named "test-project"
- Next, you can activate this virtual environment by running `source /home/dwinslow/test-project/bin/activate`. Replace `dwinslow` with your username and `test-project` with your environment name.
- This activates your new virtual environment.  You should see your command prompt change 
  to include your environment name.  



*<u>Per Project: Get our code ready to work on:</u>*

Now that we have our virtual environment active and ready, we can clone our code and install our requirements.

- cd into your code folder.  In my case I would type `cd /home/dwinslow/code` 
  - This gets us into our top level code directory.
- Clone the GitHub repo you want to work on.  If I wanted to clone my test project I would type `git clone https://github.com/wdwinslow/test-project.git`
- Git will clone this repo into a local folder named `/home/dwinslow/test-project`
- Now, we can cd into that folder and install our requirements.  In my case, I would type `cd /home/dwinslow/code/test-project`.  Obviously, your path may vary.
- Once you are in the folder where your code lives you can type `pip install -r requirements.txt`.  This will install all the things you need for this project, as defined in the requirements.txt file.



<u>*Per Project: Can we please write some code already?:*</u>

Now that all the prep work is done, we can get down to actually writing code.  In order to do that with VS Code, you can simply type `code .`  Don't miss the `.`

- The first time you do this, some stuff runs on the Linux side, and you might get some permissions prompts on the Windows side.  Just ok your way through that stuff.
- Poof!  VS Code will now be open and ready for your to edit code that lives over on the Linux / WSL side of your machine.



*<u>Per Project: Git commands to push your changes:</u>*

- Once you are done writing code use these commands to commit your code back to the GitHub repo.
  - Make sure you are in the correct location.  In my case this is `/home/dwinslow/code/test-project`.
  - Type `git add .`
    - This adds the files that have changed.
  - Type `git commit -m "Your message here"`
    - This adds a commit.
  - Type `git push`
    - This pushes your changes up to the GitHub repo.
    - You will be prompted for credentials.
    - If you use 2FA on your GitHub account, you can create a [personal access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line) and use it when prompted for your password.  There may be a better way...but I've not found it yet.



*<u>Per Project: Cleanup:</u>*

Once you are done, you might want to deactivate your virtual environment. You can do that by simply typing: `deactivate`.  Your command prompt will return to normal.

You might also like to unhook VS Code from what you were working on.  To to that go to `File` - `Close Remote Connection`.



*<u>Questions I still need to answer / document:</u>*

- How well does VS Code debugging work with this setup?
  - Related: How does VS Code deal with the virtual environments?  For now, I'm running all of my terminal commands over in the Linux environment directly.