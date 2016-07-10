---
layout: single
date: 2016-07-08
published: true
author_profile: true
title: "How to make a partial UITableView expand with AutoLayout in a UIScrollView"
---

One of the trickiest things about getting started with iOS development is wrapping your head around Auto Layout. I really struggled to get going with Auto Layout until I set aside a couple of days to do some specific tutorials and build some small test applications to practice the layouts I wanted to create. If you're struggling with Auto Layout I would highly recommend any of the tutorials on Ray Wenderlich, they are excellent and quickly put a stop to the desire to make individual layouts for each screen size.

In Stock Controller App I wanted to have a tableView that would expand to fill the lower portion of the view, like the below images show.

![iPhone screen size comparisonn](/images/SCA UI/SCA screen size comparison.png){: .align-center}

<!-- more -->

Initially this seemed fairly straight forward to make, you just set the UITableView edge distances to 0 and don't give it a fixed height or width. The complication came when I discovered that to make the text boxes in the lower portion of the table visible and editable when the keyboard is on screen I would need to embed everything in a UIScrollView and move the content up when the keyboard appeared. This makes the initial method fail, because for a UIScollView to be happy, everything inside it has to have a knowable height and width so that it can set its content size - not easy when the whole point of the table view is to expand to take up the remaining space on the screen depending on the device size.

