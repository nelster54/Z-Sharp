<img src="https://raw.githubusercontent.com/sam-astro/Z-Sharp/master/ExtraResources/ZS-Gem-Icon-Small.png"/><img src="https://raw.githubusercontent.com/sam-astro/Z-Sharp/master/ExtraResources/ZS-Logo-Light-Small.png"/>

## Introduction
Z-Sharp is a custom programming language I made because I don't like c++ very much (Z-Sharp's interpreter is written in c++ though). It used to be called Slang, standing for "Stupid Lang", but another programming language called Slang already exists :(. Z-Sharp scripts have the file extension .zs. The base syntax and formatting I would say is quite similar to C#, but differs as task complexity increases. It has support for graphics using SDL2, and by default is not enabled.

## Installation
Downloading or installing is very simple. I recommend the regular version if you are just exploring, and not the installer, because then you don't need to find the executable in your program files. If you plan on developing for a long time though, then you should use the installer and I'll guide you through that after.
### ZSharp Windows x64
1. Navigate to [the most recent release](https://github.com/sam-astro/Z-Sharp/releases) and download `ZSharp-Win-x64.zip`.
2. Unzip `ZSharp-Win-x64.zip` and open the unzipped folder.
3. You will see many files. The Z# interpreter is `ZSharp.exe` and has a Z# icon. Any time you want to execute a script, this is the program that will be used. There are a few ways to use it:
    * Drag and drop any .ZS script directly onto the executable.
    * Use command line, providing path to executable and then to script like so:
    `> ./ZSharp.exe ./Pong-Example-Project/script.zs`
    * Right-click on your .ZS script file, then select `'Open with...'`. Click `'More Apps'`, scroll down, and select `'Look for another app on this PC'`. Navigate to the `ZSharp.exe` executable and select it. Now whenever you double-click any .ZS file, it will automatically open with the interpreter.
4. Feel free to use and edit the included `Pong-Example-Project`. It is a single script called `script.zs`, and you can open it with any of the methods above.
### ZSharp Linux
1. Navigate to [the most recent release](https://github.com/sam-astro/Z-Sharp/releases) and download `ZSharp-Linux.zip`.
2. Unzip `ZSharp-Linux.zip` and open the unzipped folder.
3. You will see some files. The Z# interpreter is `ZSharp`. Any time you want to execute a script, this is the program that will be used. You can use it like so:
    * Use terminal, providing path to executable and then to script like so:
    `$ ./ZSharp ./Pong-Example-Project/script.zs`
4. Feel free to use and edit the included `Pong-Example-Project`. It is a single script called `script.zs`, and you can open it with any of the methods above.
### ZSharp Installer Windows x64
1. Navigate to [the most recent release](https://github.com/sam-astro/Z-Sharp/releases) and download `ZSharp-Installer-Win-x64.zip`.
2. Unzip `ZSharp-Installer-Win-x64.zip` and open the unzipped folder.
3. You will see some files. Both the .EXE and the .MSI both do exactly the same thing, so you may execute either to begin the installation. Follow the steps in the wizard as it guides you through the install process. Make sure to remember the directory where you install it (the default one is `C:\Program Files\ZSharp`).
3. Navigate to the directory you installed Z-Sharp (the default one is `C:\Program Files\ZSharp`).
4. You will see many files. The Z# interpreter is `ZSharp.exe` and has a Z# icon. Any time you want to execute a script, this is the program that will be used. There are a few ways to use it:
    * Drag and drop any .ZS script directly onto the executable.
    * Use command line, providing path to executable and then to script like so:
    `> ./ZSharp.exe ./Pong-Example-Project/script.zs`
    * Right-click on your .ZS script file, then select `'Open with...'`. Click `'More Apps'`, scroll down, and select `'Look for another app on this PC'`. Navigate to the `ZSharp.exe` executable and select it. Now whenever you double-click any .ZS file, it will automatically open with the interpreter.
5. Feel free to use and edit the included `Pong-Example-Project`. It is a single script called `script.zs`, and you can open it with any of the methods above.

## Here is some example code:
```c++
// Comments are indicated by two forward slashes
// They can only be on their own line
//    int j = 4 // <- This is invalid comment placement

// All programs start with a main function
func Main()
{
    int i = 0
    string s = "r"
    
    i += 2
    i -= 1
    i /= 3
    i *= 2
    
    while i < 10
    {
        i += 1
    }
    
    if s == "r"
    {
        print s + " is r"
    }
    
    int functionNumber = ExampleFunction("A", s)
    ExampleFunction(1, 3)
    
    GlobalFunction()
}

// Declare new function with 'func', then it's name, and the names of any input variables.
// The input variables don't need type, as those are automatic. Also, they don't need to
/// be assigned at all on execute and can be left blank
func ExampleFunction(inputA, inputB)
{
    print "In A is: " + inputA
    print "In B is: " + inputB
    
    // Return a value to the valling location
    return 4
}

func GlobalFunction()
{
    // Create variables that can be accessed from anywhere (ex. in Main or ExampleFunction) with the 'global' keyword before type
    global int x = 12
    global string y = "Y String"
}
```
Here is how to use graphics:
```c++
func Main()
{
    int screenWidth = 500
    int screenHeight = 500
    ZS.Graphics.Init("Title of window", screenWidth, screenHeight)
    // After graphics are initialized, the main function will not finish.
    // Instead, Start() will be called a single time, then Update() every frame after that.
}

// Runs once at start of graphics initialization
func Start()
{
    // Vec2 are initialized using function 'NVec2(x, y)'
    Vec2 position = NVec2(250, 250)
    Vec2 scale = NVec2(20, 20)
    float rotation = 0

    // Sprite object, stores (and loads from file) the texture, location, scale, and rotation
    global Sprite exampleSprite = ZS.Graphics.Sprite("./square.png", position, scale, rotation)
}

// Executes each frame
func Update()
{
    // Draws the image created in Start(). This is usually at the end of update.
    ZS.Graphics.Draw(exampleSprite)   
}
```
Currently, ZSharp is ***VERY*** strict with formatting, and can throw an error if you forget to put a space somewhere.
Also, speaking of errors, if your code has any it will show in the console. Errors are colored red, and warnings are colored yellow. A line number will also usually be provided. This is ***Not*** the line relative to the *documents* beginning, but rather the *functions* beginning.
Example:
```
ERROR: line 5 in function Main
```
This is the 5th line *inside of Main*.
```c++
func Main()
{
   // line 1
   // line 2
   // line 3
   // line 4
   int g = "s"
   // ^ above line is the error, since it is line 5
}
```
I am planning to change how error reporting works to report the document line number as well, but this is how it is for now.
