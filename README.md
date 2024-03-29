# excel_data_cleaning_tips
Repo for storing data cleaning tips, tricks, tools


## Excel

### Extract Data

##### Extract substring from start of a string (LEFT)
`=LEFT(text, [num_chars])`  
i.e. to get the first 4 characters from the beginning of a text string, use this formula:  
`=LEFT(A2,4)`  

##### Extract substring from end of a string (RIGHT)
`=RIGHT(text, [num_chars])`  
i.e. to get the last 4 characters from the end of a string, use this formula:  
`=RIGHT(A2,4)`  

##### Extract text from middle of string (MID)
`=MID(text, start_num, num_chars)`  
i.e. to get three characters from the middle of a string beginning with the 6th character, you use the following formula:  
`=MID(A2,6,3)`  

#### Extract text after a word  
This is hacky  
`=MID(A1,FIND("DISTRICT ",A1)+9,99)` 
Where we are trying to extract everything after the word "district." +9 is the number of characters in the word we're looking for and 99 will pull out 99 characters after that word.  

##### Extract text after a specific character
`=LEFT(A2, SEARCH("-",A2)-1)`  
i.e.   
`=RIGHT(A6,LEN(A6)-SEARCH(" ",A6))`  

##### Extract text between two instances of a character
`MID(cell, SEARCH("char", cell)+1, SEARCH ("char", cell, SEARCH ("char", cell)+1) - SEARCH ("char", cell)-1)`  
i.e. to extract text surrounded by two hyphens (EC1-1BB2-AC12), you'd use this formula:  
`=MID(A2, SEARCH("-",A2) + 1, SEARCH("-",A2,SEARCH("-",A2)+1) - SEARCH("-",A2) - 1)`

#### Extract text up to particular text
`=LEFT(K3,SEARCH(",",K3)-1)`
This looks at this cell: `P.O. BOX 76655, 20013` and brings over all of the text up until one character before it sees the comma!

#### Extract number of varying length from left of string  
First, find where to start the extraction by determining the position of the first digit with this generic formula:  
`MIN(SEARCH({0,1,2,3,4,5,6,7,8,9},cell&"0123456789"))`  
Then, use the RIGHT function to extract the number.  
`=RIGHT(A2, LEN(A2)-B2+1)`  
(Where B2 is the position of the first digit.)

#### Extract text before first occurance of a number  
`=LEFT(A1,MIN(FIND({0,1,2,3,4,5,6,7,8,9},A1&"0123456789"))-1)`  

#### Extract all but the last word in a cell (last names)
`=LEFT(C8,FIND("*",SUBSTITUTE(C8," ","*",LEN(C8)-LEN(SUBSTITUTE(C8," ",""))))-1)`  

#### Extract the last word in a cell (all but first name)  
`=RIGHT(C2,LEN(C2)-FIND("*",SUBSTITUTE(C2," ","*",LEN(C2)-LEN(SUBSTITUTE(C2," ","")))))`  


### Check if a string is in a cell  
`=ISNUMBER(SEARCH("apple",A1))`  
This would search for the word "apple" in cell A1.  


### Check if a string is duplicated in a column  
`=COUNTIF(J:J,J2)>1`  
This would look through all of column J for repeat instances of string in J2. All duplicated cells will be marked TRUE.  


### Check if a string is duplicated in a column without first occurance being labled  
`=IF(COUNTIF($J$2:$J2,J2)>1,"DUP","")`  
This would look through all of column J for repeat instances of string in J2. The first instance of a duplicated string will be blank, but all subsequent inastanced will be marked "DUP".  


### If statements based on conditions (OR, AND)  
Check if a cell has "this" or "that," then take a particular action. If the cells do not, then do something else.  
`=IF(OR(B2=D2,B2>100)B2*D2,FALSE)`  
This checks if B2 and D2 are equal, or if B2 is greater than 100. If either of these are true, then the cell will calculate B2xD2, if not it will return false. *(I have not tested this example.)*  

`=IF(AND(B2=D2,B2>100)B2*D2,FALSE)`  
For this example, both conditions would need to be true in order to multiply B2 and D2, otherwise it will return FALSE.  


