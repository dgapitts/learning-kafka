### 050_gradle_run_Hello_consumer_World


Definition for our java class  i.e. `com.linuxacademy.ccdak.consumer`
```
cloud_user@ip-10-0-1-101:~/content-ccdak-kafka-consumer-lab$ cat src/main/java/com/linuxacademy/ccdak/consumer/Main.java

package com.linuxacademy.ccdak.consumer;

public class Main {

    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }

}
```

gradle build script
```
cloud_user@ip-10-0-1-101:~/content-ccdak-kafka-consumer-lab$ cat build.gradleplugins 
{
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.apache.kafka:kafka-clients:2.2.1'
    testImplementation 'junit:junit:4.12'
}

application {
    mainClassName = 'com.linuxacademy.ccdak.consumer.Main'
}
```

and running this i.e. `./gradlew run`

```
cloud_user@ip-10-0-1-101:~/content-ccdak-kafka-consumer-lab$ ./gradlew run
Downloading https://services.gradle.org/distributions/gradle-5.5.1-bin.zip
.....................................................................................

Welcome to Gradle 5.5.1!

Here are the highlights of this release:
 - Kickstart Gradle plugin development with gradle init
 - Distribute organization-wide Gradle properties in custom Gradle distributions
 - Transform dependency artifacts on resolution

For more details see https://docs.gradle.org/5.5.1/release-notes.html

Starting a Gradle Daemon (subsequent builds will be faster)

> Task :run
Hello, World!

BUILD SUCCESSFUL in 39s
2 actionable tasks: 2 executed
```



