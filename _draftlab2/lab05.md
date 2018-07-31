---
layout: lab
num: lab05
ready: true
desc: "Image Manipulation"
assigned: 2017-08-17 09:00:00.00-7
due: 2017-08-21 21:00:00.00-7
---

If you find typos or problems with the lab instructions, please report them on Piazza


# Learning Goals

In this lab you will apply your knowledge from Chapters 2-5 to manipulate and transform images. A key focus of this lab is to give you lots of practice with using loops in your python code. Note that while media files are not covered in Guttag, working with media requires many of the concepts and data types covered in lecture and in the book. 

Your learning goals are:

* Use a new data type: the tuple
* Import and export media (picture) files in PIL
* Use your programming knowledge so far to manipulate pixels in picture files
* Invent and implement algorithms to transform pictures 

# Work Flow 

* Step 1: Review Chapters 4 and Chapter 5 (Sections 5.1-5.5) of Guttag

* Step 2: Create a private github repo called spis17-lab05-Name1-Name2 (following the naming convention in past labs). 

* Step 3: For each of the programming exercises in this lab come up with a solution outline by discussing with your partner. Don't be in a hurry to start coding unless you have a fairly clear idea of a solution strategy and your first steps.

* Step 4: Unit test your code as much as possible (In most cases you should be able to inspect the outcome of your code visually but we encourage you to use the unittest framework as much as possible)

* Step 5: Track your progress by committing your code frequently to git. Submit your code by pushing it to git. You may do this multiple times.



## Introduction to the Python Imaging Library (PIL)

Our computers encode all data (pictures, games, files) as sequences of 0s and 1s.  They are just a digital kingdom of bits. Some of the text below is review, but be sure to read it over (quickly) anyway.

In your computer, images (pictures) are files stored on your hard disk. A digital image is logically a rectangular grid of pixels, which appear as squares when enlarged; each pixel then typically consists of 1 byte (8 bits) for a Black-and-White image or 3 bytes (24 bits) for a color image, where one byte (a value between 0 and 255) each is for Red (R), Green (G), and Blue (B). R, G, B are three ingredients for all visible colors; for example: blue is 0 redness + 0 greenness + 255 blueness, white is 255 redness + 255 greenness + 255 blueness, and brown is 165 redness + 42 greenness + 42 blueness, etc.. The following figure by Wikipedia shows a color image with enlarged pixels.

<p align="center">
![](/images/labs/images/Pixel-example.gif)
</p>

In this lab we'll work with the Python Imaging Library (PIL) which is a graphics library like turle designed for working with image files. So let's warm up!

## Getting familiar with PIL

Create a private repo called `spis17-lab05-Name1-Name2`, as you have done in lab02. Download the  "stone bear" picture below and save it in your github repo working directory. You can do this by right clicking on the image and selecting the option to save. Be sure to save the image as "stoneteddybear.jpg".

<p align="center">

![](/images/labs/images/stoneteddybear.jpg){:height="400px"}

</p>

Next, launch IDLE in the same directory that you stored the stone bear image.

Before we can manipulate a picture in PIL, we will need to tell Python and PIL where to find it.  To do this, you will need to specify the exact path to the picture on your computer.  You also need to tell Python about the PIL Image library.  We'll start by playing around with the teddy bear image in the shell.  In the shell, type the following to load the Image library into the shell (later you'll put this line at the top of your file).  

```
>>> from PIL import Image

```

Then, you can open the picture you just downloaded as an image as follows:

```
>>> stonebear = Image.open( "stoneteddybear.jpg" )

```

The argument to the open function tells Python where to find the image. If you are getting an error here it's probably because of a typo in your filename, or because you either placed the file in the wrong place or launched IDLE from a directory different from where the image was stored. 

To ensure that the command you just executed works you can show the image you just created:

```
>>> stonebear.show()
```

Logically, an image is a grid of pixels. The size of the "stone bear" picture is 600 x 800, i.e., 480,000 pixels. You can pick a specific pixel from the image by using the `getpixel()` function. The arguments of this function are a picture object and the pixel's X position and its Y position; the function returns the pixel object at the coordinate(X, Y) of the image. Note that in the image grid, the axis is a little different from the usual 2D Cartesian axis, in that it counts from upper left to bottom right. For example, in the following 18 x 18 image grid, the coordinate (11, 7) is the grey block. Note the index starts at 0.

