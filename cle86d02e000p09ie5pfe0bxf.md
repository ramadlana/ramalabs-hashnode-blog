# How to Create Custom Service Systemd on Linux

As developers, we often want to create a service system that can run on background and then launch a service every system startup. These services can be anything, maybe you have python scripts, bash scripts, or node js scripts, or maybe like this example, we create a custom service for Metabase ([https://www.metabase.com/start/](https://www.metabase.com/start/)[)](https://www.metabase.com/start/)).

Metabase can be launched from the user terminal by typing `java -jar metabase.jar` but if every user logout or close the terminal Metabase will stop immediately.

**Goal:**

Our goal is simple we want to create services for Metabase and then control it using systemd for example `systemctl start metabase.service`

**Step 1: Goto systemd folder**

Find your user-defined services. Ubuntu was at `/etc/systemd/system/`

**Step 2: Create .service files**

Create a text file with your favorite text editor name it `whatever_you_want.service`

**Step 3: .service example**

Put the following **Template** to the file `whatever_you_want.service`

```bash
[Unit]
Description=Metabase Daemon

[Service]
PIDFile=/run/metabase.pid
WorkingDirectory=/usr/local/bin/metabase/
User=ubuntu
Group=ubuntu

#RUN COMMAND HERE
ExecStart=/usr/bin/java -jar -Xmx512m /usr/local/bin/metabase/metabase.jar

Restart=on-failure
RestartSec=30
PrivateTmp=true

StandardOutput=file:/var/log/yourmetabase.log
StandardError=file:/var/log/yourmetabase.err.log

[Install]
WantedBy=multi-user.target
```

### **Explanation**

1. Unit: Every service is called a unit and gives a description with a name for this example is Metabase Daemon
    
2. PID: process identifier and location is on /run folder.
    
3. Working directory: Where your application folder is located
    
4. User & Group: user and group your operating system
    
5. ExecStart: Command to execute. You must specify the full path to the executable. For example, if our application is running using `java my_app.jar` you must specify `/usr/bin/java`. if you are not sure where the executable is located you can run `which java` on terminal
    
6. Standard Output and Standart Error: For logging purposes, every application returned value to the user and every application faces errors
    
7. [Multi-user.target](http://Multi-user.target): Normally defines a system state where all network services are started up and the system will accept logins, but a local GUI is not started. so for simplicity here is the rule of thumb: Use [multi-user.target](http://multi-user.target) if your application is not GUI and use [graphical.target](http://graphical.target) if your application is GUI