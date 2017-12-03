
--------------------------------------------
The following pertains only to the tokohp application.
--------------------------------------------


See detailed instructions on formatting the input file at: ericag13.github.io/tokohp.html


-----------------------------
-- Software Specifications --
-----------------------------

Purpose:
   The virtual pet known as a Tokota has a number attached to it called HP. HP is accumulated through certain player activities, and those activities must be kept track of in a neatly formatted document, called an HP Journal. This journal allows both the game's players and administrators to keep accurate records on each Tokota in existence.
   However, writing these journals, updating them, and formatting them consistently is time consuming, especially as a player accumulates more pets to make journals for.
   This application addresses the issue by allowing players to store the information necessary to a journal in a compact format and have the application construct a pre-formatted HP journal at the press of a button.

Operating Environment:
   This small application is available as a website in order to be easily accessible to most users. Currently, it is written in HTML and Javascript.

Product Functions:
   Given a spreadsheet in file format .csv with the information within arranged according to the user documentation, the application reads and organizes information for each HP Activity and each individual Tokota.
   Given an individual Tokota's name and a few boolean flags to specify formatting, the application performs a counting operation on the HP Activities associated with the Tokota and then outputs a string of text that contains the information necessary for an HP Journal, formatted via HTML so that it will be easily readable once added to the website the game takes place on.

Function 1: File Parsing
   This function is performed automatically when the user inputs a file.
   The first row of the input document is assumed to contain headers and ignored.
   After that, the file is interpreted line by line. Each line is expected to represent one image known as an HP Activity. Each line is expected to contain, in order: A thumb-code used to link back to and display the image, A string describing the calculation of the HP total for this Activity, the total HP this Activity is worth, a string describing the Activity (ex Hunting, Fishing). Then, the rest of the line is expected to be the names of individual Tokotas, which participated in the Activity. The application interprets lines until it reaches an empty line, which it assumes is the end of the file.
   This information is stored via two types of objects; a Thumbnail and a Tokota. Each Thumbnail contains the thumb code, HP calculation, HP total, and description for that Activity. Each Tokota contains a name and a list of the Thumbnails it appears in.

Function 2: Totalling the HP for a Tokota
   The process for counting the totals needed to output a Tokota's journal is contained by a method within the Tokota class itself.
   As specified by the client, a tokota has a grand total and a minimum of 2 subtotals to consider. The grand total is self-explanatory; it is the sum of the HP values of all the Thumbnails the Tokota object contains. The subtotals are more complex.
   Each Tokota has a variety of tiers it can be in, depending on how much HP it has accumulated. These tiers are 'Submissive to Average', 'Average to Dominant', 'Dominant to Alpha', and from that point on there may be any number of 'Extra' tiers. These tiers will be referred to as Sub, Avg, Dom, and Extra from now on. The counting process counts for each of those tiers in the order they have just been listed.
   The general process for counting a tier is to go through the list of Thumbnails, adding each Thumbnail to the tier's list and adding each Thumbnail's HP value to the tier's total, until the tier's total reaches or exceeds a specific number. Once the maximum is reached, the total is checked for overflow. If the total exceeds the maximum, the total is reduced to the maximum and the overflow is premptively added to the total for the next tier.
   The process repeats for each tier until the end of the list of Thumbnails is reached.
   Which tiers are used depends on user input. In particular, the user specifies via a checkbox if the Sub tier is to be used; if left unchecked, the first tier is Avg instead. Theoretically, there can be as many Extra tiers as there are postive integer values, provided there are enough Thumbnails to warrant having that many tiers.

Function 3: Outputting the HP Journal for a Tokota
   This creates the output the user is looking for; the string that creates a formatted HP Journal for use in the game.
   The first part of the output is the grand total of HP for a tokota. After that are the tiers, in order of Sub, Avg, Dom, and then any Extra tiers. Only tiers that have nonzero totals are included in the output.
   The general format of each tier is the tier's name, the tier's total, a note of the previous tier's overflow value if there was any, and then a list of the Thumbnails included in the tier.
   The general format of the Thumbnail list is that each thumbnail is displayed as an image/link followed by it's HP value and HP calculation. The specific format of the list depends somewhat on user input. If the user checks the box for blockquotes, each Thumbnail's information is contained in <blockquote> tags, and if the box is left unchecked each Thumbnail is simply centered. If the user chooses via checkbox, the tier may be divided by the description of each Thumbnail; ie, it will have subheaders and subtotals for each possible description.

User Interfaces
   The only interface the application requires is a filepicker, three checkboxes, a button, and a text area. The three checkboxes determine three things; whether to use the Sub tier, whether to use blockquote formatting, and whether to use activity-description subheaders. The text area is where the output appears.
   The look and feel of these components may be altered using HTML and CSS as desired; so long as the necessary element id's in the HTML file exist, the Javascript will run properly. Other content can exist on the same page, so long as there is no conflict of element id's.
   
   
   
   
   
   
   
   
   