<p align="center">
![](/images/labs/images/coordinates.gif){:height="400px"}
</p>

So, if you make the following statement:

```
>>> pixel = stonebear.getpixel( ( 100, 200) )

```

the pixel returned is a tuple representing the RGB values of the pixel on the 200th row from top, 100th column from left, in the stonebear image. You can see this by looking at the value stored in pixel.

```
>>> pixel
(166, 201, 239)
```

Now, let's see how to modify the colors of individual pixels in the image.  To modify a pixel use the putpixel function
```
>>> stonebear.putpixel( (100, 200), (0, 0, 0) )
```

The `putpixel` function takes two arguments: 

* a pixel coordinate  represented by an (x, y) tuple.  In the example below our first argument is: (100, 200) , which is a tuple representing a single pixel. Using this function, can modify one pixel at a time.

* a tuple representing the RGB color to set the pixel to.  In the example above, this color is (0, 0, 0), i.e. black.

After running the command above, show the bear image again (you need to run the .show() again) and see if you can find the modified pixel.  It's there!

If you have a hard time seeing the modified pixel, try the following code to turn a range of pixels black.

```
for i in range(100):
    stonebear.putpixel( (i, 200) , (0, 0, 0) )

```

After running the command above, show the bear image again and see if you can find the modified pixels.  It should be easier to see your modification this time around.

## Hiding the stone bear's face

Now we are going to start working in a file so that we can save our work.  If you haven't done so already, create a new Python file called "imaging.py" in your repo, and place the appropriate header comment at the top that descibes the content of the file.  Don't forget your header comment. 

Now, after the header comment, tell Python that you want to use the Image module from the PIL library, as follows:

from PIL import Image

Save your work and commit your change to git using the `git add .` , `git commit -m ""` commands.  Now you're ready to write your first function for this lab.

The stone bear is shy, and he wants you to cover his face using a dark rectangular area. To do this, you will write a function called blockHead which will transform the color of a specified range of the picture to be all black. The header for this function is 

def blockHead( im, startx, starty, endx, endy ):

im is the image to modify, startx and starty represent the x and y coordinates of the upper left corner of the box to paint black and endx and endy represent the x and y coordinates of the lower right corner of the image to paint black.  Your function will not return anything.  For reasons we will discuss in lecture, the image will be modified even after the function returns!

