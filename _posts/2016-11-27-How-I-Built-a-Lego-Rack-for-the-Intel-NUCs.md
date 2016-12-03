---
title: How I built a Lego Rack for the Intel NUCs
excerpt: "Building a Lego Rack for the Intel NUCs, including a working front door. Lots of sweat, tears and last minute purchases from eBay..."
header:
   teaser: "kitchen_teaser.png"
category: [Homelab] 
tags: [Homelab, Education, Virtualisation, Lego, NUC, Rack, Server]
---  

{% include toc %} 
  
I wrote about my new mini lab in this [post](/homelab/The-Mini-Lab/) recently, where I mentioned the fact that I had built a rack out of legos for my Intel NUCs. I had also posted a few pics of my set-up on Twitter and Reddit and I got quite a few requests to write a set of detailed build instructions for the Lego <del>House</del> Rack.  

**Note:** No musical sensibilities were harmed during the writing of this blog post. Ed Sheeran's Lego House was not played even once... :wink:  

## The story 

There are some quite nice looking Lego based racks around the Web. For example, the awesome [Lego VSAN EVO Rack](http://vmnick0.me/?p=7) by Nicholas Farmer, or the also brilliant [Fun with Legos and Intel NUCs](https://roguevcdx.com/2016/06/10/fun-with-legos-and-intel-nucs/) by Andy Smith. Problem is, nobody is writing any guides on how to build the little beasties...

For my build, I wanted to mix (I mean, steal) the best aspects of both Nicholas' and Andy's designs. I started by examining their pictures and then came up with a design, initially sketched on paper, so that I could have a basic idea of the number of bricks required. The overhang column seen on my design was inspired by the case design of the Power Macintosh 8600/9600 with the side compartment for the motherboard:  

![Power Macintosh 9600](/images/rack/power-mac-9600.jpg){: .align-center}  

But, I must confess that it was a lot of trial and error and that I didn't keep the best of notes as I was building the rack. For this guide, in the spirit of helping the community, I sucked it up and dismantled the rack to document the build again...

## Pick a Brick  

It turned out to be very difficult to source the Lego bricks I needed for this build. I initially thought about a blue and black build (like the EVO), but blue bricks were very hard to come by. I suspect my friends in the US of A will have better luck...

Even the black stackable base plates are now hard to find in the UK (other colours available). They are available directly from [Strictly Briks](http://strictlybriks.com/stackable-baseplates/6-x-6-single-color-stackables.html), though. 

## Bill of Materials (BOM)  

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|1 (pack of 10)|Stackable Plates|Black|20x20 (6" x 6")|
|2|Brick|Black|1x16|
|4|Brick|Black|1x8|
|64|Brick|Grey|2x6|
|48|Brick|Black|2x6|
|14|Brick|Grey|2x4|
|8|Brick|Black|2x4|
|2|Brick|Black|1x4|
|8|Brick|Grey|2x2|
|24|Brick|Black|2x2|
|18|Brick|Grey|1x4|
|2|Brick|Grey|1x3|
|1|Brick|Grey|1x2|
|4|Corner Brick|Grey|1x2|
|4|Roof Tiles|Black|2x8/45˚|
|2|Roof Tiles|Black|2x4/45˚|
|8|Flat Tiles|Grey|1x8|
|2|Flat Tiles|Grey|1x6|
|4|Flat Tiles|Grey|1x4|
|2|Flat Tiles|Grey|1x2|
|9|Flat Tiles|Black|1x6|
|5|Flat Tiles|Black|1x4|
|4|Flat Tiles|Black|1x1|
|2|Arch Continuous Bow|Black|1x6|
|2|Plate|Grey|2x16|
|4|Plate|Grey|2x12|
|6|Plate|Grey|2x10|
|5|Plate|Grey|2x8|
|3|Plate|Grey|2x6|
|2|Plate|Grey|2x4|
|2|Plate|Grey|1x2|
|2|Angle Plate|Grey|1x2/2x2|
|4|Hinge Plate Locking Dual Finger on End|Black|1x2|
|4|Hinge Plate Locking Single Finger on Top|Grey|1x2|  

Other than the bricks and plates above, I also used the following items to complete the rack door:

* [Midwest Polyester Clear Sheet 0.06 mm Single](http://www.hobbycraft.co.uk/midwest-polyester-clear-sheet-006-mm-single/569117-1000)
* [Stix2 Self-Adhesive Magnetic Tape](http://www.hobbycraft.co.uk/stix2-self_adhesive-magnetic-tape-3-metres/606215-1000?queryFromSuggest=true&userInput=magnetic%20tape)
* [Modelcraft Universal Razor Saw](http://www.hobbycraft.co.uk/modelcraft-universal-razor-saw/569370-1000?queryFromSuggest=true&userInput=craft%20saw)

## The Build in Pictures (and words)   

I spent a considerable amount of time thinking about what size rack I wanted to build. I had seen the Strictly Briks' Stackable Base Plates before and noticed that Andy had used them for his own rack, so it was just a question of selecting a size that was enough to accommodate the NUCs. 

I decided to go with the smallest of the bases, which are available in sizes of 20x20 (brick dots), 22x26, 32x32 and even 50x50 (from other vendors); the larger plates just seemed too big for the look and proportions I wanted to achieve. However, the first build looked a bit boring, so I ended up having to come up with a way of extending the plates somehow, which then allowed me to incorporate the side overhang to my design.  

### Ground Floor  

The basic building blocks are the Strictly Briks Stackable Plates and the hollow building bricks that come with them. When two of these bricks are joined together, they form a nice 2x2x5 smooth column.

BOM for this section:

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|2 |Plates|Black|20x20|
|16|Stackable/Column Brick|Black|1x16|
|8 |Brick|Grey|2x6|
|10|Brick|Grey|2x4|
|8|Brick|Black|2x6|  


<u>Step 1</u>  

Sandwich together two of the base plates and add four building blocks to each corner to form a 4x2x5 column.

[ ![](/images/rack/base_and_column_sm.png) ](/images/rack/base_and_column_lg.png) [ ![](/images/rack/column_brick_sm.png) ](/images/rack/column_brick_lg.png)


<u>Step 2</u>

Two sides of the base plate will have a narrower gap: stick four 6x2 grey bricks (two over two) to complete the lower side wall.

[ ![](/images/rack/base_lower_wall_sm.png) ](/images/rack/base_lower_wall_lg.png)  

<u>Step 3</u>

Build the front and back "partition" walls by stacking five 4x2 grey brick right in the middle of the opening: 

[ ![](/images/rack/base_front_back_sm.png) ](/images/rack/base_front_back_lg.png)


<u>Step 4</u>

It is now time to put together the second pair of plates, which will enclose the base and serve as the 1st level "floor". As I decided to have a kind of overhang on one side of the rack, two plates will be placed on top of each other, but this time the top one will be offset by four "dots".  

[ ![](/images/rack/overhang_sm.png) ](/images/rack/overhang_lg.png) 

<u>Step 5</u>

We are left with a "step-down" at one end of both the top and bottom of the combined plate, which will need to be filled up with two 4x8 and one 4x4 plates on each side. 

[ ![](/images/rack/overhang_fill_sm.png) ](/images/rack/overhang_fill_lg.png)  

Once done, the base plates for the 1st, and subsequent floors, will have an overall size of 24 dots (w) by 20 dots (d).  

[ ![](/images/rack/overhang_final_sm.png) ](/images/rack/overhang_final_lg.png)  

<u>Step 6</u>

Turn the baseplate upside down and add to the middle of the short edges four 2x6 black bricks (two over two); on one side, right on the edge, and on the other offset by four dots. Those will form the upper half of the side wall of the base, including a gap in the middle.

[ ![](/images/rack/base_upper_wall_sm.png) ](/images/rack/base_upper_wall_lg.png)
  

Finally, place the assembled 1st level plate over the base.

[ ![](/images/rack/base_complete_sm.png) ](/images/rack/base_complete_lg.png) [ ![](/images/rack/base_side_sm.png) ](/images/rack/base_side_lg.png) 


### First Floor 

BOM for this section:

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|2|Plates|Black|20x20|
|4|Plates|Black|4x8|
|2|Plates|Black|4x4|
|4|Stackable/Column Brick|Black|1x16|
|24|Brick|Grey|2x6|
|2|Brick|Grey|2x4|
|6|Brick|Grey|2x2|
|8|Brick|Black|2x6|
|2|Brick|Black|2x2|
 

<u>Step 7</u> 

The first floor build starts by adding the side walls to the base plate (floor). Place three 2x6 grey bricks along the overhang edge (offset by four dots) and finish off with a 2x4 brick running lengthwise along the bottom edge of the plate.

[ ![](/images/rack/1st_row1_sm.png) ](/images/rack/1st_row1_lg.png)

Start the second row with a 2x2 grey brick, followed by three 2x6 grey bricks.

[ ![](/images/rack/1st_row2_sm.png) ](/images/rack/1st_row2_lg.png)

Rows 3 and 4 are built with 2x6 black bricks only, leaving a gap in the middle; rows 5 and 6 are built with 2x2 and 2x6 black bricks -- I started with the 2x2 bricks at different ends of the plate.

[ ![](/images/rack/1st_row3_6_sm.png) ](/images/rack/1st_row3_6_lg.png)

[ ![](/images/rack/1st_final_sm.png) ](/images/rack/1st_final_lg.png)

Finally, place 2 building bricks together at each end of the overhang, capped by a 2x2 black brick. This will give extra height to the column, matching the six row wall.

[ ![](/images/rack/column_sm.png) ](/images/rack/column_lg.png) [ ![](/images/rack/1st_column_sm.png) ](/images/rack/1st_column_lg.png)

### Second Floor  

BOM for this section:

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|2|Plates|Black|20x20|
|4|Plates|Black|4x8|
|2|Plates|Black|4x4|
|4|Stackable/Column Brick|Black|1x16|
|24|Brick|Black|2x6|
|2|Brick|Black|2x4|
|6|Brick|Black|2x2|
|8|Brick|Grey|2x6|
|2|Brick|Grey|2x2|

<u>Step 8</u>  

Build the base plate (floor) as per steps 4 and 5.

<u>Step 9</u>

As per Step 7, but starting with black, instead of grey, bricks.

[ ![](/images/rack/2nd_floor_walls_sm.png) ](/images/rack/2nd_floor_walls_lg.png) 

### Third Floor

BOM for this section:

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|2|Plates|Black|20x20|
|4|Plates|Black|4x8|
|2|Plates|Black|4x4|
|4|Stackable/Column Brick|Black|1x16|
|24|Brick|Grey|2x6|
|2|Brick|Grey|2x4|
|6|Brick|Grey|2x2|
|8|Brick|Black|2x6|
|2|Brick|Black|2x2|  

A repeat of steps 4, 5 and 7 (grey bricks).  

### Roof 

BOM for this section: 

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|2|Plates|Black|20x20|
|4|Roof Tiles|Black|2x8/45˚|
|2|Roof Tiles	|Black|2x4/45˚
|8|Flat Tiles	|Grey|1x8|
|4|Flat Tiles	|Grey|1x4|

The top of the rack (roof, if you will) is built with the same overhang base plates, then finished off by 2x8/45˚ and 2x4/45˚ black roof tiles, and capped by two 1x8 and one 1x4 grey smooth plates to the sides. The front and back of the roof are finished off with one 1x16 and one 1x4 black bricks capped by two 1x6 and one 1x8 grey smooth plates.

[ ![](/images/rack/roof_front_sm.png) ](/images/rack/roof_front_lg.png) [ ![](/images/rack/roof_side_sm.png) ](/images/rack/roof_side_lg.png)

[ ![](/images/rack/roof_final_sm.png) ](/images/rack/roof_final_lg.png)  

### The Work so Far  

We now have a rack that will suit most people.

[ ![](/images/rack/rack_no_door_sm.png) ](/images/rack/rack_no_door_lg.png)  

I myself wanted the rack to have a working door. Off course, it is not essential, but I just enjoyed the challenge... :wink: 

### The Door  

BOM for this section: 

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|4|Corner Brick|Grey|1x2|
|18|Brick|Grey|1x4|
|2|Brick|Grey|1x3|
|1|Brick|Grey|1x2|
|2|Plate|Grey|2x16|
|4|Plate|Grey|2x12|
|6|Plate|Grey|2x10|
|5|Plate|Grey|2x8|
|3|Plate|Grey|2x6|
|2|Plate|Grey|2x4|
|2|Plate|Grey|1x2|
|2|Angle Plate|Grey|1x2/2x2|
|4|Hinge Plate Locking Dual Finger on End|Black|1x2|
|4|Hinge Plate Locking Single Finger on Top|Grey|1x2|  

Designing and building the door frame was reasonably easy, but the hinges (ah the hinges) proved to be a much tougher nut to crack. There are plenty of different, nice looking hinges out there and I tested most of them. Some come fully assembled, some are hard to put together, but all proved to be either too weak to support the door or just impossible to attach to the frame. The one thing I didn't want was to glue any parts together...

I had to come up with a custom design, and it proved to be not only strong enough to hold the door, but also pretty reliable in operation. The hinges are built by using four Hinge Plate Locking Dual Finger on End (black), four Hinge Plate Locking Single Finger on Top (grey) and two 1x2/2x2 grey Angle Plates.

[ ![](/images/rack/hinge_pieces_sm.png) ](/images/rack/hinge_pieces_lg.png)

Well, lets get on with the program... 

<u>Step 10</u>  

The basic shape for the door frame is built by arranging two 2x16 grey plates (width) and four 2x12 grey plates (height).

[ ![](/images/rack/door_frame_sm.png) ](/images/rack/door_frame_lg.png)

<u>Step 11</u> 

On the hinge side, start joining the base plate with one 2x4 grey plate offset by two dots; leave another two dots free and add one 2x6 grey plate. Finally, skip another two dots and add a second 2x4 grey plate.  

[ ![](/images/rack/door_frame_hinge_side_sm.png) ](/images/rack/door_frame_hinge_side_lg.png) 

<u>Step 12</u> 

Place two black hinge plates (with the two "fingers") on each gap between the 2x4 and 2x6 plates, and  connected to the grey hinge plates ("single finger on top"); the hinges are finished off by two 1x2 black smooth plates. Finally, attach the angle plates.

[ ![](/images/rack/hinge_connected_sm.png) ](/images/rack/hinge_connected_lg.png) [ ![](/images/rack/hinge_capped_sm.png) ](/images/rack/hinge_capped_lg.png) [ ![](/images/rack/hinge_angle_plate_sm.png) ](/images/rack/hinge_angle_plate_lg.png)

[ ![](/images/rack/door_frame_and_hinge_sm.png) ](/images/rack/door_frame_and_hinge_lg.png)

{: .notice--info}
I couldn't find a mounting position for the hinges that would line up correctly with the distance between two overhangs. The top hinge needs to be "packed" with one 1x4 grey brick and two 1x2 grey plates to compensate for this.

[ ![](/images/rack/hinge_packers_sm.png) ](/images/rack/hinge_packers_lg.png) [ ![](/images/rack/hinge_top_detail_sm.png) ](/images/rack/hinge_top_detail_lg.png)


<u>Step 13</u> 

On the handle side, the base plates are simply joined by three 2x6 plates offset by two dots either side.

[ ![](/images/rack/door_frame_handle_side_sm.png) ](/images/rack/door_frame_handle_side_lg.png) 

<u>Step 14</u>

The top and bottom base plates are fixed by adding two 2x10 grey plates, starting from the free 2x2 space on each of the side plates.

[ ![](/images/rack/door_frame_top_bottom_sm.png) ](/images/rack/door_frame_top_bottom_lg.png)  

The complete door base frame:

[ ![](/images/rack/door_frame_final_sm.png) ](/images/rack/door_frame_final_lg.png)

<u>Step 15</u>

Starting with the 1x2 corner bricks, add grey 1x4 bricks around the outer perimeter of the base frame. 

[ ![](/images/rack/door_frame_edge_sm.png) ](/images/rack/door_frame_edge_lg.png) [ ![](/images/rack/door_frame_edge_2_sm.png) ](/images/rack/door_frame_edge_2_lg.png)  

Note that on the handle side, an extra two 1x3 (or one 1x6) grey bricks are set in the middle of the lower perimeter; those bricks form the basis where the door handle itself will sit.

[ ![](/images/rack/door_frame_edge_handle_sm.png) ](/images/rack/door_frame_edge_handle_lg.png)  

<u>Step 16</u>  

To finish off the inner frame, place 1x8 grey smooth plates around the inner perimeter. Note that on the hinge side, one 1x6 grey smooth plate is placed between the two 1x8 plates.

[ ![](/images/rack/door_frame_inner_sm.png) ](/images/rack/door_frame_inner_lg.png)  

### The Glass  

BOM for this section: 

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|1|Midwest Polyester Clear Sheet Single|Clear|0.06 mm|
|1|Stix2 Self-Adhesive Magnetic Tape|Brown|3 m|
|1|Modelcraft Universal Razor Saw|N/A|N/A|

**Note:** I used a razor saw, but I suppose a sharp pair of scissors would also do the trick.

<u>Step 17</u>

Measure and cut the polyester sheet to the desired size. In this case, the sheet was cut to a size of 144mm x 175mm, which fits snuggly within the inner edge of the door frame. On the handle side of the frame, a cut measuring 50mm x 10mm is also required in order for the glass to wrap around the door handle itself. The glass is then framed with the magnetic tape (both sides):

[ ![](/images/rack/door_glass_sm.png) ](/images/rack/door_glass_lg.png) [ ![](/images/rack/door_glass_cut_sm.png) ](/images/rack/door_glass_cut_lg.png)

<u>Step 18</u>

Carefully place the polyester sheet within the door frame. As mentioned above, the glass sits very snugly within the frame and might require some gentle persuasion when fit to the frame.

[ ![](/images/rack/door_with_glass_sm.png) ](/images/rack/door_with_glass_lg.png)

### Door Finish

BOM for this section: 

|<b>Quantity</b>|<b>Type</b>|<b>Colour</b>|<b>Size</b>|
|2|Arch Continuous Bow|Black|1x6|
|2|Flat Tiles|Grey|1x6|
|9|Flat Tiles|Black|1x6|
|5|Flat Tiles|Black|1x4|
|4|Flat Tiles|Black|1x1|

The handle is made up of two black arch continuous bows capped off by 1x6 grey tiles:

[ ![](/images/rack/door_handle_sm.png) ](/images/rack/door_handle_lg.png)

With the glass and handle in place, the only thing left is to cap the outer frame bricks with smooth black tiles. 

Starting with one 1x1 black smooth tile at the corners, add six 1x6 smooth black tiles to the top and bottom edges; three 1x6 and one 1x4 black smooth tiles to the hinge side and four 1x4 black smooth tiles to the handle side.

[ ![](/images/rack/door_finish_sm.png) ](/images/rack/door_finish_lg.png) [ ![](/images/rack/door_final_sm.png) ](/images/rack/door_final_lg.png)

### The NUCRac

Now, we simply attach the assembled door to the frame: the top hinge goes into the overhang of the second floor and the bottom hing into the overhang of the first floor. And that's it, the rack is complete:

[ ![](/images/rack/final_sm.png) ](/images/rack/final_lg.png) [ ![](/images/rack/rack_final_no_door_sm.png) ](/images/rack/rack_final_no_door_lg.png)

### What could be better?

Well, the top of the NUCs are very close to the "floor" above and it is very difficult to reach the power button. It is not much of a problem, because I don't expect to be powering the NUCs up and down on a regular basis. Besides, my NUCs all have vPro/AMT, so I can use the remote out-of-band features to power them up. :wink: 

As I was preparing this guide I thought about changing the height of the sections by an extra row of bricks, however, that would change the proportions of the door -- I just didn't feel like re-designing it all again...

### Parting Shot

Lastly, the wife (:ok_woman:) was so happy with the end product, she decided it could stay in the kitchen...

[ ![](/images/rack/kitchen_sm.png) ](/images/rack/kitchen_lg.png)



















