# MovingImages-RubyTests
The system tests written in ruby for end to end testing of the MovingImages Launch Agent

### Running tests from the command line

If you haven't already done so, you will need to install the MovingImages. This is done with the MovingImages application.

To run all tests then run the command runtests. Each test script file is independent and can be run seperately, these scripts are test001, test002 ... etc.

### Test script descriptions

These descriptions are a guide only to what is being tested. The point of these descriptions is as a guide to users when looking for code examples as to how to do things using ruby with MovingImages

#### test001 - Smig, MovingImages LauchAgent, Counting objects and closing all objects.

1. Gets the version number of the command line tool smig that communicates with the MovingImages LaunchAgent
2. Gets the version number of the LaunchAgent
3. Checks that you can obtain and set the launch agent idle time.
4. Checks that MovingImages returns the number of base objects currently existing, including by object type.
  * Checks that closing all objects, closes all objects.

#### test002 - Image importer base objects

1. Getting a list of image file formats an image importer can import and image exporter can export.
2. Creating an image importer from a image file and closing an image importer
3. Getting specific properties of an image importer base object.
4. Getting specific properties of an image in a image importer base object. Width, Height, exposure time, fNumber.

#### test003 - Bitmap base objects and string properties including draw basic string dimensions

1. Get a list of bitmap context presets.
2. Creating a bitmap context, keeping track of number of bitmap objects created.
3. Getting properties of a bitmap context
4. Get draw string dimensions for various string texts with properties
5. Getting a list of user interface fonts

#### test004 - Getting information about various CoreImage filters

1. Get a list of all the core image filters
2. Create a json file for every coreimage filter that describes the filter & its properties
3. Create a property list file for every coreimage filter that describes the filter & its properties


