Heroku buildpack: Oracle JDK
============================

This is a Heroku buildpack for Java applications that use Maven as build tool.
The buildpack installs Oracle JDK 1.8.0_151 and Maven 3.3.9 by default. The
buildpack can also be configured to install JCE Unlimited Strength policy
files and Ruby gems. If the application has NewRelic plugin installed, the
buildpack will install NewRelic java agent automatically and enable it.

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
    -----> Installing JDK... (downloading...) version 1.8.0_151 installed
    -----> Installing Maven... version 3.3.9 installed
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

* `MAVEN_CUSTOM_OPTS`: Command line options for Maven build  
  Defaults to `-DskipTests=true -U`
* `MAVEN_CUSTOM_GOALS`: Goals for Maven build  
  Defaults to `clean install`
* `MAVEN_OPTS`: Maven environment variables  
  Defaults to `-Xmx384m -Xss128m`
* `JAVA_OPTS`: Java environment variables for application runtime  
  Defaults to `-Xmx384m -Xss128m`
* `NEW_RELIC_DISABLED`: New Relic agent  
  `true` will disable New Relic agent for the application
* `JCE`: JCE Unlimited Strength  
  `true` will download and apply the JCE Unlimited Strength policy files
* `GEMS`: Ruby gems to be installed  
  `sass compass` will install sass and compass Ruby gems  
  (gems are only available at slug compilation time)


License
-------

Licensed under the MIT License. See LICENSE.MIT file.
