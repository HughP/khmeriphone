# International Components for Unicode #

## How to modify ICU library ##
<br>


Here are a few highlights of the services provided by ICU:<br>
<br>
Code Page Conversion: Convert text data to or from Unicode and nearly any other character set or encoding. ICU's conversion tables are based on charset data collected by IBM over the course of many decades, and is the most complete available anywhere.<br>
<br><br>
Collation: Compare strings according to the conventions and standards of a particular language, region or country. ICU's collation is based on the Unicode Collation Algorithm plus locale-specific comparison rules from the Common Locale Data Repository, a comprehensive source for this type of data.<br>
<br><br>
Formatting: Format numbers, dates, times and currency amounts according the conventions of a chosen locale. This includes translating month and day names into the selected language, choosing appropriate abbreviations, ordering fields correctly, etc. This data also comes from the Common Locale Data Repository.<br>
<br><br>
Time Calculations: Multiple types of calendars are provided beyond the traditional Gregorian calendar. A thorough set of timezone calculation APIs are provided.<br>
<br><br>
Unicode Support: ICU closely tracks the Unicode standard, providing easy access to all of the many Unicode character properties, Unicode Normalization, Case Folding and other fundamental operations as specified by the Unicode Standard.<br>
<br><br>

For more information, <b>ICU official Web Site :</b> <a href='http://site.icu-project.org/'>http://site.icu-project.org/</a>
<br><br><br>

This library is widely used in the iDevices, Macs, and many other devices... <br>

As of today the Khmer part is not yet properly fully defined. Few items are still missing.<br>
For example, if you switch the regional setting to khmer on your iPhone, then the "days" are not displayed properly. Number are displayed instead. This is due to missing definition in the ICU package, for the Khmer part.<br>
<br><br>
The following WIKI will explain how to modify the icuxxy.dat found in the iDevices.<br>
<br><br><br>
First download the ICU4C at <a href='http://site.icu-project.org/download'>http://site.icu-project.org/download</a>.<br>
This tool is needed to create, manipulate the icuxxy.dat library.<br>
<br><br>
Install the ICU4C on your computer. Follow the guide on the icu-project web site. <br>
I will consider that this installation is properly working.<br>
<br><br>

<h2>Summary steps example for iOS4:</h2>

Step 1 : Copy the icudt44l.dat from your iPhone to your computer.<br>
The icudt44l.dat is located on your iPhone in /usr/share/icu<br>
<br>
<br>

Step 2: Unpack the icudt44l.dat<br>
<br>
<br>

Step 3: Generate new xx.res file<br>
<br>
<br>

Step 4: Replace the old res.file by the new xx.res file<br>
<br>
<br>

Step 5: Repack the new icudt44l.dat<br>
<br>
<br>

Step 6: Rename/Replace the old icudt44l.dat by the new icudt44l.dat<br>
<br>
<br>


<h2>Commands Line Steps :</h2>
<br>
<h2>Step1: Copy the /usr/share/icu/icudt44l.dat from your iPhone to your Desktop.</h2>
Use WinSCP or CyberDuck or others to do this operation.<br>
<br>
<br>

<h2>Step 2: Unpack the icudt44l.dat</h2>

cd Desktop <br><br>
<b>./icupkg -tl -l icudt44l.dat > out.lst</b>
<br><br>
The above command will create the out.lst file. This .lst file will list all the files inside the xxx.dat<br>
<br>

Create a new directory named icudt44l  (example : mkdir icudt44l)<br>
<br>
Extract the package content :<br><br>
<b>./icupkg -tl -x out.lst icudt44l.dat -d icudt44l/</b>
<br><br>
The above command will extract all the files within the icudt44l.dat to the directory icudt44l. <br>
<br>
You can see that you have in this directory, some sub-directories and some aaaa.res file.<br>
The xxx.res file are the one that we will modify.<br>
For the khmer international unicode, we will modify the km.res file(s).<br>
if you want to know what is in this file, then simply browse to :<br>
<br><br><b><a href='http://source.icu-project.org/repos/icu/icu/tags/release-4-4/source/data/'>http://source.icu-project.org/repos/icu/icu/tags/release-4-4/source/data/</a></b> <br><br>
At the above address, you will find the text file version of the res file.<br>
<b>Please note that the address above is given for the 4.4 package. Each release has a different branch.</b><br>
<b>The file content differ from a version to another. Make sure to select the right version</b><br>

Select the <b>"Locales"</b> directory in the above web site.<br>
Download the file en.txt and the file km.txt <br>
<br>
You can open the both file, and see the differences. You will see that km.txt has missing field compare to the en.txt.<br>
<br>
<br>
<br>
<br>

<h2>Step 3: Generate new xx.res file</h2>
Modify the km.txt as you wish by respecting the format. <br>
Once the modification are done. We need to compile this text file to a res file. <br>
<br>

Goes to the directory where is located the km.txt file and then apply the following command. <br><br>
<b>genrb km.txt</b> <br><br>
This command will compile the km.txt to km.res<br>
<br>
<br>
<br>
<br>

<h2>Step 4: Replace the old res.file by the new xx.res file</h2>
Replace the /Desktop/icudt44l/km.res by the new one created. <br><br>
The yyy.res file directly under the /Desktop/icudt44l/ directory are the ones located in "Locales" on the ICU repo web site.<br>
The other yyy.res, follow the same directory naming as in the web site.<br>
<br>
<br>
<br>

<h2>Step 5: Repack the new icudt44l.dat</h2>
Now that we have replaced the km.res file, it is time to create a new icudt44l.dat<br>
<br>
Change directory<br>
<b>cd /Desktop/icudt44l/</b> <br>
<br>
Command to Repack<br><br>
<b>./gencmn -v -n icudt44l 0 < ../out.txt</b>
<br><br>
Now, if everything went well, you should have in /Desktop/icudt44l/ a new icudt44l.dat. <br><br>
This is your new icu file.<br>
<br>
<br>

<h2>Step 6: Rename/Replace the old icudt44l.dat by the new icudt44l.dat</h2>
Now SSH to your iphone to /usr/share/icu/ <br>
Rename icudt44l.dat to icudt44l.dat.bak <br>
Copy the new created icudt44l.dat to /usr/share/icu/icudt44l.dat <br>
Now you cross your fingers ... ;) <br><br>

<b>CRITICAL</b><br>
If you properly created the icudt44l.dat you shouldn't have any problem.<br>
Otherwise, you will be stuck in loop in the next step.<br><br>
<h2>Step 7: Respring</h2>
Now Respring or Restart your iPhone. <br><br>
If everything ok, then after few seconds your phone will be on.<br>
If you are stuck in mode loop, then SSH with your iPhone during this time, and replace the new  icudt44l.dat by the old saved  icudt44l.dat<br><br><br>


As you can understand, this operation is risky, but can be done. it is recommended to expert user only.<br>
<br>
<br>
<br>
<br>
<br>