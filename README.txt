====== Luckycycle Java Connector 1.0 ======

This is a small library which help to connect to Luckycycle API v1

Installation and using:

a. Maven Project:

This is the most easy way to use this library. The procedure is:

- install the jar file in a remote or local maven repository. For example install in the local repository by Maven command:

    mvn org.apache.maven.plugins:maven-install-plugin:2.5.1:install-file -Dfile=<path-to-jar-file>

- include dependency into your maven project:

<dependencies>
	<dependency>
		<groupId>com.luckycycle</groupId>
		<artifactId>connector</artifactId>
		<version>1.0</version>
	</dependency>
	<dependency>
		<groupId>org.glassfish.jersey.core</groupId>
		<artifactId>jersey-client</artifactId>
		<version>2.19</version>
	</dependency>
	<dependency>
		<groupId>org.glassfish.jersey.media</groupId>
		<artifactId>jersey-media-json-jackson</artifactId>
		<version>2.19</version>
	</dependency>
	...
</dependencies>

All dependencies should be resolved nicely

b. Manual include jar file into the project:

This library is using other libraries: org.glassfish.jersey.core.jersy-client and org.glassfish.jersey.media.jersey-media-json-jackson, which is required other
libraries to function as well. The full list of libraries you should download and include into your project is:

	org\glassfish\hk2\external\aopalliance-repackaged-2.4.0-b25.jar
	org\glassfish\hk2\hk2-api\2.4.0-b25\hk2-api-2.4.0-b25.jar
	org\glassfish\hk2\hk2-locator\2.4.0-b25\hk2-locator-2.4.0-b25.jar
	org\glassfish\hk2\hk2-utils\2.4.0-b25\hk2-utils-2.4.0-b25.jar
	com\fasterxml\jackson\core\jackson-annotations\2.5.1\jackson-annotations-2.5.1.jar
	com\fasterxml\jackson\core\jackson-core\2.5.1\jackson-core-2.5.1.jar
	com\fasterxml\jackson\core\jackson-databind\2.5.1\jackson-databind-2.5.1.jar
	com\fasterxml\jackson\jaxrs\jackson-jaxrs-base\2.5.1\jackson-jaxrs-base-2.5.1.jar
	com\fasterxml\jackson\jaxrs\jackson-jaxrs-json-provider\2.5.1\jackson-jaxrs-json-provider-2.5.1.jar
	com\fasterxml\jackson\module\jackson-module-jaxb-annotations\2.5.1\jackson-module-jaxb-annotations-2.5.1.jar
	org\javassist\javassist\3.18.1-GA\javassist-3.18.1-GA.jar
	javax\annotation\javax.annotation-api\1.2\javax.annotation-api-1.2.jar
	org\glassfish\hk2\external\javax.inject\2.4.0-b25\javax.inject-2.4.0-b25.jar
	javax\ws\rs\javax.ws.rs-api\2.0.1\javax.ws.rs-api-2.0.1.jar
	org\glassfish\jersey\core\jersey-client\2.19\jersey-client-2.19.jar
	org\glassfish\jersey\core\jersey-common\2.19\jersey-common-2.19.jar
	org\glassfish\jersey\ext\jersey-entity-filtering\2.19\jersey-entity-filtering-2.19.jar
	org\glassfish\jersey\bundles\repackaged\jersey-guava\2.19\jersey-guava-2.19.jar
	org\glassfish\jersey\media\jersey-media-json-jackson\2.19\jersey-media-json-jackson-2.19.jar
	org\glassfish\hk2\osgi-resource-locator\1.0.1\osgi-resource-locator-1.0.1.jar


====== Usage ======

When initiating the Luckycycle object, you must use the credentials provided by Luckycycle:

	Luckycycle lc = new Luckycycle(API_KEY, OPERATION_ID);

Example code:

import java.util.LinkedHashMap;
import java.util.Map;
import com.luckycycle.connector.Luckycycle;

public class App
{
	public static void main( String[] args )
	{
		System.out.println( "Making a poke:" );
		Luckycycle lc = new Luckycycle("ee1b37a0577f160c7dc1deb4feb6ddffbae5dddf05874107c7eb029ca1d8f457", "598c131fabba176c1b49938d027beed0");
		lc.setValue("email", "jm@iesta.com");
		lc.setValue("item_value", "45.99");
		lc.setValue("segment", "A");
		lc.setValue("language", "fr");
		lc.setValue("user_uid", "U34566");
		lc.setValue("item_uid", "654345809");
		lc.setValue("payment_method", "VISA");
		lc.setValue("shipping_value", "1.99");
		Map<String, String> cartItem = new LinkedHashMap<String, String>();
		cartItem.put("price", "50.5");
		cartItem.put("quantity", "1");
		cartItem.put("product_id", "25");
		cartItem.put("category_id", "3");
		cartItem.put("manufacturer_id", "A");
		lc.addCartItem(cartItem);
		Map<String, String> cartItem1 = new LinkedHashMap<String, String>();
		cartItem1.put("price", "30");
		cartItem1.put("quantity", "2");
		cartItem1.put("product_id", "26");
		cartItem1.put("category_id", "1");
		cartItem1.put("manufacturer_id", "B");
		lc.addCartItem(cartItem1);
		Map<String, String> cartItem2 = new LinkedHashMap<String, String>();
		cartItem2.put("price", "11.99");
		cartItem2.put("quantity", "3");
		cartItem2.put("product_id", "26");
		cartItem2.put("category_id", "2");
		cartItem2.put("manufacturer_id", "B");
		lc.addCartItem(cartItem2);

		lc.poke(); // this does make the call to the Luckycycle API
		System.out.println("Can play? "+lc.can_play());
		System.out.println("Code of last operation:"+lc.code());
		System.out.println("Message from last operation:"+lc.message());
		System.out.println("All response from last operation:"+lc.getResult().toString());
		System.out.println("Html_Data:"+lc.html_data());

	}
}

The content of html_data should be inserted in the thank you page at the right place.

