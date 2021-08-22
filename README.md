##  Performing an S2I (source to image) build within OpenShift

Clone this git repo to your local disk and then use that to create a publicly visible git rep on github.com (the public one, not the IBM enterprise git repo).
After this code is in the github.com repo, work through the task specified. Note that you will need the maven command line working locally, and
a locally installed Java 11 JDK, in order to make the first 3 steps of this exercise work. In order to make the maven command line work, you
will have to set the JAVA_HOME environment variable to point to the location of the JDK. If you cannot get this working, it is still possible
to complete the rest of this exercise (step 4 and onwards), but you will not have a reference working application to compare to.


## Task

1. Change directory to the "complete" sub-directory within the repo. Perform a maven build ("mvn package") and ensure that it completes successfully.
2. Start the spring boot app. In the "target" sub-directory, you will find a <code>spring-boot-0.0.1-SNAPSHOT.jar</code> jar file. Use a java 11 JRE to start this Spring Boot application.
3. Validate that this works correctly by using your browser to go to http://localhost:8080/ . This should print "Greetings from Spring Boot!".
4. Perform an S2I build by using the new-app command and using the "java:11" imagestream. This imagestream is a builder image for Java code -
particularly, code that will be built using maven. Specify the name of the app as "sample-boot-app". Note that:
    1.  You should use the "--as-deployment-config" flag on the new-app command.
    2.  You should also specify the "--context-dir" flag, with the "complete" sub-directory specified as its value
5. Observe the build by using the "oc logs" command to look at the buildconfig for "sample-boot-app".
6. After the build is done running, use the "oc get pods" command to observe the status of the application. Initially, you will see a deploy
pod instantiated. After it is done running, the pod for the actual application will be instantiated.
7. Observe the logs of the application as it starts up, using the "oc logs" command.
8. Create a route for the application by using the "oc create route edge" command. This will produce an https endpoint that you can access via
the browser. Check to see that you get a message at the root URI saying "Greetings from Spring Boot!".
