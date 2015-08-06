## MovingImages-RubyTests
The system tests written in ruby for end to end testing of the MovingImages Launch Agent

#### Running tests from the command line

If you haven't already done so, you will need to install the moving_images ruby gem and the LaunchAgent to be able to test MovingImages. This is done using the MovingImages application.

The pdf-reader ruby gem is needed for running the tests. You can install the gem `gem install pdf-reader`

The ruby gem works with the default ruby installation in Yosemite and ruby 2.2.1 installed using rvm also on Yosemite.

To run all tests then run the command `runtests`. Each test script file is independent and can be run seperately, these scripts are test001, test002 ... etc.

#### Test script descriptions

These descriptions are a guide only to what is being tested. The point of these descriptions is as a guide to users when looking for code examples as to how to do things using ruby with MovingImages

##### test001 - Smig, MovingImages LauchAgent, Counting objects and closing all objects.

1. Gets the version number of the command line tool smig that communicates with the MovingImages LaunchAgent
2. Gets the version number of the LaunchAgent
3. Checks that you can obtain and set the launch agent idle time.
4. Checks that MovingImages returns the number of base objects currently existing, including by object type.
  * Checks that closing all objects, closes all objects.

##### test002 - Image importer base objects

1. Getting a list of image file formats an image importer can import and image exporter can export.
2. Creating an image importer from a image file and closing an image importer
3. Getting specific properties of an image importer base object.
4. Getting specific properties of an image in a image importer base object. Width, Height, exposure time, fNumber.

##### test003 - Bitmap base objects and string properties including draw basic string dimensions

1. Get a list of bitmap context presets.
2. Creating a bitmap context, keeping track of number of bitmap objects created.
3. Getting properties of a bitmap context
4. Get draw string dimensions for various string texts with properties
5. Getting a list of user interface fonts

##### test004 - Getting information about various CoreImage filters

1. Get a list of all the core image filters
2. Create a json file for every coreimage filter that describes the filter & its properties
3. Create a property list file for every coreimage filter that describes the filter & its properties

##### test005 - Creating objects with a name and identifying objects

1. Creating a bitmap context with a name.
  * Identifying that object by object type (bitmapcontext) and index
  * Getting the object the unique object reference
  * Closing an object using the name/object type identifier.
2. Create an image importer object without specifying an object name
  * Check that the image importer object has a default name which is the full path to the imported file.
  * Check that referring to the image importer object by object type and index works
3. Accessing an image importer object as part of a draw command in a bitmap context
  * Create an image importer object with a name specified
  * Create a bitmap context
  * Have bitmap context draw command draw an image belonging to image importer into context.
    * Identify the image importer object in draw command by object type and name.
 
##### test006 - Drawing images into a bitmap context - do rotation, scaling and drawing with transparency

This test file also exports the generated image and then compares the created image with a previously created image

1. Draw a cropped image into a bitmap context. Save the image and compare.
2. Draw a rotated image into a bitmap context, rotated around its centre. Save the image and compare
3. Draw a rotated image into a bitmap context, by specifying an affine transform.
4. Draw a rotated image into a window context.
5. Draw an image into a bitmap context with an alpha value of 0.5

##### test007 - Tests drawing text and shapes into a bitmap context - draw text into a pdf context

1. Draw text constrained to an oval, a rectangle and a path.
2. Draw text using different fonts, different font sizes, different colours, both stroking and filling text
3. Draw various shapes into a bitmap context and draw a stroked rectangle rotated around its centre.
4. Draw text into a pdf context
5. Repeat 2, but draw into a window context.
6. Draw text with an inner shadow.

##### test008 - Drawing paths.

1. Draw paths, both stroked and filled.
2. Draw a path with an inner shadow

##### test009 - Tests drawing an array of shapes

This test is about testing that when drawing an array of different shapes that drawing properties can be set which apply to all elements to be drawn but that when a specific shape is being drawn those same properties can be specified again which override those set when defining the array of elements drawing.

