# MIAO
<a href="LICENSE">
    <img src="https://img.shields.io/badge/License-MIT with 996.ICU-yellow.svg">
</a>
  
- - -
EN | <a href="./README.md">中文</a>

## What is MIAO?
MIAO ("Miao Is A web demO generator", pronounced /mjɑʊ/) is a non-intrusive web demo generator that quickly converts a function or piece of code into a web UI for temporary demos or tests, out-of-the-box without a complex configuration process.

MIAO is not a Web framework, its focus is very different from the Web framework, MIAO is mainly used to create some small temporary demos or small online tools, rather than being used in production environments, and is not recommended for formal projects.

MIAO is a trade-off between flexibility and ease of use, mainly focused on providing convenient, out-of-the-box temporary web demo generation, without providing too much configuration and custom UI/interaction features, and not like the Web framework, such as "Permission control", "Routing", "Template rendering", "Session" and other features.
A small temporary demo can be created quickly in just three steps.
Import the library -> Add annotations -> Start the server

MIAO currently only supports Java and Python, support for other languages (such as Golang,Haskell) will be added later, so stay tuned.

## How to use?
**This tool is not yet fully developed, only some of the main features can be used at present, the rest of the features are planned to be implemented in the "Roadmap" section later**

In pom.xml (Maven).
``` xml
<dependencies>
    <dependency>
        <groupId>cn.voidnet</groupId>
        <artifactId>MIAO</artifactId>
        <version>0.0.10</version>
    </dependency
</dependencies>
```

Alternatively, you can go to Release and download the jar and add it to your project's external library dependency directory

Then just put the @WebDemo annotation on the function you want to generate the UI for (obviously, only static functions)
``` java
	  @WebDemo
    public static int getRandomNumber(int min, int max) {
        return new Random().nextInt(max - min + 1) + min;
    }
```
Finally, in the main function (or wherever you want to start the service), just start the server side of the tool
``` java
    public static void main(String[] args) {
        MIAO.start();
    }
```
The start() function will block on execution, so place this line of code after the rest of your code in main, or open a new thread for this tool to serve.

Then you can automatically generate a temporary demo like this.
! [](MIAO/2BDC99A1-FDB7-4D7F-B878-FEF673A309F7.png)

Click "Execute" to execute and get the return value: !

! [](MIAO/72C26721-DC73-495F-B3A7-ACC79921898A.png)

Of course, this tool also provides some simple customization options, for example you can change the function name parameter names, etc.: !
``` java
@WebDemo("Add two numbers")
public static double add(
        @Parameter("operand1") double opr1,
        @Parameter("operand2") double opr2
) {
    return opr1 + opr2;
}
```
! [](MIAO/F93D29A9-ABF7-4AD9-83F1-FF1972D8793C.png)
The title above can also be modified by means of the following parameters:
``` java
MIAO.start("Cat Ear Switch Controller");
```
[image:7698089C-E420-4322-BC71-4E2D3D77EA28-33798-00012951A6E99FCB/4C9314FA-D50A-4DC9-8D5A-285070BF659B.png]


More customization items will be added in the future (e.g. the way return values are displayed, parameters can be selected from optional, etc.)

PS: If you are using Gradle, please add mavenCentral() to the repositories, and then introduce this library.

**PPS:Please set the function you want to generate the web demo and the class it is in to public to circumvent Java reflection restrictions**

**PPPS:Since this tool is not yet fully developed, only basic data types are supported for function parameters and return values for now, support for "images" "tables" "charts" "objects" "files" "videos" "function images" will be added later, see the "Roadmap" section**
## What does the name mean?
MIAO is an abbreviation for "Miao Is A web demO generator", and is also a Chinese syllable used to describe the sound of a cat's purr (meow, pronounced /mjɑʊ/), similar to "meow" and "にゃ" (≧∇≦).

When you mention the name of this framework, you can also call it MiaoLib to avoid ambiguity or confusion with cat calls.
## Some examples
<Put example code here>.

<Put the UI image here>.
Possible examples: maven to gradle
## Differences in focus between MIAO and web frameworks
MIAO is not a Web framework, its focus is very different from the Web framework, the two are more of a complementary relationship between MIAO is mainly concerned with the application of the following scenarios.
1. you want to show a half-finished project to colleagues or friends temporarily, using the command line to show it is not very intuitive, and sometimes not very convenient, especially for test users who are not familiar with the computer, but also need to spend some time to introduce the use of the command line, the empty command line UI is not suitable for temporary demonstration purposes.
And if you and the demo viewer are in a different location (such as online presentation on the Internet), you often also need a remote desktop/conference software type of tool to assist the demonstration, too much trouble. Writing another ad-hoc front-end application for this purpose would be too much of a waste of time.
For this scenario, you use this tool to generate a temporary demo and hang it on the server (or on the local machine if it is on the same intranet), others can directly access your temporary demo by typing in the URL on their computers or cell phones, which is very convenient!
2. You have developed a new tool or library (e.g. face recognition, target detection, etc.) and want to turn your academic results into an interactive demo program for other people to use or for academic communication, you can introduce this library into your Python or Java code to automatically generate web demos (support for charts, etc. will be added later) without writing front-end code
3. You want to make some small tools for online use, such as text formatting, face beauty, emoticon creation, binary conversion, text recognition, tagging tools, etc., but it is not convenient to use front-end technology (Web or Native) for development, or you are not familiar with front-end technology. You can use this library to generate the front-end UI (support for image/file upload and return value will be added later), instead of writing a front-end application, saving your development cost.
4. You are developing some embedded applications (e.g. IoT, Home Automation, etc.), and you want users to access your application remotely through the web to do some simple operations (e.g. turn on lights, turn off lights, adjust brightness, etc.). You can write the control program in a Python-enabled embedded device (e.g. Raspberry Pi), and then bring in this library to generate the web control page. Save the cost you spend on developing the front-end part.
## Roadmap
The following features will be added to this tool step by step. If you are interested in this project, you are also welcome to contribute code to this project by forking and PR.
- [ ] Front-end type-checking
- [ ] Multi-language support
- [ ] More unit tests
- [ ] Support for "file" type for arguments and return values
- [ ] Support for "List" type for arguments and return values
- [x] Support for Python language
- [ ] Improvements to the Python version
- [ ] Type annotation for Python version
- [ ] Support "object" type for return value, e.g. return object directly and display it as a tree in the UI (you can also pop up a dialog box to show the details)
- [ ] Support a new setting item: present multiple return results in a table, i.e., each return result is a row, each return result's property is a different column, and multiple return results form a table.
- [ ] Parameter and return value support "image" type
- [ ] UI style_theme_color_modification
- [ ] Simple password authentication mechanism, for example, when entering the UI requires a password, but does not need to be too complex

## Q&A
### Will there be more customization options for the UI in the future? For example, provide API to modify the UI structure or style
If you have complex UI requirements, the Web framework may be a better choice.

Of course, we do not rule out the possibility of adding some simple UI theme settings to change the style or color of the UI, but will not provide such complex customization APIs as "modify the web structure and layout CSS style of the UI".

However, the UI code is also open source, you are welcome to directly fork the UI code (here is the code repository address) to modify it directly, and we will add the API to change the UI web page (front-end) later.
## Contribute code
If you are interested in this project, you are also welcome to contribute code to this project by forking and PR.

If you encounter any problems with the code, or if you find bugs, you are welcome to give me feedback via Issue or contact me directly, and I will reply as soon as possible.

Contact:
thevoid2333@gmail.com
Or just create a issue.