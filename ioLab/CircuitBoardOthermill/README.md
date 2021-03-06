# Make a Circuit Board with Fritzing and Othermill
This tutorial describes how to create your very own printed circuit board (PCB) using the tools in Art & Technology Studies ioLab at the [School of the Art Institute of Chicago](http://www.saic.edu).  Here's what we will cover in this tut:

1. Using [fritzing](http://www.fritzing.org) to design the PCB for your project and export gerber files to be milled.
2. Importing the gerber files into the Othermill's control software, Otherplan.
3. Setting up the [Othermill](https://othermachine.co/) with a PCB blank and running a mill job.
4. Finishing your PCB and preparing to put it into use.

For this tutorial, let's assume that you already have downloaded [Fritzing](http://fritzing.org/download) and [Otherplan](https://othermachine.co/otherplan/), you have designed your PCB, you have some electronics experience and that you're proficient at breadboarding a circuit, soldering, and checking continuity with a multimeter.  I will be touching briefly on the example design, but there are many more in-depth tutorials over at http://fritzing.org/learning/.

Ok, let's get started!!

## 1. Using Fritzing to design the PCB.
If you're ready to design and fabricate a PCB, that usually means that you have already worked out your circuit on a breadboard.  You may even have soldered up one or two of said circuit on a protoboard. A dedicated PCB can save you space and keep you from having to solder a million jumpers all over your protoboard.  For this tutorial, we're going to use a PWM controller I designed based on [this circuit](http://makezine.com/projects/the-dial-a-speed/).  This circuit is a simple PWM generator based off of a 555 timing chip and it will show some of the features of that can make a PCB more desirable than a protoboard.  [Here](https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/555PWM.fzz) is the Fritzing file we'll be using (it is also in the assets folder of this repo).

So, we're going to open that up in Frizting, which should look a little something like this:

![alt text][1]
We are so done with breadboarding, though.  Let's move on to the PCB tab.  To get there you want to click on the button that says "PCB" up at the top of the page.  Alternatively, you can press ⌘4 to get there.

![alt text][2]

Ok, so now we have the PCB view up, and you can see that I already have all my components placed and the traces properly routed. Once I've got everything finalized, I want to do a quick design rules check (⇧⌘D) to make sure none of the traces cross or come too close to one another--this becomes more important with more complex boards and it will be easier to mill if it passes the DRC.

![alt text][3]

Once we've passed the DRC and we're ready to export, go to `File>>Export>>For Production>>Extended Gerber (RSX274X)`. Specify the folder you'd like to export to.

 *Hint: This action exports several files all at once, so I recommend creating a new folder for each project.  Just exporting it to your desktop or wherever will become a mess real fast.*

 *Double Hint: I try to design my boards to be single-sided. A double-sided board adds a layer of complexity and I try to avoid it when possible.  You can ensure that you're designing a single-sided board by clicking the gray board in Fritzing, and selecting "one layer (single-sided)" in the Inspector.  If you do this, you __must__ switch it back to double-sided right before you export.  If you don't, there will not be a "copper top" file to open in Otherplan.*

![alt text][4]

## 2. Preparing the file for milling in Otherplan
Open Otherplan and connect the Othermill to your computer with a USB cable.  Home the machine.
The material we are using in this tutorial is single-sided FR-1.  Measure the size of your blank and input it into the appropriate boxes. It is important when measuring the thickness of the board to include the layer of double-sided tape used to adhere the board to the mill.  If you don't include this, you may cut into the spoilboard.
In Otherplan, make sure that your material is aligned to the bracket.  This is handy for single-sided boards and essential for double-sided boards where the bracket provides the registration for the flip milling.

Click "Open Files..." and navigate to the folder you exported the Gerber files to.  Select the file that ends in ".gtl" (that's that "copper top" layer I was telling you about) and press "Open." The window that opens will ask you to choose which Gerber files to associate with the bottom, outline, and holes of your board.  Usually you won't have to change these, but you are able to if needed.

![alt text][5]

Your design should show up on the material in Otherplan.  You can change the location of the design by changing the values under "Placement."  Make sure that your design is offset from the material edge by a few millimeters so that the end mill does not cut into the bracket.

Specify which end mills you will be using for your job.  For this design, we will be using the 1/32" flat mill and the 1/64" flat mill.  There may be areas higlighted in red. That means that those areas will not be cut unless you use a smaller bit.  When adding text to the copper layer, (as is the case here) there will always be red, no matter what.  It will still turn out.  

![alt text][6]

**Note on double sided boards:** When cutting the first side, you only want to cut the traces.  Wait to cut the holes and outline when you do the other side.  You can select/deselect what features are cut by clicking the buttons labeled `Traces`, `Holes`, and `Outlines`.

## 3. Preparing the circuit board blank and mill
In order to mill a circuit board, our PCB blank needs to be affixed to the mill's bed so it won't move around while the job is running.  A few strips of double-sided tape will do the trick here.  Make sure there are no folds or crinkles in the tape and that the tape is not overlapping itself.  We want the board to be as level as possible for milling and even a double thickness of tape can throw things off. It should look something like this:

![alt text][7]

![alt text][8]

Next, we need to put the bit into the mill. Please refer to this [excellent tutorial](https://othermachine.co/support/basics/tool-locating/) from the Othermachine Co. for details on inserting and locating an end mill.  

![alt text][9]

When you have imported your design and chosen all the parameters, begin milling the board by clicking "Start Milling." There will also be an estimate of the time it will take to mill your board.  Otherplan will inform you when and how to change end mills.

## 4. Finishing
Once we have cut the traces and cut out the board, it is time to put it into use!!!  Use a scraper to get the PCB off the bed of the mill and remove all double-sided tape and dust from both the spoilboard and your PCB.  Don't forget to vacuum out the Othermill so it is clean for the next person!

![alt text][10]

![alt text][11]

At this point, inspect the board for any potential problems.  the edges of the traces should be smooth.  If there are any burrs, they can be gently sanded away or cut away with a utility knife.  Check each of the pads and connections for continuity.  Make sure the traces that should be electrically connected are and make sure things that shouldn't be electrically connected aren't.  Check the large empty areas of copper left on your board in addition to the traces.  If you have a connection where there shouldn't be one, inspecting the board under a magnifying glass or microscope can help.  Sometimes small bits of copper get stuck in the troughs and connect two adjacent pieces of copper.

If you have been handling your PCB a lot, you may want to give it a wipe down with some alcohol or acetone to take finger oils off of the copper. These oils can make soldering difficult and corrode the copper in the long run.  Handle the board with gloves or by the edges after you do this.

You are now ready to solder in your components!  This is what mine looked like when I was all done:

![alt text][12]

This concludes the tutorial.  





[1]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/BreadboardView.jpg?raw=true "Breadboard view."
[2]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/PCBView.jpg?raw=true "PCB View."
[3]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/PCBViewDRC.jpg?raw=true "Design Rules Check (very important!)."
[4]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/PCBViewDExport.jpg?raw=true "Export Gerber."
[5]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/OtherplanSelectFiles.jpg?raw=true "Selecting Gerber files."
[6]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/OtherplanPlacement.jpg?raw=true "Placement and bit selection."
[7]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/Tape.jpg?raw=true "Tape on back of PCB blank."
[8]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/Blank.jpg?raw=true "PCB blank on Othermill."
[9]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/EndmillCollet.jpg?raw=true "End mill in collet."
[10]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/Scraper.jpg?raw=true "Using scraper to get board off."
[11]:https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/FinishedBoard.jpg?raw=true "Finished board."
[12]: https://github.com/SAIC-ATS/Tutorials/blob/master/ioLab/CircuitBoardOthermill/assets/images/Soldered.jpg?raw=true "Soldered all up!"
