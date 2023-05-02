Download Link: https://assignmentchef.com/product/solved-comp1406-assignment-5
<br>
In this assignment, you will build a slider puzzle game from scratch.   The purpose  is to become familiar with event handling for various window components.

(1) <strong>Slider Puzzle Game</strong>

You will be creating the following application:

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/150.png?w=980&amp;ssl=1" class="aligncenter lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" class="aligncenter" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/150.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>This application represents a slider puzzle game.  There are 15 tiles that can be exchanged horizontally or vertically with a blank tile in order to shuffle the image pieces around.   When the tiles are arranged in the correct order, they form a complete image and the game is done.   The game is timed … so the faster you can complete the puzzle, the better your score.

The game must meet all of the following requirements:

<ul>

 <li>There is a 4 x 4 grid of 16 Buttons that will hold the images for a puzzle.  Your interface should show these buttons as indicated in the screen snapshot above.   Each button should be 187 x 187 pixels in size. With a 1 pixel spacing vertically and horizontally between each button.  You will need to set the padding to 0 for each button using setPadding(<strong>new </strong>Insets(0,0,0,0));</li>

</ul>

This will allow the image to take the full space in the button.   There are 4 sets of images available for you to use (although you can add your own as well).   These are available on the course website, where you downloaded the assignment.   All images must be unzipped and copied into the <strong>src</strong> folder of this assignment in order to be able to be loaded properly.   For each puzzle, there are 17 images … one is a thumbnail image which shows the whole image in 187×187 size.  The others are the individual tile images (each 187×187 in size) and are labeled with the format Name_RC … where Name is the name of the puzzle (i.e., Pets, Scenery, Lego or Numbers) and R is the row number and C is the column number for that image (i.e., 0, 1, 2 or 3).   Recall that you set the image for a button as follows:

setGraphic(<strong>new </strong>ImageView(<strong>new </strong>Image(getClass().getResourceAsStream(<strong>filename</strong>))));  where <strong><sub>filename</sub></strong> is a string representing the name of the file (e.g., “Lego_21”).   It may be a good idea to make sure that you can create the buttons and display all of the images from a puzzle in order on each button before you go any further on the assignment.

<ul>

 <li>Your GUI should also show the complete image (i.e., use the available <strong>Thumbnail</strong> image) as a <strong>Label</strong> and underneath it should be a <strong>ListView</strong> showing (at least) the names of the 4 puzzles. See snapshot above.</li>

 <li>There should be a</li>

</ul>

<strong>Start/Stop</strong> button (shown as <strong>Stop</strong> on the snapshot above) as well as a “Time:” <strong>Label</strong> and a <strong>TextField</strong> that shows the time that has elapsed since the puzzle was started.  All components must be

“nicely” arranged/sized with reasonably consistent margins all around.

<ul>

 <li>Upon window startup, the buttons should show the <strong>png</strong> image on</li>

</ul>

each button, the thumbnail <strong>Label</strong> should be enabled and the <strong>Start</strong> button should be <strong>DARKGREEN</strong> with

<strong>WHITE</strong> letters indicating “<strong>Start</strong>“.   The time should be “<strong>0:00</strong>“.  See image here.

<ul>

 <li>When an item is selected from the list, the appropriate image should be shown in the Thumbnail <strong>Label</strong>.</li>

 <li>When <strong>Start</strong> is pressed, the game should begin running. When the game is running, the following should happen:</li>

 <li>The Thumbnail <strong>Label</strong> should be disabled (it will look faded as in the first snapshot on this assignment).</li>

 <li>The <strong>Start</strong> button should become <strong>DARKRED</strong> and indicate “<strong>Stop</strong>” instead of “<strong>Start</strong>“.</li>

 <li>The images on the buttons should be changed to the 16 images for the tiles that make up the puzzle image. One of these tiles (chosen randomly) should remain as a blank one.  The tiles should be shuffled randomly (see first snapshot) … more will be mentioned about this below.</li>

 <li>A <strong>Timer</strong> should be started. Use a <strong>Timeline</strong> object (from the <strong>animation</strong> package).   Here is how to set up the timer to tick once per second.  You should set this up in the <strong>start()</strong> method:</li>

</ul>

<strong>updateTimer </strong>= <strong>new </strong>Timeline(<strong>new </strong>KeyFrame(Duration.<em>millis</em>(1000),

<strong>new </strong>EventHandler&lt;ActionEvent&gt;() {

<strong>public void </strong>handle(ActionEvent event) {

<strong>// FILL IN YOUR CODE HERE THAT WILL GET CALLED ONCE PER SEC.</strong>

} }));

