# data_cleaning_tips
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


### Check if a string is in a cell  
`=ISNUMBER(SEARCH("apple",A1))`  
This would search for the word "apple" in cell A1.  

### Concatenate
`=C2&" "&C3' 
This combines the string from C2 and C3 together with a space between.

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




