# opendaylight-hello
For OpenDayLight
 $ cat .bash_aliases 
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export M2_HOME=/usr/share/maven
export MAVEN_OPTS="-Xms256m -Xmx512m" # Very important to put the "m" on the end
source .bashrc

mkdir workdir
cd workdir

cp -n ~/.m2/settings.xml{,.orig} ; wget -q -O - https://raw.githubusercontent.com/opendaylight/odlparent/master/settings.xml > ~/.m2/settings.xml

export GROUP_ID=org.opendaylight.controller
export ARTIFACT_ID=opendaylight-startup-archetype
// export ARCHETYPE_VERSION= 1.2.2  //for sodium 
export ARCHETYPE_VERSION=1.2.4-Boron-SR4

mvn archetype:generate -DarchetypeGroupId=$GROUP_ID -DarchetypeArtifactId=$ARTIFACT_ID -DarchetypeRepository=http://nexus.opendaylight.org/content/repositories/opendaylight.release/ -DarchetypeCatalog=remote -DarchetypeVersion=$ARCHETYPE_VERSION
Define value for property 'groupId': : org.opendaylight.example
Define value for property 'artifactId': : example
Define value for property 'version':  1.0-SNAPSHOT: : 1.0.0-SNAPSHOT
Define value for property 'package':  org.opendaylight.example: :
Define value for property 'classPrefix':  ${artifactId.substring(0,1).toUpperCase()}${artifactId.substring(1)}
Define value for property 'copyright': : Copyright (c) 2015 Yoyodyne, Inc.


mvn clean install -DskipTests

./karaf/target/assembly/bin/karaf
feature:install odl-restconf odl-l2switch-switch odl-mdsal-apidocs odl-dlux-core
feature:install all hells

http://localhost:8181/index.html
http://localhost:8181/apidoc/explorer/index.html

Using a browser REST client
For example, use the following information in the Firefox plugin RESTClient https://github.com/chao/RESTClient
POST: http://localhost:8181/restconf/operations/hello:hello-world
Header:

Accept: application/json
Content-Type: application/json
Authorization: Basic admin admin
Body:

{"input": {
    "name": "Andrew"
  }
}
using the API Explorer through HTTP
Navigate to apidoc UI with your web browser.
NOTE: In the URL mentioned above, Change localhost to the IP/Host name to reflect your development machine’s network address.
Select

hello(2015-01-05)
Select

POST /operations/hello:hello-world
Provide the required value.

{"hello:input": { "name":"Your Name"}}
Click the button.

6. Enter the username and password. By default the credentials are admin/admin.

