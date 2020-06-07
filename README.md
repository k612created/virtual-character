# virtual-character
`virtual-character` is an application written in Python. <br>
I tried to code it in C++, but I realized it's nearly impossible for me to write an interpreter in C++ to analyze and instantiate
character objects. <br>

But I wrote an app in C++ to call `virtual-character.py` instead of typing `python virtual-character` all the time.

Also, `vcFunction.sh` is available for Linux users.

## How to custom my own character?
`virtual-character` uses **Python** as the script language. Just code a class in **Python** and enjoy.

`virtual-character` will use this in the application:
<br> Calling a character: <br>
```
  eval('<CustomCharacterClass>(<Filename>).<CalledFunction>()')
```
<br> Creating a character: <br>
```
  eval('<CustomCharacterClass>().createNew(sys.argv)')
```
<br>
and so you gonna write your own config file format!

Besides, these function are required in your own script:
```
  def __init__(self, filename = ''):
    # This function instantiates an object using the data in the file.
    <Your own code here . . .>
    pass
  
  def createNew(self, param):
    # This function analyzes the data in the argument 'param' and creates a new object.
    # Make sure this function saves the data in a file.
    <Your own code here . . .>
    pass
```

## Use `virtual-character` with C++
Download and compile the file `vc.cpp` using this command:
```
	g++ -o vc vc.cpp -lm
```
Or, you can copy these lines of code to any text editor and save it as `vc.cpp`.
```
	#include <cstdlib>
	#include <string>
	
	// If you are a windows user, remove the backslashes in the next line:
	// #define WINDOWS
	
	// Or, if you are a *nix user (OSX also counts), remove the backslashes in the next line:
	// #define UNIX
	
	using namespace std;
	
	int main(int argc, char** argv) {
		string x = "";
		#ifdef WINDOWS
			x += "python ";
			for (int i = 0; i < argc; i++) {
				x += string(argv[i]) + " ";
			}
		#endif
		
		#ifdef UNIX
			x += "python3 ";
			for (int i = 0; i < argc; i++) {
				x += string(argv[i]) + " ";
			}
		#endif
		
		system(x.c_str());
		return 0;
	}
```
