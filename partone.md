# How to write your first JAVA Smart Contract for the ICON Blockchain | 1 / 4 

Blockchain interoperability in 2022 has been a major topic across the blockchain industry. It is likely to remain an important theme in 2023 as the ICON Network builds towards interoperable solutions for users and developers.

  

Currently, the ICON ecosystem has two related interoperability solutions – [BTP](https://icon.community/learn/btp/) and [ICON Bridge](https://icon.community/learn/icon-bridge/). BTP is fully trustless and uses on-chain light clients for cross-chain message verification, while ICON Bridge relies on a trusted operator for verifying and relaying messages.

  

[Smart contracts](https://101blockchains.com/what-is-a-smart-contract/) based on blockchain technology are available on the ICON Network and documentation for developers is accessible on the [icon.community website](https://icon.community/). Community members often want to know how to become a smart contract developer and what the many benefits of smart contract development on ICON are!

In short, the functionalities of smart contracts on ICON allow developers to build popular [DeFi platforms and NFT collections](https://icon.community/ecosystem/). Smart contracts on the ICON Blockchain are written in Java and are called SCOREs (Smart Contract on Reliable Environment).

In this series of articles we will go through the steps needed for getting your first SCORE deployed on the ICON Blockchain. Throughout this series we will be referencing the Github of the ICON Project a lot. So be sure to check [https://github.com/icon-project/java-score-examples](https://github.com/icon-project/java-score-examples) when writing SCOREs.
I will run a script now and then to check if exchanges are using new addresses.

In this part, the first one, we will go over the ‘Hello World’ example. A simple Smart Contract that, you guessed it, will create a greeting-function!

## 1 OpenJDK

Before we start you need to make sure that you got JDK 11 or later installed on your system. Visit OpenJDK.org for prebuilt binaries or use:

Mac OS **:

```bash 
brew tap AdoptOpenJDK/openjdk
brew cask install adoptopenjdk11
```
  

Linux:
```bash
sudo apt install openjdk-11-jdk
```
** If you are using an Apple M1 device and have issues with this step check out this post: [https://forum.icon.community/t/getting-icon-2-0-set-up-with-an-apple-m1-arm64-device/2233](https://forum.icon.community/t/getting-icon-2-0-set-up-with-an-apple-m1-arm64-device/2233)

  ## 2 Clone the ICON Java-Score-Examples

Make sure to clone the Java Score Examples from [https://github.com/icon-project/java-score-examples](https://github.com/icon-project/java-score-examples) and know that the project uses the Gradle build-tool ([https://docs.gradle.org/current/userguide/what_is_gradle.html](https://docs.gradle.org/current/userguide/what_is_gradle.html)).

We will be using the 'Hello World' example. The source code for this example is located at:

`java-score-examples/hello-world/src/main/java/com/iconloop/score/example/HelloWorld.java`

You can see that the example is fairly straightforward, let's go over the steps!

## 3  Define the Class & import dependencies

Before we build the SCORE, which is a Java Class we define a package and import the needed dependencies:

```java
package com.iconloop.score.example;  
  
import score.Context;  
import score.annotation.External;  
import score.annotation.Payable;
```

## 4 Create the Class
After the needed imports, we create a public class:

```java
public class HelloWorld {
```
_*We will close the class at the end of the document, of course._

## 5 Declare variable 'name'
In this Smart Contract we will have a function that will use the 'name' variable in its return value. 

'name' will be given an initial value in the constructor. But first we will need to declare to 'name' variable to be able to do so:
```java
private String name;
```

## 6 The Constructor
The public function with the same name as the class is the Constructor. Below we let the Constructor set a value to the above created 'name' variable.

```java
public HelloWorld(String _name) {  
	this.name = _name;  
}
```

_Make sure to read the next parts of the 'How to write your first JAVA Smart Contract for the ICON Blockchain'-series to see how we instantiate the contract using the Constructor. If you are not experienced with [Object-Oriented Programming(OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming) this will help understand what is going in the Constructor._


## 7 Create 'setName( )'
Now we create a function that can be used to set / change the ‘name’ variable on the contract:

```java
@External()
public void setName(String _name) {  
	this.name = _name;  
}
```
The ‘@External( )’ decorator is needed to make the function externally callable. Without it it would be a private function that is only usable from within the class itself.

## 8 'get' the name

Create a function that lets us see the current value of the ‘name’ variable:
```java
@External(readonly=true)  
public String name() {  
	return name;  
}
```

We added the ‘External’ decorator again so the function is callable from outside of the class. The (readonly=true) parameter makes the function ‘read only’. You can not change anything using ‘read only’ functions. (In Solidity you would use the ‘view’ attribute for this.) The ‘String’ tells Java what the return-type of this function is.

## 9 Create 'getGreeting( )'
Now we will create the function ‘getGreeting’ which will return a string that greets the name-value that is currently set to the 'name' variable. 
```java
@External(readonly=true)  
public  String getGreeting() {  
	String msg = "Hello " + name + "!";  
	return msg;  
}
```
Keep in mind; We have set the 'name' variable in the Constructor and might have changed it using the setName( ) function we created in step 7.

## 10 Create a fallback function
The last function of this example is the fallback function which lets the contract receive ICX funds:

```java
@Payable  
public  void  fallback() {  
	// just receive incoming funds  
}
```
The @Payable decorator is needed on functions that should be able to receive/handle payments. The ‘fallback’ function is needed when you want the contract to be able to hold ICX tokens.

Don’t forget to close the Class with a } and your first ICON Smart Contract is almost ready for deployment! In the next part we will compile the Java code using the [Gradle build-tool](https://gradle.org/) so it will be ready to deploy on the ICON Blockchain!

## Closing words

The journey of any smart contract developer in ICON involves a set of core ICON development tools. Smart contracts are written in JAVA, and smart contract developers on ICON can use the 'java-score-example' repo of the [official ICON Github](https://github.com/icon-project/java-score-examples) to get started.

  

Training for JAVA smart contract developer jobs is all about learning skills that help you build robust code for popular applications. Following along with these tutorials will help you build your skills and increase your practical knowledge of smart contract development.

On icon.community, you can read [in-depth articles about key ICON topics](https://icon.community/learn/) and concepts. ICON developers can stay updated with the [latest ICON news and developments](https://icon.community/blog/) too. To learn more about the details of the tutorials and how it can help your smart contract development career, head over to [https://forum.icon.community/](https://forum.icon.community/).

## note to Dave & team
Point to a support channel / forum here, it will be better to do it on a forum-site instead of Discord/Telegram. The forum should be a good place for (new) people to create topics and for active developers to answer questions. I notice that in the dev telegram group a lot of repeat questions come by. 

And it can be demotivating the you can not get your issues solved because there are no "active" devs in the existing channels. A database of q-and-a's in a forum style maybe a solution for this.
