# Jenkins for Continuous Integration


## Installation on Ubuntu 12.04.x

```
wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

There might have a small problem, jenkins requires java version 1.7 but default version of java on Ubuntu is 1.6. So here I am gonna install openjdk 1.7:
```
sudo apt-get install -y openjdk-7-jdk

Switch the default 1.6 to 1.7:

sudo update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      auto mode
  1            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      manual mode
  2            /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java   1051      manual mode

Press enter to keep the current choice[*], or type selection number: 2
update-alternatives: using /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java to provide /usr/bin/java (java) in manual mode.

java -version

java version "1.7.0_79"
OpenJDK Runtime Environment (IcedTea 2.5.5) (7u79-2.5.5-0ubuntu0.12.04.1)
OpenJDK 64-Bit Server VM (build 24.79-b02, mixed mode)

```

And now, we can start jenkins by the following command:
```
sudo service jenkins start
```

