java-client
===========
Java client allow to sent SMS messages and SMSAPI.com account managment.


Required library:
https://github.com/douglascrockford/JSON-java

Example:

```java
package com.example.smsapi_java_client_example;

import pl.smsapi.BasicAuthClient;
import pl.smsapi.api.SmsFactory;
import pl.smsapi.api.action.sms.SMSSend;
import pl.smsapi.api.response.MessageResponse;
import pl.smsapi.api.response.StatusResponse;
import pl.smsapi.exception.ClientException;
import pl.smsapi.exception.SmsapiException;
import pl.smsapi.proxy.ProxyNative;

public class Main {
    public static void main(String args[]) {
        try {
            String passwordHash = "00000000000000000000000000000000";
            BasicAuthClient client = new BasicAuthClient("username", passwordHash);

            SmsFactory smsApi = new SmsFactory(client, new ProxyNative("https://api.smsapi.com"));
            String phoneNumber = "000000000";
            SMSSend action = smsApi.actionSend()
                    .setText("test")
                    .setTo(phoneNumber);

            StatusResponse result = action.execute();

            for (MessageResponse status : result.getList() ) {
                System.out.println(status.getNumber() + " " + status.getStatus());
            }
        } catch (ClientException e) {
            e.printStackTrace();
        } catch (SmsapiException e) {
            e.printStackTrace();
        }
    }
```

## JAVADOC
[2.2](http://labs.smsapi.com/docs/javadoc/pl/smsapi/smsapi-lib/2.2/)

[2.1](http://labs.smsapi.com/docs/javadoc/pl/smsapi/smsapi-lib/2.1/)

[2.0](http://labs.smsapi.com/docs/javadoc/pl/smsapi/smsapi-lib/2.0/)

## MAVEN

In file **pom.xml** add:

```xml
<repositories>
        <repository>
            <releases>
                <enabled>true</enabled>
                <updatePolicy>always</updatePolicy>
                <checksumPolicy>fail</checksumPolicy>
            </releases>
            <id>smsapi</id>
            <name>smsapi</name>
            <url>http://labs.smsapi.com/maven/</url>
            <layout>default</layout>
        </repository>
    </repositories>
    <dependencies>
        <dependency>
            <groupId>pl.smsapi</groupId>
            <artifactId>smsapi-lib</artifactId>
            <version>2.4</version>
        </dependency>
    </dependencies>
```

## LICENSE
[Apache 2.0 License](https://github.com/smsapi/smsapi-java-client/blob/master/LICENSE)
