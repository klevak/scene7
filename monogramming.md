

HIGH Level Estimate of

Skills Required

Adobe Image Server HTTP API
- http://crc.scene7.com/is-docs-4.0/
- http://crc.scene7.com/is-docs-4.0/pages/HTTP-Protocol-Reference.htm

Adobe Image Catalog
- http://crc.scene7.com/is-docs-4.0/pages/Image-Catalog-Reference.htm

Batch Job That Generates Catalog
- ecd189


ANCII Tables
- http://www.asciitable.com/
- 

Kerning
-- http://en.wikipedia.org/wiki/Kerning



Image URL Breakdown

```
http://cdni.llbean.com/is/image/?layer=0&size=1201,507&extend=50,50,50,50&bgc=255,255,255&fmt=png&resMode=sharp&layer=5&pos=-2150,-1400&anchor=500,500&src=is{wim/236564_39047_42?scl=0.4}&layer=10&pos=-600,-253&anchor=0,0&src=is{wim-mono/script_84?op_colorize=160,160,45}&layer=20&pos=-365,-253&anchor=0,0&src=is{wim-mono/script_105?op_colorize=160,160,45}&layer=30&pos=-270,-253&anchor=0,0&src=is{wim-mono/script_109?op_colorize=160,160,45}&layer=40&pos=25,-253&anchor=0,0&src=is{wim-mono/script_109?op_colorize=160,160,45}&layer=50&pos=315,-253&anchor=0,0&src=is{wim-mono/script_121?op_colorize=160,160,45}&wid=360&hei=140
```

```
http://cdni.llbean.com/is/image/?

-- The first layer denotes the background image
layer=0
&size=1201,507
&extend=50,50,50,50   - Adds margins to a layer or crops the layer rectangle.
&bgc=255,255,255
&fmt=png
&resMode=sharp 

-- Denotes the image used for the swatch
&layer=5
&pos=-2150,-1400 - Positive values move the layer towards the right/bottom, negative towards the left/top.
&anchor=500,500  - 
&src=is{wim/236564_39047_42?scl=0.4}





&layer=10
&pos=-600,-253
&anchor=0,0
&src=is{wim-mono/script_84?op_colorize=160,160,45}
-- http://cdni.llbean.com/is/image/wim-mono/athletic_75?op_colorize=160,160,45 
-- http://cdni.llbean.com/is/image/wim-mono/script_84?req=userdata&id=script_84
s7data({'coords':'391,507,8713,54,0,143'},'script_84')

&layer=20
&pos=-365,-253
&anchor=0,0
&src=is{wim-mono/script_105?op_colorize=160,160,45}

&layer=30
&pos=-270,-253
&anchor=0,0
&src=is{wim-mono/script_109?op_colorize=160,160,45}

&layer=40
&pos=25,-253
&anchor=0,0
&src=is{wim-mono/script_109?op_colorize=160,160,45}

&layer=50
&pos=315,-253
&anchor=0,0
&src=is{wim-mono/script_121?op_colorize=160,160,45}


&wid=360
&hei=140
```


System Impacts  (Effort / Complexity)

 - WIM Swing/Java/JSP Application (To Expose New "Monogramming" Image Type)
    - Database Impacts - (High / High)
        - Configuration data (meta data that drives the image type)  - (Low / Med)
            - Assumption is that this will be a prereq to Ongoing updates
            
        - Prepopulate  (only for pages that have monogramming)  (Very High / High)
            - Insert new values in Tables to create new "monogramming" image types  (SQL Script or Program)
            - Using Data sourced from current swatches
            - Risk
               - Keys
               - Logic to select pages that are affected (will come from a static list)
               - Determine what tables to populate
               - Test
               - Planning
            
        - Ongoing  (Assume that the image type status is disabled)  Low / Med (esp. if disabled)
            - Modifications to WIM Image Import to create new image type when needed


    - Possible Java impacts for adding new image type ?? (Assumption is no)
    
    - NEW Image Type
        - Related to the Composite purpose  (Product Page)
    
    - Image Preview  (Med / Med)
        - Previewing new "Monogramming" Image Type
        - JSP (Page that displays html for preview) To add the new image on the page
        - Java (class that generates the url) would not be impacted as only coord data is updated
           - Assumes little or no Java updates
 

 - WIM Batch  
    - Image Import  (Low / High) ** Unknowns / Lots of testing
      - Creates new image type data in WIM database.  
       * This is impacted by the new relationship between the "monogramming" image type and the product page composite purpose
         - Uses data inside of the image manifest
         - Creates or Update
             - Composite
             - Image Types
             - Layers
             - etc.


  - Image Catalog Generation (PERL)  (Low / Med) ** Unknowns / Lots of testing
    - Generates URLs based on data from WIM tables
    - Geletes and inserts records in catgroup_image table
    - Creates wim.txt files
      



Definition of 'Done'

 - New entry in the image catalog to represent "Monogramming" image type (e.g. 236564_39047_XX)
    -  http://cdni.llbean.com/is/image/?layer=0&size=1201,507&extend=50,50,50,50&bgc=255,255,255&fmt=png&resMode=sharp&layer=5&pos=-2150,-1500&anchor=500,500&src=is{wim/236564_39047_42?scl=0.4}&wid=360&hei=140

 - WIM Application
    - WIM UI Shows the Monogramming image type
        - User is able to edit the values for pos, anchor, scale (at the image type level)
        - User is able to edit the values for pos, anchor, scale (at the image type level / color level)
        
    - WIM Preview displays the image type

