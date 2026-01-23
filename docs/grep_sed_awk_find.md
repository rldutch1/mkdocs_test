#<h1>Linux Utilities:</h1>

#### AWK:
###### Remove duplicate lines using awk.
	- awk '!($0 in array) { array[$0]; print }' somefile.txt

###### Print all lines from /etc/passwd that have the same uid and gid (if column 3 = column 4).
	- awk -F ':' '$3==$4' /etc/passwd

#### GREP:
###### Print the matched line, along with the 3 lines after it.
	- grep -A 3 -i "example" somefile.txt

#### FIND:
###### Search all .sql files in the system and archive them.
	- find / -name *.sql -type f -print | xargs tar -cvzf sqlfiles.tar.gz

#### SED:
###### Remove carriage return from the end of a filename.
	- sed 's/.$//' somefile.txt

###### Add line number for all non-empty-lines in a file.
	- sed -n '1!G;h;$p' somefile.txt

###### Search and replace all the strings/patterns without opening a file.
	- sed 's/Old/New/' somefile.txt

###### Search and replace all the strings/patterns without opening all files.
	- sed -i -e 's/Old/New/g' *

###### Replace only the second occurrence on each line.
	- sed 's/Old/New/2' somefile.txt

###### Replace the second occurance of a string in a particular line.
	- sed '2 s/Old/New/' somefile.txt

###### Replace all occurrences of a string/pattern in a file.
	- sed 's/Old/New/g' somefile.txt

###### Exclude lines 2-4 of a file and print the rest.
	- sed -n '2,4p' somefile.txt

###### Print/display multiple consecutive lines (print lines 2 and 3, and 5 and 6).
	- sed -n -e '2,3p' -e '5,6p' somefile.txt

###### Print/display lines which contain a specific word.
	- sed -n /operating/p somefile.txt

###### Add a line in between each line in a file.
	- sed G somefile.txt

###### Eliminate blank lines or ignore them.
	- sed '/^$/d' somefile.txt

###### Remove any blank lines and any commented "#" lines from a file.
	- sed '/^#\|^$\| *#/d' somefile.conf

###### Delete all lines except the range specified?
	- sed '3,5!d' somefile.txt

###### Ignore the case-sensitivity when replacing a word replace all (Old or old).
	- sed 's/old/new/i' somefile.txt

###### From within the VI editor you can replace a character (semi-colon in this example) with a  literal carriage return character using Ctrl+V followed by Enter (or Ctrl+M):
	- :%s/;/^M/g

#### Top
###### To display only the processes that belong to a particular user use -u option. The following will show only the top processes that belongs to oracle user.
	- top -u oracle

#### XARGS:
###### Copy all .jpg images to another directory:
	- ls *.jpg | xargs -n1 -i cp {} /another/directory

###### Download all the URLs listed in filename.txt file:
	- cat filename.txt | xargs wget -c

