AMI content:
----
1.Create EC2 instance

2.Connect to the ec2 instance via ssh

3.Install tomcat7


    sudo yum install tomcat7
4.Run *tomcat7* on startup. Verify that *tomcat7* is running under root in order to allow port *80* to be permitted for *tomcat7*.


    chkconfig --add tomcat7
    chkconfig tomcat7 on
5.If you want the port 80 (default http port) to be used by application, find server.xml config file in /tomcat7/conf/ folder and replace the standard 8080 port of config element from


    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />

to 80

    <Connector port="80" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />


6.Deploy sample webapplication on tomcat7.

      scp sample.war ec2-user@<ec2-instance-ip>:/usr/share/tomcat7/webapps/sample.war

Running EC2 instance:
----
Note! In case of using port 80 for incoming connections you should run EC2 instance with security-groups allowing inbound connections on port 80. For instructions on how to open port 80 for particular security-group follow the link:
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/authorizing-access-to-an-instance.html

List of public AMI.
----
1.*ami-49484e79* *pureHelloWorldAppFinalv3* AMI. Runs simple Tomcat 7 with deployed Hello World Application accessible via port 80 (http standard port) available at http://ip
