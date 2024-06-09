# Central 3D Print GCode Server

This is a simple server to host 3D Print GCode files for [Pull Printing](https://wikipedia.org/wiki/Pull_printing).
Simply put, you send your GCode file to the server after authenticating with a username and password (or ideally LDAP), it saves it in a folder, you go to the printer that you want to print on, authenticate with the same username and password, and then you can print the file.