This is a quick guide on how to solve this problem (since I couldn't find one and had to spend a good few hours working it out), I'll walk you through making one of the Stock Controller App screens as it's a reasonably tricky layout and once we're done you'll have a pretty good idea of how to get Auto Layout working well.

### Step 1

Create a single view application. First select the initial view controller go to Editor > Embed In > Navigation Controller. Then, select the initial view controller (now a navigation controller) and change the screen size to "iPhone 4-inch" - given that it's easier to scale up a design and the iPhone 5/S/SE are all very popular I like to design for the smaller screen size in the knowledge that everything will scale up well.

![step 1](/images/SCA UI/SCA UI S1.png){: .align-center}

### Step 2
Now drag out a UIScrollView. Drag it out to fill all of the space under the navigation bar and the set the margins to 0 on all 4 sides, make sure "Constrain to margins" is unchecked and click "Add 4 Constraints".

![step 2](/images/SCA UI/SCA UI S2.png){: .align-center}

### Step 3

Now drag out a UIView and expand it to fill the whole of the UIScrollView. Same as above, select the UIView and set the top, leading, trailing and bottom constraints to 0.

![step 3](/images/SCA UI/SCA UI S3.png){: .align-center}

### Step 4

Even though we have pinned the UIView to the UIScrollView edges the view still doesn't have a width. So, in the document outline control drag from the View in the Scroll View to the View Controller's main View and select "Equal Widths". 

![step 4](/images/SCA UI/SCA UI S4.png){: .align-center}

### Step 5

Now we need to add the rest of the content so that we can give our Scroll View content a height. We'll attack this next bit in 3 steps. First, pull out an image view and two text fields. See the image below for the dimensions and positioning. Remember that we're not doing anything in auto layout with these yet, just get everything laid out and we'll add auto layout constraints in a few steps time.

![step 5](/images/SCA UI/SCA UI S5.png){: .align-center}

### Step 6
Pull out 3 text fields, 3 labels and 2 UIViews. Make the width of the UIViews 1 and set the background to a middle gray to create the vertical lines. The image below will help you lay it out, the gray lines are 65 long. Xcode's guide lines will help you lay this out just make sure the the middle text field is centered in the screen and horizontally center the labels below the text fields.

![step 6](/images/SCA UI/SCA UI S6.png){: .align-center}

### Step 7
Final bit to get the UI together is to pull out a navigation bar and a table view. Set the Y position of the navigation bar to 178 and then drag the table view out to fill the rest of the remaining space.

![step 7](/images/SCA UI/SCA UI S7.png){: .align-center}

### Step 8
Now we start to add auto layout constraints. Start with the image, set the height, width, top space and leading space as the image below and click Add 5 Constraints. Don't worry about any red lines that appear at this stage, they will go away as we go - have faith!

![step 8](/images/SCA UI/SCA UI S8.png){: .align-center}

### Step 9
Select the top text field, set the top space, height, leading and trailing space. 

![step 9](/images/SCA UI/SCA UI S9.png){: .align-center}

### Step 10

Control drag from the second text field up to the first and select Vertical Spacing. Then select the second text field and set the leading space, trailing space and height. Do not select the top space!

![step 10](/images/SCA UI/SCA UI S10.png){: .align-center}

### Step 11

Now control drag from the first of the three labels to the image view and select Vertical Spacing.

![step 11](/images/SCA UI/SCA UI S11.png){: .align-center}

### Step 12

Now select all three labels and set their heights and for them to have equal widths.

![step 12](/images/SCA UI/SCA UI S12.png){: .align-center}

### Step 13

You can do this next bit a couple of ways but this is my preferred method. Control drag from the middle label to the left label and select Top - this will align their top edges. Do the same for the label on the far right.

![step 13](/images/SCA UI/SCA UI S13.png){: .align-center}

### Step 14

Control drag from the vertical gray lines (do this in the document outline if they are tricky to select) to the bottom large text field and select Vertical Spacing.

![step 14](/images/SCA UI/SCA UI S14.png){: .align-center}

### Step 15

Select both of the gray lines and set up the height, width, leading and trailing space. If your leading and trailing constraints say multiple it means that they are not both the same distance from their surrounding text fields, give the left line a nudge to the left or right with the arrow keypad on your keyboard and some blue alignment lines should pop up when you've got it right. Failing that, just do one at a time and let them be slightly different.

![step 15](/images/SCA UI/SCA UI S15.png){: .align-center}

### Step 16

Select the far left label and set the leading edge. Then select the far right label and set the trailing edge. Control drag from the labels to the text fields above them and select Center Horizontally and Vertical Spacing.

![step 16](/images/SCA UI/SCA UI S16.png){: .align-center}

### Step 17

Next control drag from the navigation bar to the left vertical gray bar and select Vertical Spacing. Then add the leading edge, trailing edge and height constraints as below.

![step 17](/images/SCA UI/SCA UI S17.png){: .align-center}

### Step 18

For the table view set the top, leading, trailing and bottom to 0.

![step 18](/images/SCA UI/SCA UI S18.png){: .align-center}

### Step 19

Now for the magic to make the table view expand to fill the rest of the screen and give the scroll view its content size. In the document outline control drag from the table view to the view controller's view and then select Vertical Spacing to Bottom Layout Guide. This will pin the table view to the bottom of the screen no matter the device size.

![step 19](/images/SCA UI/SCA UI S19.png){: .align-center}

### Step 20

There will still be a couple of yellow warnings to deal with, click them in the document outline and select "Update frames" - it will change the look of the storyboard by shrinking the table view and scroll view view but won't affect anything in the final layout.

![step 20](/images/SCA UI/SCA UI S20.png){: .align-center}

### Step 21

The final step is to stop the view controller being too clever and offsetting the content by the height of the top navigation controller. Create an outlet in the viewController and paste in:

{% highlight swift%}
self.automaticallyAdjustsScrollViewInsets = false
scrollView.contentInset = UIEdgeInsets(top: 0, left: 0, bottom: 0, right: 0)
scrollView.scrollIndicatorInsets = UIEdgeInsets(top: 0, left: 0, bottom: 0, right: 0)
{% endhighlight %}

Some final design to make it look nice wouldn't hurt but as you can see below this runs on all screen sizes from iPhone 4S to 6S and even up to iPad Pro (although we should be a bit more imaginative at that scale perhaps!)

![step 21](/images/SCA UI/SCA UI S21.png){: .align-center}

