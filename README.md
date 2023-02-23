# doxygen
Contains installation, setup and usage guide for doxygen for code documentation


#### Table of Content
1. [Installation](#installation)
- 1.1. [ROS](#ros)
- 1.2. [Standard](#standard)
2. [Configuration File](#configuration-file)
3. [Tag Reference](#tag-reference)


## Installation

### ROS
[Link to rosdoc_lite](http://wiki.ros.org/rosdoc_lite)

Install rosdoc_lite:
```
apt-get install ros-$ROS_DISTRO-rosdoc-lite
```

Above command should install **doxygen** from upstream pacakge but if it doesn't you can run following command:
```
sudo apt-get install doxygen
```

Another approach would be to build **doxygen** from source. Refer section **1.2 Standard** in current chapter.

You can use **rosdoc_lite** to generate local copis of documentation. When you run the *rosdoc_lite* command, it will generate documentation into the *doc* folder of the local directory unless output directory is mentioned.
```
Usage: rosdoc_lite [options] [package_path]

Options:
	-h, --help                       Show this help message and exit.
	-q, --quit                       Suppress doxygen errors.
	-o OUTPUT_DIRECTORY              The directory to write documentation to.
	
	-t TAGFILE, --tagfile=TAGFILE    Path to tag configration file for Doxygen.
	                                 Ex: /home/user/tagfiles_list.yaml
	
	-g GENERATE_TAGFILE, --generate_tagfile=GENERATE_TAGFILE
					 This will generate a doxygen tagfile.
					 Ex: /home/user/tags/pacakge.tag
```

Generate documentation for a package:
```
rosdoc_lite <path_of_package>
```

### Standard
[Link to official guide](https://doxygen.nl/download.html)

You will require necessary build tools -> g++, python, cmake, flex, bison. For most of them you could go with apt-get install unless you require some specific versions.

Install them with this command:
```
sudo apt-get install g++ python cmake flex bison build-essential
```

Validate installation of each dependency one by one:
```
g++ --version
python --version
cmake --version
flex --version
bison --version
```

Clone official git repo for doxygen:
```
git clone https://github.com/doxygen/doxygen.git
```

Build and make:
```
mkdir build
cd build
cmake -G "Unix Makefiles" ..
make
```

Install build binaries:
```
make install
```

Check installation:
```
doxygen --version
```

## Configuration File

**This section is not required while documentating ROS Nodes as you will be using rosdoc_lite which configures all parameters automatically**.

Each project should have its own configuration file which is used by Doxygen. Inorder to create a template configuration file, use following command:
```
doxygen -g <config-file>
```
Here <config-file> is the name of the configuration file. If the file name is omitted, a file named **Doxyfile** will be created. If "-" (i.e. the minus sign) is used as the file name then doxygen will try to read the configuration file from standard input (stdin), which is useful for scripting. **Keep the default name of configuration file**.

Note:
- For a small project consisting of a few C and/or C++ source and header files, one can leave **INPUT** tag empty and doxygen will search for sources in the current directory.

- If the project is large, then source directory or tree should be assigned to **INPUT** tag, and add one or more file patterns to the **FILE_PATTERNS** tag (for instance *.cpp *.h). Only the files that match one of the patterns will be parsed.

- For recursive parsing of a source tree, set the **RECURSIVE** tag to YES.

- To omit all *test* directories from a source tree for instance, this can be used:
```
EXCLUDE_PATTERNS= */test/*
```

## Tag Reference 

Following tags should be placed at the top of file.

| Tag                         | Description       |
| --------------------------- | ----------------- |
| ```@file <FILENAME>```      | File Name         |
| ```@author <AUTHOR_NAME>``` | Author Name       |
| ```@brief <BRIEF>```        | Short description |
| ```@date <DATE>```          | Date              |

Example implementation: => FILE: WIDoc.hpp
```
/**
 * @file   WIDoc.hpp
 * @brief  WI Documentation Format
 * @author Somebody from WI
 * @date   2021-05-27
 ***************************************************/
```

Following tags should be used to document Functions, Classes, Methods and so on

| Tag                                  | Description                                                       |
| ------------------------------------ | ----------------------------------------------------------------- |
| **General Description**              |                                                                   |
|                                      |                                                                   |
| ```@brief```                         | Brief description of class or function (fits a single line)       |
| ```@details```                       | Details about class or function                                   |
| ```@author <AUTHOR NAME>```          | Inert author name                                                 |
|                                      |                                                                   |
| **Function Or Method Documentation** |                                                                   |
|                                      |                                                                   |
| ```@param <PARAM> <DESCR>```         | Function or method parameter description                          |
| ```@param[in] <PARAM> <DESCR>```     | Input parameter (C-function)                                      |
| ```@param[out] <PARAM> <DESCR>```    | Output parameter of C-style function that return multiple values  |
| ```@param[in, out] <PARAM> <DESCR``` | Parameter used for both input and output in a C-style function.   |
| ```@tparam <PARAM> <DESCR>```        | Template type parameter                                           |
| ```@trhow <EXCEP-DESCR>```           | Specify exceptions that a function can throw                      |
| ```@pre <DESCR>```                   | Pre conditions                                                    |
| ```@post <DESCR>```                  | Post conditions                                                   |
| ```@return <DESCR>```                | Description of return value or type                               |
|                                      |                                                                   |
| **Code Blocks**                      |                                                                   |
|                                      |                                                                   |
| ```@code ... <C++-Code>.. @encode``` | C++ code example.                                                 |
|                                      |                                                                   |
| **Miscellaneous**                    |                                                                   |
|                                      |                                                                   |
| ```@remark```                        | Additional side-notes                                             |
| ```@note```                          | Insert additional node                                            |
| ```@warning```                       |                                                                   |
| ```@see SomeClass::Method```         | Reference to some class, method, or website                       |
| ```@li```                            | Bullet point                                                      |
| ```@todo <TODO-NOTE>```              | TODO annotation, remainders about what is still needs to be done. | 