<strong>updateTimer</strong>.setCycleCount(Timeline.<strong><em>INDEFINITE</em></strong>);

To start the timer, you use: <strong>updateTimer</strong><sub>.play();</sub>  This should be done when the <strong>Start</strong> button is pressed.   When the <strong>Stop</strong> button is pressed, you should stop the timer by using: <strong>updateTimer</strong>.stop();

<ul>

 <li>At any time that the game is running, the time should be displayed in the <strong>TextField</strong>, with proper formatting. That is, it should show the number of minutes that have elapsed, followed by a ‘<strong>:</strong>‘ character and then the number of seconds that have elapsed since the last minute (always shown as 2 digits).  You should use<strong>format() </strong>here.   You’ll have to keep track of the number of seconds that have elapsed since the timer was started.</li>

 <li>The game should stop if the user pressed the <strong>Stop</strong> button, or when the puzzle has been completed (more on this is described below). At this time, the timer should be stopped (use: <strong>updateTimer</strong><sub>.stop();</sub>) .  Also, the thumbnail <strong>Label</strong> should be <strong>enabled</strong> The <strong>Stop</strong> button should become <strong>DARKGREEN</strong> and indicate “<strong>Start</strong>” instead of “<strong>Stop</strong>“.  If the user pressed the <strong>Stop</strong> button, then all 16 tile buttons should show the BLANK.png image.  If the game ended due to tile completion, then all 16 tile buttons should be <strong>disabled</strong> and the blank tile should be replaced by the puzzle image that was missing from the start (you will want to remember which one was replaced by the blank image upon starting so that you can show it at this time).</li>

 <li>During the game, when the user clicks on a tile button, you should do the following. Determine which <strong>row</strong> &amp; <strong>col</strong> was clicked on (an example of this was given in chapter 5 of the notes with our <strong>ToggleButtonsApp</strong>).  Then you should look <strong>above</strong>, <strong>below</strong>, <strong>left</strong> and <strong>right</strong> of that <strong>(row, col)</strong> location to see if the blank tile is there (be careful of boundary cases).   If the blank tile is there, then the image on the blank tile should be swapped with the image of the tile that was clicked on.   Visually, it should appear that the clicked tile slides into the blank position, moving the blank position into its position.  It would be a good idea to create a method called <strong>swap(row,col) </strong>that takes the<strong> (row,col) </strong>of the button that was clicked on, and then attempts to find the blank image around it and swap it.</li>

 <li>To shuffle the images upon startup, it is good to start with the full 16 images, and then simply call your <strong>swap(row, col) </strong>method 5000 times or so. This will cause a bunch of tiles to be slid around and should give you a reasonable shuffling.   Then replace one of the tiles at random with the blank one.   Remember to keep hold of the replaced image so that you can show it at the blank spot when the puzzle is completed.</li>

 <li>To determine when the puzzle is complete, you will need to know when each tile piece is in the correct location. That is, image “xxx_00.png” should be at the top left with image “xxx_01.png” beside it, image “xxx_10.png” below it, etc…   It may be easiest to keep three 2D arrays.   One for the buttons, one for the images of each button, and one for the coordinate of each button (i.e., the row/col of the image for that button).   A coordinate can be stored using a <strong>Point2D</strong> object which has an <strong>x </strong>and <strong>y</strong>   You can determine when the board is complete by examining each button row by row and col by col (using the double FOR loop) and just check that the coordinate value matches the<strong> (row,col)</strong> of that button.   This will only work if you swap the coordinates along with swapping the images in your <strong>swap(row,col)</strong> method.  You do not have to do things this way, it is just an idea.   If you have a simpler way to determine when the board is complete, you can do that instead.</li>

</ul>




<ul>

 <li>Before you hand in your assignment, make sure that you are handing in ALL of the images along with it … in the same <strong>src</strong> You will lose marks if any image files are missing.</li>

</ul>




<ul>

 <li>Have fun with this game. You may add features (no bonus marks though) such as additional puzzles (<strong><u>DO NOT USE ANY INAPPROPRIATE IMAGES</u></strong>) or perhaps a <strong>TextArea</strong> or <strong>ListView</strong> on the window that shows a sorted list of “high scores” (lowest time is the highest score).</li>

</ul>





