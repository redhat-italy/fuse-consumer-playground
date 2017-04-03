helloworld-mdb: Helloworld Using an MDB (Message-Driven Bean)
============================================================
Author: Serge Pagop, Andy Taylor, Jeff Mesnil  
Level: Intermediate  
Technologies: JMS, EJB, MDB  
Summary: The `helloworld-mdb` quickstart uses *JMS* and *EJB Message-Driven Bean* (MDB) to create and deploy JMS topic and queue resources in JBoss EAP.  
Target Product: JBoss EAP  
Source: <https://github.com/jboss-developer/jboss-eap-quickstarts/>  

What is it?
-----------

The `helloworld-mdb` quickstart demonstrates the use of *JMS* and *EJB Message-Driven Bean* in Red Hat JBoss Enterprise Application Platform.

This project creates two JMS resources:

* A queue named `HELLOWORLDMDBQueue` bound in JNDI as `java:/queue/HELLOWORLDMDBQueue`
* A topic named `HELLOWORLDMDBTopic` bound in JNDI as `java:/topic/HELLOWORLDMDBTopic`


System requirements
-------------------

The application this project produces is designed to be run on Red Hat JBoss Enterprise Application Platform 7 or later. 

All you need to build this project is Java 8.0 (Java SDK 1.8) or later and Maven 3.1.1 or later. See [Configure Maven for JBoss EAP 7](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/CONFIGURE_MAVEN_JBOSS_EAP7.md#configure-maven-to-build-and-deploy-the-quickstarts) to make sure you are configured correctly for testing the quickstarts.


Use of EAP7_HOME
---------------

In the following instructions, replace `EAP7_HOME` with the actual path to your JBoss EAP installation. The installation path is described in detail here: [Use of EAP7_HOME and JBOSS_HOME Variables](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_OF_EAP7_HOME.md#use-of-eap_home-and-jboss_home-variables).


Start the JBoss EAP Server with the Full Profile
---------------

1. Open a command prompt and navigate to the root of the JBoss EAP directory.
2. The following shows the command line to start the server with the full profile:

        For Linux:   EAP7_HOME/bin/standalone.sh -c standalone-full.xml
        For Windows: EAP7_HOME\bin\standalone.bat -c standalone-full.xml


Build and Deploy the Quickstart
-------------------------

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean install wildfly:deploy

4. This will deploy `target/jboss-helloworld-mdb.war` to the running instance of the server. Look at the JBoss EAP console or Server log and you should see log messages corresponding to the deployment of the message-driven beans and the JMS destinations:

        ...
        INFO  [org.wildfly.extension.messaging-activemq] (MSC service thread 1-4) WFLYMSGAMQ0002: Bound messaging object to jndi name java:/queue/HELLOWORLDMDBQueue
        INFO  [org.wildfly.extension.messaging-activemq] (MSC service thread 1-2) WFLYMSGAMQ0002: Bound messaging object to jndi name java:/topic/HELLOWORLDMDBTopic
        ....
        INFO  [org.apache.activemq.artemis.core.server] (ServerService Thread Pool -- 67) AMQ221003: trying to deploy queue jms.queue.HelloWorldMDBQueue
        ...
        INFO  [org.apache.activemq.artemis.core.server] (ServerService Thread Pool -- 12) AMQ221003: trying to deploy queue jms.topic.HelloWorldMDBTopic
        INFO  [org.jboss.as.ejb3] (MSC service thread 1-7) WFLYEJB0042: Started message driven bean 'HelloWorldQueueMDB' with 'activemq-ra.rar' resource adapter
        INFO  [org.jboss.as.ejb3] (MSC service thread 1-6) WFLYEJB0042: Started message driven bean 'HelloWorldQTopicMDB' with 'activemq-ra.rar' resource adapter
        

Access the application 
---------------------

The application will be running at the following URL: <http://localhost:8080/jboss-helloworld-mdb/> and will send some messages to the queue.

To send messages to the topic, use the following URL: <http://localhost:8080/jboss-helloworld-mdb/HelloWorldMDBServletClient?topic>

Investigate the Server Console Output
-------------------------

Look at the JBoss EAP console or Server log and you should see log messages like the following:

    INFO  [class org.jboss.as.quickstarts.mdb.HelloWorldQueueMDB] (Thread-9 (ActiveMQ-client-global-threads-1189700957)) Received Message from queue: This is message 5
    INFO  [class org.jboss.as.quickstarts.mdb.HelloWorldQueueMDB] (Thread-6 (ActiveMQ-client-global-threads-1189700957)) Received Message from queue: This is message 1
    INFO  [class org.jboss.as.quickstarts.mdb.HelloWorldQueueMDB] (Thread-7 (ActiveMQ-client-global-threads-1189700957)) Received Message from queue: This is message 4
    INFO  [class org.jboss.as.quickstarts.mdb.HelloWorldQueueMDB] (Thread-5 (ActiveMQ-client-global-threads-1189700957)) Received Message from queue: This is message 2
    INFO  [class org.jboss.as.quickstarts.mdb.HelloWorldQueueMDB] (Thread-4 (ActiveMQ-client-global-threads-1189700957)) Received Message from queue: This is message 3


Undeploy the Archive
--------------------

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn wildfly:undeploy


Run the Quickstart in Red Hat JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts or run the Arquillian tests from Eclipse using JBoss tools. For general information about how to import a quickstart, add a JBoss EAP server, and build and deploy a quickstart, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JBDS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts) 

_NOTE:_ Within JBoss Developer Studio, be sure to define a server runtime environment that uses the `standalone-full.xml` configuration file.


Debug the Application
------------------------------------

If you want to debug the source code of any library in the project, run the following command to pull the source into your local repository. The IDE should then detect it.

    mvn dependency:sources
   


<!-- Build and Deploy the Quickstart to OpenShift - Coming soon! -->

