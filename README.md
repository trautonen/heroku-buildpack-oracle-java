Heroku buildpack: Oracle JDK
============================

This is a Heroku buildpack for Java applications that use Maven as build tool.
The buildpack installs Oracle JDK 1.8.0_20 and Maven 3.2.1 by default. The
buildpack can also be configured to install JCE Unlimited Strength policy
files.

**Oracle License Agreement**  
By using this buildpack you must agree the Oracle Binary Code License
Agreement for the Java SE Platform Products and JavaFX.  
http://www.oracle.com/technetwork/java/javase/terms/license/index.html

Usage
-----

    $ ls
    Procfile  pom.xml  src

    $ heroku apps:create example --buildpack https://github.com/trautonen/heroku-buildpack-oracle-java

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Java app detected
    -----> Installing wget... version 1.15 installed
    -----> Installing JDK... (downloading...) version 1.8.0_20 installed
    -----> Installing Maven... version 3.2.1 installed
    -----> Installing NewRelic agent... done
    -----> Executing build...
           mvn -B -Duser.home=/tmp/build_2be971b4-90c0-48d4-8045-8ef1b5521352 -Dmaven.repo.local=/app/tmp/cache/.m2/repository -DskipTests=true -U clean install

The buildpack will detect `pom.xml` in the project root folder and executes
maven with `clean` and  `install` goals to create the executable.


Configuration
-------------

Different features of the buildpack can be configured with Heroku config vars.
Config vars can be set using the Heroku CLI:

    $ heroku config:set VAR="value"

* `JCE`: JCE Unlimited Strength  
  `JCE="true"` will download and apply the JCE Unlimited Strength policy files
* `GEMS`: Ruby gems  
  `GEMS="sass compass"` will install sass and compass Ruby gems  
  (gems are only available at slug compilation time)


License
-------

Licensed under the MIT License. See LICENSE.MIT file.
