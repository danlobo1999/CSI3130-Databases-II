# CSI 3130 - Lab 1

Class: CSI 3130
Created: September 19, 2022 12:59 PM
Type: Lab

# Lab 1 - Setting-up-PostgreSQL-on-your-own-machine

## This Lab is to be done in Linux

If you don’t have Linux installed, you can create a virtual machine by following the steps in this [tutorial](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview):

 [https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview).

## Steps to build and install postgresql v 8.1.7 from source code

1. Download the source code for postgresql-8.1.7 with this command (You can also download it from [https://www.postgresql.org/ftp/source/v8.1.7/](https://www.postgresql.org/ftp/source/v8.1.7/))
    
    ```bash
    wget https://ftp.postgresql.org/pub/source/v8.1.7/postgresql-8.1.7.tar.gz
    ```
    
2. Open the terminal and cd into the downloads directory
3. Type the following command to unzip the file
    
    ```bash
    tar xzf postgresql-8.1.7.tar.gz
    ```
    
4. To configure postgresql, a few libraries need to be installed:
    
    In the terminal type the following commands:
    
    ```bash
    sudo apt-get update
    sudo apt-get install make
    sudo apt-get install libreadline-dev
    sudo apt-get install zlib1g-dev
    sudo apt-get install clang
    ```
    

1. Next, make sure you are in the "postgresql-8.1.7" directory and type this command
    
    ```bash
    sudo ./configure CC=/usr/bin/clang CFLAGS="-O1" --enable-debug --enable-cassert
    
    #Note: the CFLAGS="O1" is O the letter and not zero
    ```
    

If you get an error stating that there is no C complier, type the following commands in the terminal. Then retry the previous command.

```bash
sudo apt-get update
sudo apt-get install build-essential
```

1. Next, to build the code type:
    
    ```bash
    sudo make
    ```
    
2. And then to install postgresql type:
    
    ```bash
    sudo make install
    ```
    
3. Create a separate user for postgres
    
    ```bash
    sudo adduser postgres
    
    #Switch to the new user
    su  postgres
    ```
    
4. Before initializing the database, add “/usr/local/pgsql/bin” to your shell’s command search path,
so that it can find the newly installed programs.
    
    To edit the path you have to modify the .bashrc file
    
    Open the .bashrc file using an editor like nano or vim. (You can open the file directly and edit and save it also. It is a hidden file in your home directory)
    
    ```bash
    #Open the .bashrc file using an editor like nano or vim
    nano ~/.bashrc
    
    #Add the following line at the end of the file
    export PATH="/usr/local/pgsql/bin:$PATH"
    
    #Save (Ctrl+O), press enter and exit (Ctrl+X) the file
    
    #Use this command for the changes to take effect
    source ~/.bashrc
    
    #You can verify that it has been added to the path using this command
    echo $PATH
    ```
    

1. Initialize : 
    
    ```bash
    initdb -D $HOME/pgdb
    ```
    

1. Start the server :
    
    ```bash
    postmaster -D $HOME/pgdb
    ```
    

1. To stop the server : 
    
    ```bash
    kill -INT ‘head -1 $HOME/pgdb/postmaster.pid‘ OR ctrl C
    ```