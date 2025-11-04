<h1>Create a Linux shell script and set it as executable</h1>

<h2>Description</h2>
<ul>
  <li>Create a bash script in Kali Linux with the nano command and paste the script into the text file</li>
  <li>Set the bash script to executable in order to execute the file</li>
  <li>View the results and test the script</li>
</ul>

<h2>Languages and Utilities Used</h2>

- <b>Kali Linux, Linux Executable Permissions, Bash Scripts</b> 

<h2>Environments Used </h2>

- <b>Windows 11, VirtualBox, Kali Linux</b>

<h2>Program walk-through:</h2>

<h3>Part 1: Create a Bash Script in Kali Linux
</h3>

<p>Open Kali Linux VirtualBox image</p>

<br />

<p>Enter the following command to navigate to the home directory</p>
<ul>
  <li>cd (change directory)</li>
</ul>

<p>Enter the following command to verify you are in the home directory</p>
<ul>
  <li>pwd (print working directory)</li>
</ul>

<p>Enter the following command to create a text file</p>
<ul>
  <li>sudo nano scripttest.sh</li>
  <li>nano opens a text file in linux</li>
</ul>

<img src="https://i.imgur.com/2gfwzjM.png" height="80%" width="80%" alt="nano scripttest.sh"/>

<img src="https://i.imgur.com/x1Y382S.png" height="80%" width="80%" alt="nano text editor"/>

<p>Copy the script that will be executed</p>
<ul>
  <li>In kali Linux, choose the edit tab at the top and select paste clipboard</li>
</ul>

<img src="https://i.imgur.com/wwVXkyB.png" height="80%" width="80%" alt="bash script in nano"/>

<h3>Part 2: Script description:
</h3>

<p>#!/bin/bash</p>
<ul>
  <li>Since Linux has multiple shells, this signifies that the following script should be run in a bash shell</li>
</ul>

<p>function show_ipinfo()</p>
<ul>
  <li>Creates a function called show_ipinfo</li>
</ul>

<p>`IP_VAR=`ifconfig eth0 | grep "inet" | tr -s " " ":" | cut -f3 -d ":"`</p>
<ul>
  <li>The right side of the equals sign is enclosed in two backticks (`) meaning it will execute everything within the backticks and store it in a variable called IP_VAR</li>
  <li>Runs a Linux command ifconfig against eth0</li>
  <li>piping ( | sends output as input) filtering for text inet | </li>
  <li>tr (translating) -s (squeeze repeats, replaces sequences of a repeated character with just a single instance of that character)</li>
  <li>“ “ “:” (changes spaces to colons) |</li>
  <li>cut (cut out) -f3 (field 3, based on the delimiter)</li>
  <li>-d “:” (with a delimiter of a colon)</li>
</ul>