##### test010 - More shape drawing tests

1. Draw some more basic shapes which haven't previously drawn including a linear gradient object
2. Draw a radial gradient

##### test011 - Test using CoreImage filters

1. Test of various simple CoreImage filters, just applying a single filter to an image.
2. Test of various CoreImage blend filters first drawing a background image & then foreground image with filter.
3. Construct a filter chain made up of five different core image filters.
  * Uses radial gradient filter, crop filter, height field mask filter, shaded material filter, bump distortion filter

##### test012 - Test of taking, drawing and clearing snapshots. Test cleanup commands

You can take a snapshot of a bitmap context or window context and draw that snapshot back into the context later.

Cleanup commands are commands that run after the last command in the main list of commands has run. The cleanup command will always run even if the main list commands did not finish and all cleanup commands will be attempted. The cleanup commands will mostly be close object commands or remove images from the image collection.

1. Test snapshot in a bitmap context
2. Test snapshot in a window context
3. Test cleanup commands

##### test013 - Tests using equations and variables and calculating graphic size of text. Test MIMeta

1. Uses equations and variables for positions, sizes, colours and shadow blur of shapes being drawn.
2. Testing that equations work when specifying source & destination rectangles when rendering a filter chain.
3. Calculate graphic text size using user interface fonts and post script fonts.
4. Test MIMeta returns correct values for core graphic blend modes, presets, video writer presets
5. Test getting pixel data works for a floating point backed bitmap context.
  * Test getting pixel data works for a 8 bit per component integer based context.
6. Test the getproperties command by getting image properties from an image works.

##### test014 - Draw arcs, use equations, apply clipping

1. Draw a path made up of arcs and stroke.
2. Set up a clipping path, and then draw an image which will have its drawing clipped.
3. Use a grayscale image as an image mask before drawing an image.

##### test015 - Movie Importer objects

1. Getting various bits of metadata from a movie importer about the movie file
2. Getting various bits of metadata from a video track in a movie importer object
3. Get an image composed from all video tracks in a movie file at a specific movie time. Compare.
4. Get an image composed from a single video tracks in a movie file at a specific movie time. Compare.

##### test016 - Using the image collection. MovieImporter object process frames command.

1. Add, access and remove an image in the collection, original source from a movie frame.
    * Draw the image in the image collection to a bitmap context.
2. Add an image created from a bitmap context and add it to the image collection.
    * Confirm that the image can be drawn
    * Confirm that the image can be drawn after its image source is taken away.
    * Confirm that the image is removed from collection by trying to draw again.
3. Use the processing frames command to apply a sequence of commands to movie frames.
    * This is probably one of the most complex commands to use.

##### test017 - Tests the movie video writer object

1. Test writing as different movie formats. mp4, m4v, mov.
    * Test creating and closing a video frames writer object.
2. Tests adding a video input to the video frames writer object.
3. Test reading frames from an imported movie and then adding frames to the video writer.

##### test018 - Tests the movie video editor object

1. Get a list of export presets. Get the number of movie editor objects
2. Create a movie editor, check that the number of movie editor objects is 1.
    * Add a video track, check that the number of video tracks is 1.
    * Add a content segment. Get the segment mappings.
    * Add an empty segment, and then another content segment.
    * Get the segment mappings.
    * Add a single passthru segment for the length of the movie.
    * Save the composition map to a file.
    * Compare with a previsouly created composition map.
    * Export the video composition.
    * Check that the video composition is right length and size.
3. Create a movie editor object with multiple video tracks with composition instructions.
    * Create movie editor and add 3 video tracks.
    * Confirm that the number of tracks is 3.
    * Add video content to all 3 video tracks.
    * Add video composition instructions.
    * Save the composition map to a file.
    * Compare with a previsouly created composition map.
    * Export the video composition.
    * Check that the video composition is right length and size.
   