### Concatenate
`=C2&" "&C3' 
This combines the string from C2 and C3 together with a space between.  

#### Concat with added character  
`=CONCATENATE(A1, ", ", B1)`  
or  
`=A1 & ", " & B1`

#### Concatenate text cell with numeric cell that has leading zeros
`=B2&TEXT(C2,REPT("0",3))`  
In this sample B2 has text and C2 has 3 numbers with leading zeros. the "3" indicates how many of the "0" to add.  

### Check if values in two cells are the same  
`=EXACT(T2,E2)`  

### Pivot Tables
* Insert/PivotTable/OK
* Typically, add field(s) to Rows
* Add calculation field to Values & adjust calculation as needed

* Add a unique count to a pivot table:  
When inserting pivot, click tick box "add this data to the Data Model" and this will add "distinct count" to your Value Field Settings for the variable you are counting.


### Convert Multiple Rows to Columns and Rows
> A1: Smith, John  
> A2: 111 Pine St.  
> A3: San Diego, CA  
> A4: (555) 128-549  
> A5: Jones, Sue  
> A6: 222 Oak Ln.  
> A7: New York, NY  
> A8: (555) 238-1845  
> A9: Anderson, Tom  
> A10: 333 Cherry Ave.  
> A11: Chicago, IL  
> A12: (555) 581-4914  

In cell C1, type:  
`=OFFSET($A$1,(ROW()-1)*4+INT((COLUMN()-3)),MOD(COLUMN()-3,1))` 
then fill down to row 3.  

[Additional info](https://support.office.com/en-us/article/how-to-convert-multiple-rows-and-columns-to-columns-and-rows-in-excel-09c017ec-a151-41b0-9caf-60b01f9a4deb).


### Dates
#### Extract month and year:
In empty column:
`=TEXT(B1,"yyyymm")` or
`=TEXT(B1,"mm/yyyy")`, etc.
#### Extract numeric month to written month:
`=TEXT(B1,"mmm")`


### VLookups
#### Search for a given value from a column range: 
`=VLOOKUP(B1,E2:E100,1,FALSE)`  
In this sample, B1 refers to the cell with the value we're trying to match. E2:E100 is the range of values we're looking in to find the matching value (this can also span multiple columns - E2:G50 - or sheets - Sheet2!B2:B50. The number 1 refers to the 1st column and FALSE tells it we're looking for an exact match, where TRUE would tell it that it has to be a close match. 


### MAXIFS
#### Find the max value within defined groups of data
`=MAXIFS($T$2:$T$29648,$R$2:$R$29648,R2)`  
In this sample, T2:T29648 (max_range) refers to the range of cells where you want to find the max values in. R2:R29648 (criteria_range) is the range within you want to identify your sub-groups (i.e.: it will group together cells/rows where this value is the same). R2 (criteria) is the criteria I will be using to find all other matching uses within the criteria_range. You can use multiple criteria_range/criteria cases to the one formula. This was used for finding the highest vote count for each Race_ID.  
You can add multiple criteria too  
`=MAXIFS($E$2:$E$29659,$D$2:$D$29659,D2,$S$2:$S$29659,S2)`  
This essentially would group matching items first in column D and then group matching items in column S.  


### Searches
#### Search a cell to see if it contains a string, then return the contents of that cell:  
`=IF(ISNUMBER(SEARCH("District",E2)),E2,"No")`  
In this sample, E2 is the cell we're searching in for the string "District." Not an exact match; E2 can contain other letters/numbers.


### Hacking Medians in Pivot Tables
#### To get medians into a pivot table  
`{=MEDIAN(IF($B$2:$B$31=B2,$C$2:$C$31))}`  
To get curly brackets, press Ctrl + Shift + Enter at end of formula. This tells Excel that this is an array. This is key.  
This forumal is saying look in the range B2 - B31 and if you find a match to B2 then use the corresponding cell in C2 - C31.  
Then, in your pivot table add your median column and change the value field settings to Average.  


### Copying
#### Pasting a list into Excel  
Hold CTRL down when highlighting what you want to paste. Then, when you paste - it should put each item in the list in its own cell.  


### Non-Excel hacks  
#### Copy files names from inside a folder to paste into Excel, etc. (Windows!)  
Open command prompt and file explorer.  
cd into correct file location.  
Type:  
`dir /b > filenames.txt`  
txt file with all file names with be located in the folder.  