<p>`DGW_VAR=`ip route show | grep "default" | tr -s " " ":" | cut -f3 -d ":"`</p>
<ul>
  <li>Same idea as the previous only the Linux command is ip route show piped to grep “default”</li>
</ul>

<p>echo "IP ADDRESS:" $IP_VAR</p>
<p>echo "DEFAULT GATEWAY:" $DGW_VAR</p>
<ul>
  <li>The echo command in Linux is used to display a line of text or a variable’s value to the terminal (standard output)</li>
  <li>These two echo commands will display a string("IP ADDRESS:") followed by the stored variable($IP_VAR)</li>
  <li>The $ refers to the variable that is stored</li>
</ul>

<p>cat /etc/resolv.conf | grep "nameserver" | grep -v "#"</p>
<ul>
  <li>Displays some name server information by using cat against the /etc/resolv.conf file</li>
</ul>

<img src="https://i.imgur.com/Ksxq7E9.png" height="80%" width="80%" alt="while loop in bash script"/>

<p>This is the while loop (in between do and done) that will be the interaction with the user. The user will see text similar to the contents within the echo statements.</p>
<ul>
  <li>The user has the ability to select 1, 2, or 3</li>
  <li>The read selection command will accept the user input and save it to a variable called selection</li>
  <li>The case $selection tests the variable in a case statement depending on which number the user enters</li>
  <li>1 will run the show_ipinfo function</li>
  <li>2 will return who the user is logged in as</li>
  <li>3 will clear the screen and exit the loop</li>
  <li>esac (case spelt backwards ends the case statement)</li>
  <li>read junkvar pauses the script and allows the user to make another selection</li>
</ul>

<p>Enter the following to save and exit out of the text file</p>
<ul>
  <li>Ctrl + x</li>
</ul>

<img src="https://i.imgur.com/TEpJooB.png" height="80%" width="80%" alt="save text file"/>

<p>Press y to save the text file</p>

<img src="https://i.imgur.com/6Up08TL.png" height="80%" width="80%" alt="save file name for text file"/>

<p>Asking the file name to write to</p>
<ul>
  <li>Press enter if the file name is correct</li>
</ul>

<h3>Part 3: Run the Bash Script
</h3>

<p>Enter the following command to list the contents of the current directory where the script was saved</p>
<ul>
  <li>ls</li>
</ul>

<img src="" height="80%" width="80%" alt="view scripttest.sh in file"/>

<p>Notice the new file called scripttest.sh</p>

<p>Enter the following command to run the Linux script</p>
<ul>
  <li>sudo ./scripttest.sh</li>
</ul>

<img src="https://i.imgur.com/PdEOXPL.png" height="80%" width="80%" alt="failed perms on executable prompt"/>

<p>Notice the script does not run. This is because the script has not been flagged as executable.</p>

<p>Enter the following command to check the permissions on the script file</p>
<ul>
  <li>ls -l scripttest.sh</li>
</ul>

<img src="https://i.imgur.com/Uw1ND8Q.png" height="80%" width="80%" alt="default permissions with text file"/>

<p></p>

<p>Enter the following command to change the permissions on the file</p>
<ul>
  <li>sudo chmod 550 scripttest.sh</li>
  <li>The first 5 is a combination of read (4 in linux) and execute (1 in linux) 4 + 1 = 5</li>
  <li>The three characters (550) signifies the groups in Linux (User (owner), Group, Others)</li>
</ul>

<img src="https://i.imgur.com/wnVCjrw.png" height="80%" width="80%" alt="change permissions command"/>

<p>Enter the following command to view the permissions on the file again</p>
<ul>
  <li>ls -l scripttest.sh</li>
</ul>

<img src="https://i.imgur.com/Bty2xsb.png" height="80%" width="80%" alt="executable permissions shown"/>

<p>Notice how the string has an x (executable) in the 4th and 7th slot of the string meaning the user and group now have executable privileges</p>

<p>Enter the following command to run the script again now that the user has execute privileges</p>
<ul>
  <li>sudo ./scripttest.sh</li>
</ul>

<img src="https://i.imgur.com/awzbHdf.png" height="80%" width="80%" alt="utility menu from script"/>

<p>Notice the script now runs and the user is prompted with the utility menu created in the script</p>

<p>Example of when the user enters 1:</p>

<img src="https://i.imgur.com/pwq5n8L.png" height="80%" width="80%" alt="choice 1"/>

<p>Example of when the user enters a 2:</p>

<img src="https://i.imgur.com/0iva9XK.png" height="80%" width="80%" alt="choice 2"/>

<p>Example of when the user enters a 3:</p>

<img src="https://i.imgur.com/XzTJ9ro.png" height="80%" width="80%" alt="back to kali command line"/>

<p>Notice it exits the script and we are back to the command line</p>

<h3>Summary</h3>
<p>Developed a Bash script on Kali Linux using the nano text editor and saved as a text file. The script file was then set to executable using the chmod command, enabling it to run as a standalone program. The script is then executed successfully, and its functionality was verified through testing. The intended results were then demonstrated through use of user input through the utility menu created in the script.</p>
 
