# SSH setup in Visual Studio Code - Key Based Authentication

#### Install Visual Studio Code software in your local machine. Refer the links below to download and install Visual Studio Code.

Download: Depending on which OS you are using select the supported version. [https://code.visualstudio.com/download](https://code.visualstudio.com/download)

#### Installation Steps:

- [https://code.visualstudio.com/docs/setup/windows](https://code.visualstudio.com/docs/setup/windows)
- [https://code.visualstudio.com/docs/setup/mac](https://code.visualstudio.com/docs/setup/mac)
- [https://code.visualstudio.com/docs/setup/linux](https://code.visualstudio.com/docs/setup/linux)

#### Remote Development using SSH:  


**Step 1:** Open Visual Studio Code in your local machine and install Remote-SSH extension by selecting extensions option in the left side nav bar as shown below.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/g0msPIPPAWXPqon3-image.png)

**Step 2:** Type Remote and select Remote - SSH extension, choose install after installation is completed the screen will appear as shown below.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/j6CSdm6Gri4gH84E-image.png)

### SSH key-based Authentication

**Step 1:** Open the Ubuntu Linux server to configure the SSH key-based authentication.

- Open the configuration file located in the root directory /etc/ssh/
- Only root and super user have access to edit the system files, in order to access and edit the config files login as root or use the `sudo` command.
- To edit use the `nano` editor. Type `sudo nano ssh_config` command and enter the password if the terminal asks user.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/iIl9K3seUDCxBp6I-image.png)

**Step 2:** Give permission to log in as a root user.

- - Add the line '`PermitRootLogin yes`' after the `# Aythentication`.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/coXjNoapbQqfV3vq-image.png)

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/A777jSdCAO35Em2V-image.png)

- Scroll down using the Arrow keys on the keyboard to fetch the line `# To disable tunneled clear text passwords, change to no here!`
- After that Uncomment `#PermitAuthentication yes` by removing # and adding `no` instead of `yes` to disable the password-based authentication. Follow the screen 2.

**Screen 1:**

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/xpIpTlLUoKWP3VUX-image.png)

**Screen 2:**

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/prZve4P2fg6oONQ9-image.png)

- Use keyboard shortcut 'Ctrl + o' to save the file and 'Ctrl + x' to exit from the editor

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/JGpbuhfvb1nEVRFp-image.png)

- Restart the SSH server using the command `sudo service ssh restart` and it was shown in the above screen.
- Check the server status using the command `sudo service ssh status`, server will be in `an active (running)` state and it was shown in the below screen.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/YSly4v4DJ50oNDdk-image.png)

#### Sharing the public key into the remote server (Ubuntu Linux Server):

**Step 2:** To share the Public key we use `scp` command. SCP is the short form of Secure Copy Protocol. This command uses SSH keys or Secure Shell keys for the secure transfer of data.

**Step 3:** Remember, in order to copy the keys from the local machine to a remote machine, we need ssh keys present in the local machine also. Refer to the steps, already explained in [SSH setup in Ubuntu Linux Server](https://atlas.i.camp/books/linux-server-setup-manual/page/ssh-setup-in-ubuntu-linux-server).

**Step 4:** In the Windows search option type cmd and click on `Run as administrator`.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/345NMnUAMqBXheKh-image.png)

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/ql7Q2ilkkCROMgDM-image.png)

- Follow the on-screen commands to locate the ssh keys in your local machine.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/0KwBt7OW2EMDcWbg-image.png)

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/IqCq1HJdiJr9OIYX-image.png)

- From the above screen we can conclude that our local machine's public IP is copied into our Ubuntu Linux server's specified directory i.e, `~/.ssh/autherized_keys` exists in the home directory. Enter the root password if the terminal prompts the user.
- Below screen shows our public key is copied from local machine to remote machine.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/Pp1rP3NleSAabhty-image.png)

**Step 4:** Launch VS Code. Open the Command Palette (Cmd+Shift+P) and type 'Remote-SSH' to find the SSH Extension and select `Remote-SSH: Connect to Host`, and press enter as shown in the below screen.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/8T4mU6iyMyKfw9Zm-image.png)

**Step 5:** User can connect to the remote Host by using another option called `Open a Remote Window` which is shown in the below screen indicated with a circle.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/WPeTesdC3sMfmnKN-image.png)

**Step 6:** By clicking on `Open a Remote Window` button, the dropdown menu will appear on the screen as shown below and select Connect to Host option.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/RvwCv048wZlbkHkU-image.png)

**Step 7:** After Selecting Connect to Host, the user will be prompted to add a new SSH Host or Configure Host. Here user needs to choose `Add New SSH Host` Option and press Enter.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/RB6bTGzXPphA2nTV-image.png)

- Enter the host address following `ssh` command as shown in the below screen.
- Syntax: `ssh -i [path_for_local_machine_private_key_file_name] host_name@domain_name_or_IP`
- Here in our case type `ssh -i C:/Users/user/.ssh/id_rsa <a href="mailto:root@192.168.1.38">root@192.168.1.38</a>` and enter

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/CAqeBIZWtK5psMr5-image.png)

**Step 8:** After pressing enter, at the command palette prompt user need to select the first option as shown in the below screen.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/HAFkHezlcRRAXCc8-image.png)

- A popup will appear in the below right corner called a Host added! message asking to `Connect `or `Open Config` file.
- Here we will select the open config option to cross-verify the Host details that are added in .config file which is stored in .ssh folder on our local machine.
- Please check screen 2.

**Screen 1**

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/VsWYCfo8WMT6yFQS-image.png)

**Screen 2**

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/j7sRdJoQ4vxpBRJH-image.png)

**Step 9:** Save the config file and repeat from Step 5 to Step 8, after completing all the steps click on connect as shown on screen 1 in Step 8.

- User needs to select Linux because our remote host was Ubuntu Linux Server.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/aUSMhLgeG7GF7app-image.png)

**Step 10**: After clicking on connect button, the system will never ask password to login into the host machine. Users can directly connect to the remote host machine without using a password. As shown in the below screen we are in our remote Ubuntu Linux server Machine.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/beMESvva6l7TdZ6o-image.png)

**Step 11:** We can verify whether our connected remote machine is correct or not.

- Click on the Explorer button or use Ctrl + Shift + E.
- Open folder button will appear on the screen and check the server's directories.

![image.png](https://atlas.i.camp/uploads/images/gallery/2023-07/scaled-1680-/FyB7ZT8UaT31NHCf-image.png)

- Finally we are able to login into our remote machine using the Remote SSH extension in vs code without using a password.
