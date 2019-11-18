# data_cleaning_tips
Repo for storing data cleaning tips, tricks, tools


## Excel

### Extract Data

##### Extract substring from start of a string (LEFT)
`=LEFT(text, [num_chars])`  
i.e. to get the first 4 characters from the beginning of a text string, use this formula:  
`=LEFT(A2,4)`  

##### Extract substring from start of a string (RIGHT)
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


### Pivot Tables
* Insert/PivotTable/OK
* Typically, add field(s) to Rows
* Add calculation field to Values & adjust calculation as needed
