# Buddi currency converter

This simple PHP script was created to convert Buddi ( http://buddi.digitalcave.ca/ ) data XML from one currency to another. Buddi internally does not allow to specify
relations between different currencies. And if you ever need to convert from one to another (for example if you move to different country
and need to switch from USD to EUR) there is no easy way to handle this. To use this script you first need to export Buddi data XML,
run script on it by specifying path to data file and your rate for conversion.

**WARNING:** Always make backups.

**WARNING:** There is no guarantee that this script converts things properly.

**WARNING:** Script does not evaluate real structure of XML file, but simply converts all float/long fields. At the time of writing it worked
properly, however this is **WRONG** way to do things. Only correct nodes should be converted. Plus this approach makes conversion slow.
In my case it took ~35 seconds for 7.5MB big XML file (~ 7500 transactions).

**WARNING:** Keep in mind that conversion might not be 100% accurate because of rounding. Conversion will happen on every transaction and
as a result totals will differ a bit.

**Usage:** ```php buddi.php -f ~/path_to_buddi.xml -r 0.702804```

This will take XML file in specified path and will apply rate 0.702804 to all stored float's/long's.
Example is for conversion I had to do when changed base currency Lat's to Euro ( 0.702804 LVL == 1 EUR ).
If everything will work fine, then in the same directory where you had your Buddi XML file, you should see 'converted_buddi.xml'.

If you do not have Buddi XML file you can get it by extracting. This can be done with command like this:
```$ java -jar ~/Buddi-3.4.1.6.jar  --extract ~/Buddi/buddi.buddi3```
In --extract you should pass path to your Buddi data file. After extraction in the same directory where data file is located
you should see newly created Buddi XML. If it is not there, try to use different Buddi JAR file. At the time of writing, most recent
version (3.4.1.11) was not able to extract XML, but 3.4.1.6 was.

To import converted XML file back into Buddi use:
```$ java -jar ~/Buddi-3.4.1.11.jar --import ~/Buddi/converted_buddi.xml```

**NOTE:** import flag was added only in version 3.4.1.11

This projected is licensed under the terms of the MIT license.

Copyright (c) Endijs Lisovskis 2013 <endijs@lisovskis.com>