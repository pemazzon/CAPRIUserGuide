Connecting Visual Studio Code
=============================

.. _vscode:

If you are familiar with the editor Visual Studio Code by Microsoft 
(from now on “VS Code”), it’s now possible to run it locally on your 
computer, either on a browser tab or as a standalone program, while 
executing your code on the server: this is made possible by linking the 
two executions through an account and a tunnel. <br />It can be convenient 
since you are going to use your local installation with its graphical 
interface that makes easy to access your projects. The results of the 
execution will also be presented on the local instance.

This is a link to the **official Microsoft guide**: https://code.visualstudio.com/docs/remote/tunnels


Procedure 
---------


For this to work you need:

    • VS Code in tunnel mode on the server;
    • an account to log in. It can be a GitHub or a Microsoft one;
    • the extension “Remote - Tunnels” by Microsoft if the software is locally installed.


Once connected to **capri.dei.unipd.it** you can request an interactive session
and from there the tunnel mode can be established:

::

  ssh username@capri.dei.unipd.it
  interactive
  
Wait for the confirmation of allocation and then input:

::

  code tunnel  

You will obtain a message like this: <br />
__ Open this link in your browser https://vscode.dev/tunnel/hpcapri __. <br />
Paste it and then:

    1. in the dropdown menu choose if you have a GitHub or a Microsoft Account;
    2. log in and input the code if provided;
    3. give a name to the machine for VS Code to identity it (default is “hpcapri”);
    4. open the new link provided in a browser.

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