You might notice that blockHead is in fact not specific to blocking the head in the stone bear image, but rather will block any rectangle in any image, according to the parameters passed in. For the rest of this lab, we'll ask you to use nested loops and the putpixel method, so feel free to try this here.
Don't forget you can access the [documentation for the Image module](http://pillow.readthedocs.io/en/3.1.x/reference/Image.html)
When you have finished writing your function, test it by calling it in the shell to block the stone bear's face.  Note, to do this you will need to do the following as commands in the shell:
Create an image from the stone bear file (if you haven't done so already)
Call your blockHead method, passing in the appropriate arguments  The coordinates of the four corners of the rectangle are (240, 130), (450, 130), (450, 290), and (240, 290), starting from upper left, clockwise.  
Show the image after you call the function to make sure that the black rectangle appears as expected.
If your blockHead is implemented correctly, you should have the shy bear's head cover as follows (left - original, right - covered):

                

## Saving modified pictures

The last step of our warm-up: be aware you just changed a COPY of the stone bear image! Even though you see the change in the stone bear image, that change will not be saved when you exit Python.  What? What does that mean? 

Even after all your work playing with colors and hiding the bear's face in the previous activities, the original picture file has not changed!  To see this, open your "stone bear" file by opening the picture in your git directory and double clicking on the image file. You will find nothing changed. It looks like nothing has been done to it. Why?

Basically, the Python functions you've used are not directly processing the stone bear image on the hard disk.  Rather,  when you open an image, PIL makes a duplicate of that image and loads that duplicate copy into  memory. The copy, as you can imagine, is exactly what was assigned to stonebear, so whatever you have done to stonebear only happened to the copy of your "stone bear" image. 

As a programmer, you should always have the concept of the computer memory in your mind. This technique of loading a copy of a file to memory (which is relatively fast) rather than directly handing a file on the disk (slow) is very common. 

What if we we want to save the changes we've made to the file on disk? We will need to force computer to write the latest memory copies back to the disk, so that the files on the disk change, too.

Let's get back to the shy stone bear. If you correctly changed the stonebear, and you want the actual file of "stone bear" picture to be changed accordingly, you should use the Image.save function. Read the documentation to see how it works (HINT: It takes one argument, which is a string specifying where you want the file saved including its name) and save your modified stonebear picture now.  A word of advice: we recommend you don't apply the changes to the original "stone bear" image, but to a different file (let's say, "shystonebear.jpg" somewhere). This way you won't lose your original picture in case you blocked a wrong area of the shy bear.  

That is all for our warm-ups. Make sure you understand how all this works before launching into your tasks below.

## Invert Function

Way back in the days of film cameras and chemical processing of photo images, one step in the processing process produced a negative image.

We can achieve the negative (aka inverted) effect digitally by subtracting each of the original RGB values of a pixel from 255.

For example, if the pixel RGB values are 34, 67, 87, the new RGB values of that same pixel will be 255-34, 255-67, 255-87. Or 221, 188, 168.

But that is only for one pixel and an image consists of thousands, or even millions, of pixels. Here we will use for loops to traverse through the list of pixels in an image. 

Read over this function to get a sense of how to we will use nested loops to modify pictures

```
def invert( im ):
    ''' Invert the colors in the input image, im '''
    
    imsize = im.size
    width = imsize[0]
    height = imsize[1]
    # Note that the previous 3 lines could be replaced by the single line:
    # (width, height) = im.size()
    # We will use this shorthand below.  Ask a tutor if you are confused.

    for x in range(width ):
        for y in range( height ):
            (red, green, blue) = im.getpixel((x, y))
            newRed = 255-red
            newGreen = 255-green
            newBlue = 255-blue
            im.putpixel((x, y), (newRed, newGreen, newBlue))

```

Copy this function into your "imaging.py" file, load it and run it.  Again, you will need to follow the three steps from above to run this function:
* Create the stone bear image
* Run the function, passing in the image
* Show the image after running the function
Tired of typing these lines into the shell? You can actually place the lines that will execute the three steps above into your "imaging.py" file, outside of any function (below all the function definitions). Then, every time you press F5, you will automatically run these lines!
When you execute the invert function on the stone bear picture given to you. Your result should look similar to this.

<p align="center">
![](/images/labs/images/PIL/invertedbear.jpg){:height="400px"}
</p>

## Functions for YOU to write

NOTES: 

In all of the functions below, we would like you to use (nested) loops and the putpixel() function on the Image object. PIL already implements many of the things we're asking you to do below. However, we ask that you use the putpixel() function to re-implement this functionality so that you get practice implementing these more complex functions.

You should also test your functions after writing each one.  You should test them on the stone bear image, and AT LEAST ONE OTHER IMAGE. We suggest using your own picture available in one your earlier git hub repos :)

## Greyscale

Now that we have some experience changing the colors in a picture, we'll write functions to make greyscale and black and white (binary) images.  The concept of image luminance will help us out. In layman's terms, luminance is how bright or dark the colors in a pixel are (compared to white).

As (the almighty) Wikipedia calculates it, luminance is 21% red, 72% green, and 7% blue. Intuitively, this makes sense because if you think of standard red, green, and blue, green is the lightest and thus has highest positive impact luminance, while blue is darker and has a lower value for luminance. This is useful! You're going to calculate luminance for pixel operations.

Write a function called greyscale that takes an image as a parameter and modifies it to make it greyscale. For this, you'll want to do something similar to invert, except that we will first calculate the luminance of a pixel and then set each of the three color channels to this value.  Since luminance is an indication of how white/black a pixel is, just insert the same value in each of the three color channels!


<p align="center">

![alt-bear1](/images/labs/images/PIL/originalbear.jpg){:height="400px"} 
![alt-bear2](/images/labs/images/PIL/grayscalebear.png){:height="400px"}

</p>


Hint: Getting an OverflowError: unsigned byte integer is greater than maximum? This might be because your luminance calculation results in RGB values higher than 255. Make sure that all of your percentages add up to 1. Also, if you get "integer argument expected, got float", it may mean you are trying to assign red, green or blue a floating point value. You may solve this by using a typecast c = int(a/b) or doing an integer division c = a//b versus the floating point one c = a/b (Note that this is one of the differences between Python 2, which was used last year in SPIS, and Python 3, which we are using this year. In Python 2, the / with two integer arguments resulted in an int, while it results in a float for Python 3. See also (http://sebastianraschka.com/Articles/2014_python_2_3_key_diff.html#integer-division). This is one of the challenging issues when porting between these two different versions of Python).

## Binarize

Now, write a function called `binarize( im, thresh)`, which makes modifies im to be black and white based on a threshold luminance value (thresh) specified by the user. This threshold is a brightness value between 0 and 255 - if a pixel's RGB average is greater than the threshold value, then it should turn white, and if it is less than the threshold value, then it should turn black.

What is the expected behavior of binarize(im, 0) (for any image)?

What is the expected behavior of binarize(im, 255) (for any image)?

<p align="center">

![](/images/labs/images/PIL/binarizedbear.png){:height="400px"}

</p>

## Geometric Transformations!

The following four functions take an image as an argument and do some geometric transformations on it.  
Write `mirrorVert`: This function takes an image and modifies the image to mirror the photo across its horizontal axis (i.e., so that the top part is mirrored upside down on the bottom of the image). Hint: Think carefully about which pixels you need to loop over, and where each pixel in the top half needs to be copied to create the mirror effect.  Start with concrete examples. Then derive the general formula based on the pixel's location (x, y) and the height and width of the image.

<p align="center">

![](/images/labs/images/PIL/vertmirror.jpg){:height="400px"}

</p>

`mirrorHoriz`: Same as above, but mirroring across the vertical axis. Hint:  Instead of replacing the bottom rows with the reversed top rows (as you did in `mirrorVert`), you'll replace the last half of the pixels in every row with the reversed first half of the pixels.

<p align="center">

![](/images/labs/images/PIL/horizmirror.jpg){:height="400px"}

</p>

Write `flipVert`, a function which flips the image in a picture along its horizontal axis (so the result is that the bottom is on the top and the top is on the bottom). Again, think carefully about where each pixel needs to end up, how far your loop needs to run, and be careful not to overwrite the pixels in the bottom half of your image before you've copied them over into the top!

<p align="center">

![](/images/labs/images/PIL/flipvert.jpg){:height="400px"}

</p>

Next up, `flipHoriz`, flip the image on its vertical axis. This should work in the same way as flipVert but the flip occurs in the horizontal direction. 

<p align="center">

![](/images/labs/images/PIL/fliphoriz.jpg){:height="400px"}

</p>


The next three methods create and return a copy of the image passed in (i.e., use the return statement). They should NOT modify the original image.
The command below can be helpful. It creates a new image im, as a color image (this is what the RGB means), of a certain width and height given by the tuple.
```
    im = Image.new('RGB',(width,height))
```

* scale: Take an image as a parameter and create a copy of that image that is scaled to be half its original size.  Then return this scale copy. Hint: one way to do this is to skip every other pixel when copying from one image to the other.  Be careful with your coordinates so that you do not go out of bounds in the smaller image.

* blur: Again create and return a copy of the image that is passed in.  This copy will be a blur of the original image, created by combining neighboring pixels in some way (entirely up to you). You might consider averaging the RGB values of a designated 'square' of pixels, then changing each of these pixels' values to the average.

* randomGrid: Creates and returns a copy of the original image.  To create this copy it divides the image into an NxN grid (where the N is up to you, or make it an argument of the function) and randomly sorts the pieces of the grid across the image - "sliding puzzle"-style. Hint: you can use the random library (just google this). 
```
    import random
```

Now it's time to create your own effects!! Please be sure to include a comment or note to the tutors explaining what you did. Be creative!  There is literally no end to this assignment. Add any creative routines that you come up with to your public repo and continue working on the joint group mashup project.


## Submission

Submit your code to github using the usual `git add`, `git commit`, `git push` commands

Congratulations on finishing lab 5!!








