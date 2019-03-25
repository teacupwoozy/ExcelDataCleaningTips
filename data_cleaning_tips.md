# Collections of Data Cleaning Tips

 A (likely) haphazard complilation of data cleaning tips, tricks, tools

## The Big Picture
type( ): id the type of data the object is.     
dir( ): identify methods a particular data type can do.
help( ): returns documentation for the object or method.  
df.sample(n = 5): provides a random sample of df  
Regex Cheatsheet: https://www.rexegg.com/regex-quickstart.html  

## iPython Magic
%run: 
%store: pass variables between two different notebooks. -r: Refresh all variables from store (overwrite current vals).  
%run: execute python code from .py files - this is well-documented behavior. Lesser known is the fact that it can also execute other jupyter notebooks, which can quite useful.  

## On Import
Do not assume a numeric field contains only numbers. A NaN or null can become a 0.

## Removals
.notnull( ): is not NaN.

## Locating/Finding/Matching
df.isin(['cat', 'dog', 'mouse']): determines if each element in the df is contained in the listed values.
enumerate( ): loop over something and have a counter for it. i.e.: keep a count of iterations.  
isdigit( ): Return true if all characters in the string are digits and there is at least one character, false otherwise.  
isalpha( ): Return true if all characters in the string are alphabetic and there is at least one character, false otherwise.  

## Transforming
.from_dict: create df out of a dictionary.

## Numbers, Time, etc.
datetime.strptime( ): Convert a string to datetime. Parse according to format.  
strftime( ): returns a string from date and time.  
Key datetime formats: https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior  

## matplotlib
.xlim( ): Get or set the x limits of the current axes.