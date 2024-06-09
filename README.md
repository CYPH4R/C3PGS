# Central 3D Print GCode Server

This is a simple server to host 3D Print GCode files for [Pull Printing](https://wikipedia.org/wiki/Pull_printing).
Simply put, you send your GCode file to the server after authenticating with a username and password (or ideally LDAP), it saves it in a folder, you go to the printer that you want to print on, authenticate with the same username and password, and then you can print the file.

This is ideal for environments where you have multiple printers, such as offices or makerspaces as you can give certain users access to certain printers.

              +-----------------+
              | Central LDAP/AD |
              |     Server      |
              +--------+--------+
                       |
                       |
+----------------------+----------------------+
|           Central Print Server             |
|--------------------------------------------|
| - Receives authenticated Gcode files       |
| - Stores user-related Gcode files          |
| - Communicates with LDAP/AD for auth       |
+--------+---------------------+-------------+
         ^                     |
         | User logs on and    |
         | credentials checked |
         |                     |
         |                     v
+------------------+        +-----------------+
|    User Device   |        |    3D Printer   |
|  (PC/Mac/Linux)  |        |                 | 
|                  |        |-----------------|
|------------------|        | - Auth with     |
| - Auth with LDAP |        |   LDAP/AD       |
|   via Print      |        | - Pulls Gcode   |
|   Server         |        |   files from    |
| - Sends Gcode    |        |   Print Server  |
|   file to Print  |        | - Displays      |
|   Server         |        |   user files    |
|                  |        | - Starts        |
+------------------+        |   printing      |
                            |   upon user     |
                            |   selection     |
                            +-------+---------+
                                    |
                                    | User selects
                                    | file and starts
                                    | printing
                                    v
                            +-----------------+
                            |   3D Print Job  |
                            |     Begins      |
                            +-----------------+
