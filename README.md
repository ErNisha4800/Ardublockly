# Ardublockly
Ardublockly is a visual programming editor for Arduino. It is based on Google's [Blockly][1], which has been forked to generate [Arduino][15] code.

The `ArdublocklyServer` Python package initialises a local server to be able to compile and load the Arduino code using the [Arduino IDE][2].

This is all packaged in a self contained executable desktop application for Windows, Mac OS X, and Linux.

![Ardublockly desktop program screenshot][desktop_screeshot]


## Features
* Generates Arduino code with visual drag-and-drop blocks
* Uploads the code to an Arduino Board
* Useful "code block warnings"
* Compatible with a wide range of official Arduino Boards
* Works on Windows / Linux / Mac OS X

Ardublockly is still under development and a few features are not yet implemented. A to-do list can be found in the [TODO.md][3] file.

Currently tested under Windows with Python 2.7 and 3.4 and in Linux and MacOS X with Python 2.7.


## Cloning the repository
Please note that there are submodules in the repository that need initialisation. So, to correctly clone the Ardublockly repository:

```
git clone https://github.com/carlosperate/ardublockly.git
cd ardublockly
git submodule update --init --recursive
```


## Installing
The desktop application is available for Windows/Mac/Linux and runs as a stand-alone executable that can be downloaded from the [Ardublockly repository releases page][4].

You will also need the [Arduino IDE version 1.6.x or higher][2].

#### Development builds
You can also test __UNSTABLE__ development builds automatically generated every time an update is added to the GitHub repository:

| Linux build         | Windows build       | Mac OS X build       |
|:-------------------:|:-------------------:|:--------------------:|
| [![Linux Build Status](https://circleci.com/gh/carlosperate/ardublockly/tree/master.svg?style=svg)](https://circleci.com/gh/carlosperate/ardublockly/tree/master) | [![Windows Build status](https://ci.appveyor.com/api/projects/status/t877g920hdiifc2i?svg=true)](https://ci.appveyor.com/project/carlosperate/ardublockly) | [![Mac Build Status](https://travis-ci.org/carlosperate/ardublockly.svg?branch=master)](https://travis-ci.org/carlosperate/ardublockly) |
| [Download Link][12] | [Download Link][13] | [Download Link][14]  |

#### "Core version" (Python server only)
If you prefer, the core software can be used by running only the Python server, which loads the web interface on your local browser (Chrome recommended).

Full installation instructions for this version can be found in [this Github repository Wiki][5].

The quick version: Clone this repository, initialise all submodules, and execute:

```
python start.py
```

This will work on Windows, Linux (including ARM) and Mac OS X, with Python >2.7 or >3.4


## Running
1. [Install Ardublockly][5].
2. Install the [Arduino IDE][2] version 1.6.x or higher (latest version is always recommended).
3. Run Ardublockly as defined in your installation method.
3. Configure Ardublockly to locate the Arduino IDE [following these instructions][6].


## Online Demos
A demo of the latest release of Ardublockly main interface can be found in the following two links (to load the code into an Arduino it requires the full Ardublockly application to be downloaded and run on your computer):

#### [Ardublockly][10]
![WebApp screenshot responsive design][web_screenshot_responsive]

#### [Ardublockly classic][11]
![WebApp screenshot][web_screenshot_classic]


## Documentation
The documentation, including installation instructions, configuration instructions, and developer information can be found in the [Ardublockly GitHub repository Wiki][7].

To download the documentation you can git clone the wiki data:

```
git clone https://github.com/carlosperate/ardublockly.wiki.git
```


## Credit
This project has been inspired by [BlocklyDuino][16].

Blockly original source is Copyright of Google Inc. [https://developers.google.com/blockly/][1]. A list of changes to the Blockly fork can be found in the [Blockly subdirectory README][17] file.


## License
Copyright (c) 2016 carlosperate https://github.com/carlosperate/

Unless stated otherwise, the source code of this projects is
licensed under the Apache License, Version 2.0 (the "License");
you may not use any of the licensed files within this project
except in compliance with the License.

The full document can be found in the [LICENSE][9] file.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


[1]: https://developers.google.com/blockly/
[2]: http://www.arduino.cc/en/main/software/
[3]: TODO.md
[4]: https://github.com/carlosperate/ardublockly/releases/
[5]: https://github.com/carlosperate/ardublockly/wiki/Installing-Ardublockly
[6]: https://github.com/carlosperate/ardublockly/wiki/Configure-Ardublockly
[7]: https://github.com/carlosperate/ardublockly/wiki
[8]: https://github.com/carlosperate/ardublockly/compare/blockly-original...master
[9]: https://github.com/carlosperate/ardublockly/blob/master/LICENSE
[10]: http://ardublockly.embeddedlog.com/demo/index.html
[11]: http://ardublockly.embeddedlog.com/demo/classic/index.html
[12]: http://ardublockly-builds.s3-website-us-west-2.amazonaws.com/index.html?prefix=linux/
[13]: http://ardublockly-builds.s3-website-us-west-2.amazonaws.com/index.html?prefix=windows/
[14]: http://ardublockly-builds.s3-website-us-west-2.amazonaws.com/index.html?prefix=mac/
[15]: http://www.arduino.cc
[16]: https://github.com/BlocklyDuino/BlocklyDuino
[17]: blockly/README.md

[desktop_screeshot]: http://carlosperate.github.io/ardublockly/images/screenshot_desktop_1.png
[web_screenshot_responsive]: http://carlosperate.github.io/ardublockly/images/screenshot_material_all_small.jpg
[web_screenshot_classic]: http://carlosperate.github.io/ardublockly/images/screenshot_1.png


Building Ardublockly
 
Carlos edited this page on May 7, 2017 · 9 revisions
Building Ardublockly
The package folder contains the Electron project and Python scripts required to package Ardublockly into a stand-alone executable. This way it can be distributed without any dependencies other than having the Arduino IDE.

The application can be categorised in three main components:

Python server
HTML/Javascript front end
Desktop application wrapper (Electron).
The Python server is packaged into its own stand-alone executable using PyInstaller.

The desktop wrapper is based on Electron, which uses node.js. The node.js component is only used where required for the application to integrate well with the individual desktop platforms. Originally the Chromium Embedded Framework Python bindings were used, but cross-platform maintenance proved to be problematic and Electron has provided a much smoother alternative.

Continuous Integration Build Servers
Each commit to the Ardublockly GitHub repository triggers the build servers to follow all these build steps and upload the build output to an online server to make them available for download.

There is a CI Server for each platform (Windows, macOS, and Linux) with their own configuration script. So it could be useful to have a look at these scripts if some of the instructions here are not completely clear:

Windows AppVeyor script: https://github.com/carlosperate/ardublockly/blob/master/.appveyor.yml
macOS Travis script: https://github.com/carlosperate/ardublockly/blob/master/.travis.yml
Linux CircleCI script: https://github.com/carlosperate/ardublockly/blob/master/circle.yml
Ardublockly build dependencies
Git
Git needs to be installed on the system and accessible through the command line interface.

Python
The build scripts included in the package folder were originally developed and tested on Python 2.7, and later the build system was moved to use Python 3.4. Therefore, while these scripts should still be compatible with Python 2, in their current form they have only been tested on Python 3.

While the "core version" of Ardublockly (command line server + browser-based GUI) should be fully compatible with both Python 2 and 3 (tested on Python 2.7 and 3.4), there is one particular step in this build process that requires Python 2.7.

If you are using Python virtual environments on Windows this collection of Python extensions binaries is highly recommended.

The specific versions of the Python dependencies can be found in the package/requirements.txt file.

PyInstaller
Converts Python scripts into stand-alone executables. PyInstaller can be easily installed using pip:

 pip install pyinstaller
MkDocs
MkDocs is a static page generator specifically designed for documentation using Markdown.

The project documentation is written and hosted in the Ardublockly GitHub Wiki. The build script for the documentation pulls its markdown files and converts them into an HTML static site for offline access.

More information about this procedure can be found in this article.

MkDocs can be easily installed using pip:

pip install MkDocs
Node.js
Node.js is required to run Electron. It can be downloaded from the official website.

The npm package manager should be included with node, which is used to deal with all the Electron application dependencies.

Download the Source Code
Download and initialise this project repository:

git clone https://github.com/carlosperate/ardublockly.git
cd ardublockly
git submodule update --init --recursive
If you have already downloaded the Ardublockly source code, make sure the submodules have been initialised. The submodules in this repository are the 'closure-library' in the project root directory, and 'ardublockly.wiki' in the 'package/ardublocklydocs/' folder. You can run the last git command listed above, from the project root directory, to ensure the submodule directories are not empty.

Build Instructions
First step: Blockly
When Blockly is compiled, all the source code contained in the blockly folder is compressed in the blockly/blockly_compressed.js, blockly/blocks_compressed.js, and blockly/arduino_compressed.js files (among others). The repository version of these compressed files might not be the most up-to-date, so the first step should be to compile Blockly to ensure the compressed files are up-to-date.

You will need Python 2.7 for this step, as the Blockly build script is not currently compatible with Python 3. You will also need to be online, as the Google's "Closure Compiler Service" is used. From the project root directory:

cd blockly
python build.py
At this point, to continue with the next steps you'll have to go back to the project root directory:

cd ../
Second step: Python server
To build the Python application all you have to do is execute the build_pyinstaller.py file from the project root directory. It is highly recommended to use Python 3 instead of Python 2 for this step:

python package/build_pyinstaller.py
The optional command line argument linux, mac, or windows can be provided, but the operating systems should be automatically detected.

This will remove any previous build directory, rebuild, and create any required launch script into the project root (ardublockly_run.sh on Linux, or ardublockly_run.bat on Windows).

Third step: Electron
Execute the following commands from the project root directory:

cd package\electron
npm install
npm run release
The npm scripts will automatically detect and deal with the operating system different build requirements.

At this point, to continue with the next steps, it is recommended to go back to the project root directory:

cd ../../
Fourth step: Documentation
Build the offline documentation by running the build_docs.py script from the project root directory (Python 3 recommended):

python package\build_docs.py
This will remove any previous build directory, rebuild it, and remove any temporary files.

Final Step: Packing all Ardublockly
This step is only meant if you wish to pack the Ardublockly application into a distributable form. You can pack Ardublockly running the following command from the project root directory:

python package/pack_ardublockly.py
The pack script is designed for the build servers to zip the required contents into a single file to be uploaded to cloud storage, so it does not pack all the repository source code. This script creates a new folder on the same level as the project root, removes unnecessary files from this copied directory, and then zips it and saves it into the folder 'upload' within the original project root.
