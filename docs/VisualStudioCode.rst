Connecting Visual Studio Code
=============================

If you are familiar with the editor Visual Studio Code by Microsoft 
(from now on “VS Code”), it’s now possible to run it locally on your 
computer, either on a browser tab or as a standalone program, while 
executing your code on the server by linking the two executions 
through an account and a tunnel. This makes it easy to debug code 
that’s stored on your local machine and that can be conveniently 
edited taking advantage of the local graphical interface. The results 
of the execution will also be presented on the local instance.


Procedure
---------

For this to work you need:

    • VS Code in tunnel mode on the server;
    • an account to log in. It can be a GitHub or a Microsoft one;
    • the extension “Remote - Tunnels” by Microsoft if the software is locally installed.


Once connected to **capri.dei.unipd.it** an interactive session can be 
requested with the command interactive and from there the tunnel 
mode can be established:

    ``code tunnel``

Subsequently you need to: 

    1. choose the type of account you have;
    2. click on the link to open it in a browser;
    3. log in and input the code provided;
    4. give a name to the machine for VS Code to identity it (default is “hpcapri”);
    5. open the link provided in a browser.

This will connect your account between the browser and the instance of 
VS Code on hpcapri. 

Similarly you can connect your local installation to the server using the 
services provided by the extension “Remote – Tunnels”:

    1. clic the button “Open on a Remote Window” whose symbol should be located on the left part of your panel (two white arrows on a blue background);
    2. select “Connect to Tunnel”;
    3. choose the account you want to log in with;
    4. grant permission and this will open the connection to the software running on the server.

From now on every code execution will be run on the server and the result 
will be presented on the local terminal of the program.
