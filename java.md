# Java Instructions

## Setting Up Java Runtime on the Pi

* To install Java on the Pi, run the following command on the Pi: 
`sudo apt-get install oracle-java8-jdk`

The following shouldn't be necessary and should only be done if problems are found: 
 * Install the pi4j libs that allow you to talk to the gpio pins: `curl -s get.pi4j.com | sudo bash`

### Verifying the Installation 

* `which java` should print something like `usr/bin/java`.  If this works, Java is on the PATH. 
* Running `java -version` indicates that Java is properly running. 

### Wiring Support

Wiring support for the Raspberry Pi comes via the [Wiring Pi project](http://wiringpi.com/download-and-install/). 

Check out the code and build it. 

## Setting Up The Java Dev Environment on the Laptop

If not already present, Java and a Java IDE are needed on the workstation laptops. 
* Install the Java JDK (8 or similar) if it is not already installed. 
* Install Eclipse if it is not already installed. 

Start Eclipse and create a workspace with a Maven project. 

Add to pom.xml file:
```
  <repositories>
	<repository>
		<id>oss-snapshots-repo</id>
		<name>Sonatype OSS Maven Repository</name>
		<url>https://oss.sonatype.org/content/groups/public</url>
		<snapshots>
			<enabled>true</enabled>
			<updatePolicy>always</updatePolicy>
		</snapshots>
	</repository>
</repositories>
  <dependencies>
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-core</artifactId>
   <version>1.3-SNAPSHOT</version>
</dependency>
  </dependencies>
```

## Writing the Code 

The code is not provided, but here is a sample that might be useful: 

```
package UAHS.ParkingSensor;

import com.pi4j.io.gpio.GpioController;
import com.pi4j.io.gpio.GpioFactory;
import com.pi4j.io.gpio.GpioPinDigitalOutput;
import com.pi4j.io.gpio.RaspiPin;

public class ParkingSensor {

	   public static void main(String[] args) {
		    try {
		        /** create gpio controller */
		        final GpioController gpio = GpioFactory.getInstance();

		        final GpioPinDigitalOutput ledPin = gpio.provisionDigitalOutputPin(RaspiPin.GPIO_15);


		        /** Blink every second */
		        ledPin.blink(1000, 15000);

		        /** keep program running until user aborts (CTRL-C) */
		        while (true) {
		        Thread.sleep(500);
		        }

		    } catch (Exception e) {
		        e.printStackTrace();
		    }
		    }
}
```

## Running Your Code

* Export as a runnable JAR file with the libraries packed in.
* Move your Java JAR file over to the Raspberry Pi using:

`scp ParkingSensor.jar pi@raspberrypi.local:ParkingSensor.jar`

* Run the program with: 

`sudo java -jar ParkingSensor.jar`
