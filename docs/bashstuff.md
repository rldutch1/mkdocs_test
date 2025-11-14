#Bash Stuff
####Bash ALIASES
<pre>
  <span style="color: #3366ff;">#alias ports='ss -lt'</span>
  <span style="color: #3366ff;">#alias ports1='netstat -pantu'</span>
  <span style="color: #3366ff;">alias netsettings='nmcli'</span>
  <span style="color: #3366ff;">alias diskdata='duf'</span>
  <span style="color: #3366ff;">alias foldershow='ncdu'</span>
  <span style="color: #3366ff;">alias LSBlk='lsblk -o +UUID,PARTUUID'</span>
  <span style="color: #3366ff;">alias LSBlk1='lsblk -o +UUID,FSTYPE,PARTUUID'</span>
  <span style="color: #3366ff;">alias LSBLK='lsblk -o \"NAME,MAJ:MIN,RM,SIZE,RO,FSTYPE,MOUNTPOINT,UUID\"'</span>
  <span style="color: #3366ff;">alias diskbyid='ls -lF /dev/disk/by-id'</span>
  <span style="color: #3366ff;">alias disku='duf'</span>
  <span style="color: #3366ff;">alias rootcompare='sudo QT_GRAPHICSSYSTEM=native bcompare'</span>
  <span style="color: #3366ff;">alias showdisks='sudo lshw -short -C disk'</span>
  <span style="color: #3366ff;">alias minecraft='~/.minecraft/launcher/minecraft-launcher'</span>
  <span style="color: #3366ff;">alias lsblk2='lsblk -o type,name,label,partlabel,size,fstype,model,serial,wwn,uuid'</span>
  <span style="color: #3366ff;">#alias youtube='echo yt-dlp <url>'</span>
  <span style="color: #3366ff;">alias ssh='ssh -XC'</span>
</pre>

#### Bash ARRAYS:
Are you finding it challenging to determine the length of an array in Bash? You’re not alone. Many developers find themselves puzzled when it comes to handling arrays in Bash, but we’re here to help.

Think of Bash’s array length command as a measuring tape – allowing us to quickly and accurately gauge the size of our arrays, providing a versatile and handy tool for various tasks.

In this guide, we’ll walk you through the process of determining the length of an array in Bash, from the basics to more advanced techniques. We’ll cover everything from the simple use of the <span style="color: #3366ff;">${#array[@]}</span> syntax to more complex scenarios, as well as alternative approaches.

Let’s get started!
##### How Do I Find the Length of an Array in Bash?

To find the length of an array in Bash, you can use the <span style="color: #3366ff;">${#array[@]}</span> syntax. This command will return the number of elements in the array.

Here’s a simple example:
<span style="color: #3366ff;"><br />
array=("apple" "banana" "cherry")<br />
echo "${#array[@]}"<br />
</span>

###### Output the number of elements in the array:
<span style="color: #3366ff;">
 3
</span>

In this example, we’ve created an array with three elements: ‘apple’, ‘banana’, and ‘cherry’. The <span style="color: #3366ff;">${#array[@]}</span> syntax is used to find the length of the array, which in this case is 3.

##### Bash Array Length: The Basics

Before we dive into complex scenarios, let’s start with the basics of finding the length of an array in Bash. The syntax for finding the length of an array is <span style="color: #3366ff;">${#array[@]}</span>.

Let’s look at a simple example:
<span style="color: #3366ff;"><br />
fruits=("apple" "banana" "orange" "grape" "pineapple")<br />
echo "${#fruits[@]}"
</span>

###### Output the length of an array:
<span style="color: #3366ff;">
5
</span>

In this example, we’ve created an array named ‘fruits’ with five elements. We then use the <span style="color: #3366ff;">${#fruits[@]}</span> syntax to find the length of the array, which returns 5, as there are five elements in the array.

This basic usage of the <span style="color: #3366ff;">${#array[@]}</span> syntax is the foundation for finding the length of an array in Bash. As you become more comfortable with this concept, you can start to explore more advanced scenarios.

Intermediate Bash: Length of Multi-Dimensional Arrays and Empty Elements

As you gain more experience with Bash, you’ll likely encounter more complex scenarios. For example, you may need to determine the length of a multi-dimensional array or handle arrays with empty elements. Let’s take a closer look at these situations.

##### Multi-Dimensional Arrays
In Bash, multi-dimensional arrays aren’t supported directly. However, you can simulate them using one-dimensional arrays. Here’s an example:
<span style="color: #3366ff;"><br />
matrix=("1 2 3" "4 5 6" "7 8 9 0")<br />
for row in "${matrix[@]}"; do<br />
    set -- $row<br />
    echo "${#matrix[@]}"<br />
done
</span>

###### Output the number of elements in each row of the array:
<span style="color: #3366ff;"><br />
 3<br />
 3<br />
 3
</span>

In this example, we’ve created a simulated 3×3 matrix. Each element of the ‘matrix’ array is a string representing a row of the matrix. The set -- $row command splits the string into separate elements, and ${#*[@]} gives the number of elements in each row, effectively giving us the ‘length’ of each dimension.

##### Handling Empty Elements in an array:
Bash considers an empty string as a valid array element. Therefore, it contributes to the length of the array. Let’s see this in action:
<span style="color: #3366ff;"><br />
array=("apple" "" "cherry")<br />
echo "${#array[@]}"<br />
</span>

###### Array with empty string output:
<span style="color: #3366ff;">3</span>

In this example, ‘apple’, an empty string, and ‘cherry’ are the elements of the array. Even though the second element is an empty string, Bash counts it as a valid element, so the length of the array is 3.

These are some of the more complex scenarios you might encounter when finding the length of an array in Bash. Understanding these concepts will help you handle arrays more effectively in your scripts.
Alternative Methods: Bash Array Length

While the <span style="color: #3366ff;">${#array[@]}</span> syntax is the most straightforward way to determine the length of an array in Bash, there are alternative approaches you can use. Let’s explore some of these methods, their benefits, drawbacks, and when to use them.
Using a Loop

##### Find the length of an array:
One way to find the length of an array is by using a loop to iterate over the array elements. Here’s an example:
<span style="color: #3366ff;"><br />
fruits=("apple" "banana" "orange" "grape" "pineapple")<br />
length=0<br />
for fruit in "${fruits[@]}"; do<br />
    length=$((length+1))<br />
done<br />
echo $length
</span>

###### Length of an array output:
<span style="color: #3366ff;">5</span>

In this example, we initialize a counter (length) to zero. Then, for each element in the array, we increment the counter by one. After the loop, length holds the number of elements in the array.

This method provides more control and can be useful in scenarios where you want to perform additional operations on each element. However, it’s more verbose and less efficient than the <span style="color: #3366ff;">${#array[@]}</span> syntax.
Using External Commands

##### Length of array using printf and wc:
You can also use external commands like awk or wc to find the length of an array. Here’s an example using printf and wc:
<span style="color: #3366ff;"><br />
fruits=("apple" "banana" "orange" "grape" "pineapple")<br />
length=$(printf '%s\n' "${fruits[@]}" | wc -l)<br />
echo $length
</span>

###### Length of array using printf and wc output:
<span style="color: #3366ff;">5</span>

In this example, we use printf to print each element on a new line, then pipe the output to wc -l to count the number of lines. This gives us the number of elements in the array.

This method can handle large arrays and complex string manipulations, but it’s slower and less readable than the <span style="color: #3366ff;">${#array[@]}</span> syntax. It also depends on external commands, which may not be available in all environments.

In conclusion, while the <span style="color: #3366ff;">${#array[@]}</span> syntax is generally the best way to find the length of an array in Bash, understanding these alternative methods can broaden your scripting skills and help you tackle a wider range of problems.
Troubleshooting Bash Array Length

While finding the length of an array in Bash is generally straightforward, there are some common issues that you might encounter. In this section, we’ll discuss these potential problems and provide solutions to overcome them.

##### Special Characters in Array Elements
Bash treats some characters as special, which can cause unexpected behavior when they’re included in array elements. Let’s look at an example:
<span style="color: #3366ff;"><br />
array=("apple" "banana \n cherry")<br />
echo "${#array[@]}"
</span>

###### Special chracters output:
<span style="color: #3366ff;">2</span>

In this example, the array has two elements: ‘apple’ and ‘banana \n cherry’. Despite the newline character (\n) in the second element, Bash still counts it as a single element, so the length of the array is 2.

To handle special characters in array elements, you can use quotes to treat the entire string as a single element.

Large Arrays<br />
When dealing with large arrays, the <span style="color: #3366ff;">${#array[@]}</span> syntax can become slow. In these cases, you might want to consider using an external command like wc, as discussed in the ‘Alternative Approaches’ section.

Here’s a code example for handling large arrays:

<span style="color: #3366ff;">
large_array=($(seq 1 10000))<br />
length=$(printf '%s\n' "${large_array[@]}" | wc -l)<br />
echo $length<br />
</span>

##### Large array count output:
<span style="color: #3366ff;">10000</span>

In this example, we’ve created a large array with 10,000 elements using the seq command. We then use printf and wc to find the length of the array.

Remember, while this method can handle large arrays, it’s slower and less readable than the <span style="color: #3366ff;">${#array[@]}</span> syntax. It also depends on external commands, which may not be available in all environments.

By understanding these common issues and their solutions, you can handle arrays more effectively in your Bash scripts.

Understanding Arrays in Bash

Before we delve deeper into the nuances of determining the length of arrays in Bash, it’s crucial to understand what arrays are and how they function in Bash.
What is an Array?

An array is a data structure that stores a collection of elements. These elements, also known as values, are stored in a specific order and can be accessed by their index, which is their position in the array.

In Bash, arrays are zero-indexed, meaning the first element is at index 0, the second element is at index 1, and so on.

Here’s a simple example of an array in Bash:

fruits=("apple" "banana" "cherry")<br />
<span style="color: #3366ff;">echo "${fruits[0]}"</span>

###### Simple array output:
<span style="color: #3366ff;">apple</span>

In this example, ‘apple’, ‘banana’, and ‘cherry’ are the elements of the array. The command <span style="color: #3366ff;">echo "${fruits[0]}"</span> prints the first element of the array, which is ‘apple’.
Manipulating Arrays in Bash

##### Add element to an array:
Bash provides various commands to manipulate arrays, such as adding elements, removing elements, and finding the length of an array.

For instance, to add an element to an array, you can use the following syntax:
<span style="color: #3366ff;"><br />
fruits=("apple" "banana" "cherry")<br />
fruits+=("orange")<br />
echo "${fruits[@]}"<br />
</span> <br />

###### Add element to an array output:
<span style="color: #3366ff;">apple banana cherry orange</span>

In this example, we’ve added ‘orange’ to the ‘fruits’ array. The += operator is used to append elements to an array in Bash.
Data Structures in Bash

In addition to arrays, Bash supports other data structures like strings and associative arrays. While strings are simple data structures that hold a sequence of characters, associative arrays (also known as hash maps) are more complex and hold pairs of keys and values.

Understanding these fundamental concepts about arrays and data structures in Bash is crucial for effective scripting. With this knowledge, you can better understand how to determine and manipulate the length of an array in Bash.
The Power of Arrays in Bash Scripting

Arrays are incredibly versatile and powerful tools in Bash scripting. They are fundamental to a multitude of tasks and operations, making them an indispensable part of any Bash programmer’s toolkit.
Arrays in File Handling

##### List of files:
Arrays can be used to handle files and directories in Bash. For instance, you can store the list of files in a directory in an array and perform operations on each file. Here’s an example:
<span style="color: #3366ff;"><br />
files=(/path/to/directory/*)<br />
for file in "${files[@]}"; do<br />
    echo "Processing $file"<br />
done
</span> <br />

###### List of files in array output:
<span style="color: #3366ff;"><br />
 Processing /path/to/directory/file1<br />
 Processing /path/to/directory/file2
 ...
</span>

In this example, we’ve stored all the files in a directory in an array. We then iterate over the array and print a message for each file.
Arrays in Data Processing

##### Processing lines in a .csv file:
Arrays also play a crucial role in data processing tasks in Bash. They can be used to store and manipulate data, making it easier to perform complex operations. For instance, you can use an array to store the lines of a CSV file and process each line. Here’s an example:
<span style="color: #3366ff;"><br />
IFS=$'<br />
' lines=($(cat data.csv))<br />
for line in "${lines[@]}"; do<br />
    echo "Processing $line"<br />
done
</span> <br />
###### Processing lines of a .csv file output:
<span style="color: #3366ff;"><br />
 Processing line1<br />
 Processing line2
 ...
</span>

In this example, we’ve read a CSV file line by line into an array using the cat command. We then iterate over the array and process each line.

[Source1:](https://ioflood.com/blog/bash-length-of-array/)<br />
[Source2:](https://www.geeksforgeeks.org/bash-scripting-array/)

####Bash FUNCTIONS:
  <span style="color: #000000;">
    <span style="color: #3366ff;">thefunctionname()</span> {<br />
    <span style="color: #3366ff;">if</span> [ $# -eq 0 ]<br />
    <span style="color: #3366ff;">then</span><br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Usage: thefunctionname someargument"<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Example: Blah blah blah."<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "     thefunctionname someargument"<br />
    <span style="color: #3366ff;">else</span><br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Running thefunctionname... " $1<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;thefunctionname $1<br />
    <span style="color: #3366ff;">fi</span><br />
    }<br />
	</span>

  <span style="color: #000000;">
    A function using if/case:<br >
    <span style="color: #3366ff;">anotherfunction()</span> {<br />
    <span style="color: #3366ff;">if</span> [ $# -eq 0 ]<br />
    <span style="color: #3366ff;">then</span><br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "anotherfunction someargument"<br />
    <span style="color: #3366ff;">else</span><br />
    <span style="color: #3366ff;">case</span> $1 in<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;argument1)<br />
            	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;do some work<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;argument2)<br />
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;do some work<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;<br />
            *)<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;message="Default message if no argument is supplied."<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo $message<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;<br />
    <span style="color: #3366ff;">esac</span><br />
    <span style="color: #3366ff;">fi</span><br />
    }<br />
	</span>

####STAT command:
   <span style="color: #3366ff;">stat -c "%a %n %C" filename.txt </span><br />

####Multiple search using grep:
   <span style="color: #3366ff;">grep 'word1.&#42;word2' logs </span><br />
   <span style="color: #3366ff;">ls -al |grep 'rob.&#42;Nov.&#42;mp3' |grep -v ".sh" </span><br />
   <span style="color: #3366ff;">ip addr |grep -i 'inet.&#42;global' </span><br />

####The following examples prints numbers from 1 to 10 using the for and while loops
   <span style="color: #3366ff;">echo "for(i=1;i<=10;i++) {i;}" | bc </span><br />
   <span style="color: #3366ff;">echo "i=1; while(i<=10) {i; i+=1}" | bc </span><br />

####For loop (count):
<span style="color: #3366ff;">
  y=1<br />
  for x in *.jpg<br />
  do<br />
  echo $y<br />
  	mv $x 20241215_sequentially_numbered_file_$y.jpg<br />
  	((y++))<br />
  done<br />
 </span>

####For loop on multiple file extensions:
<span style="color: #3366ff;">for i in {*.gz,*.rar}<br />
	do<br />
		ls -al > "$i"<br />
	done<br />
<br />
	rm -f *.gz *.rar<br />
</span><br />

####While loop (count):
<span style="color: #3366ff;">
  counter=0<br />
  while [ $counter -lt 5 ]; do<br />
    echo "Counter: $counter"<br />
    ((counter++))<br />
  done<br />
 </span>

####Increment a variable inside a bash loop:
<span style="color: #3366ff;">
FILE=$1<br />
<br />
tail -n40 mylog > $FILE #Send the contents of mylog to $FILE<br />
<br />
while read country _; do<br />
  if [ "US" = "$country" ]; then #Search for US in the $country variable.<br />
        USCOUNTER=$(expr $USCOUNTER + 1) #Increment by one for each US found.<br />
        echo "Found $USCOUNTER US" #Display the incremented count.<br />
  fi<br />
done < "$FILE"<br />
  echo "Found a total of $USCOUNTER US." #Display the final count of US.<br />
 </span>
[Source:](https://stackoverflow.com/questions/20681210/incrementing-a-variable-inside-a-bash-loop)<br />

####Other options for counting "US" from above:
<span style="color: #3366ff;">
        grep -cE "^([^ ]&#42; ){0}US" mylog<br />
 </span>
    #      -c count<br />
    #      ([^ ]* ) To detect a column<br />
    #      {0} the column number<br />
    #      US your pattern<br />

####Increment with array example to convert png files to jpg using ImageMagick:
<span style="color: #3366ff;">
		#files=(/home/rob/Pictures/Screenshots/{*.png,*.jpg})<br />
		files=(/home/rob/Pictures/Screenshots/*.png)<br />
		#TIMESTAMP=&#96;date +"%Y%m%d%H%M%S%Z"&#96;<br />
		TIMESTAMP=&#96;date +"%Y%m%d%H%M"&#96;<br />
		y=$TIMESTAMP"0000000" #Adjust the number of zeros according to the number of digits in the date (19 digits max on 64bit systems).<br />
		echo "" > $TIMESTAMP"_log.txt"<br />
for file in "${files[@]}"; do<br />
    #echo "cp \"$file\" /home/rob/Pictures/Screenshots/xyz/$y.png"<br />
    echo "magick '$file[800x600]' /home/rob/Pictures/Screenshots/xyz/$y.jpg"<br />
    echo "\"$file\" = $y.jpg" >> $TIMESTAMP"_log.txt"<br />
    ((y++))<br />
done<br />
 </span>

####Using the following 1 line command for renaming files in linux using a specific phrase:
<span style="color: #3366ff;">
find -type f -name '*.jpg' | rename 's/holiday/honeymoon/'
 </span><br />
For all files with the extension ".jpg", if they contain the string "holiday", replace it with "honeymoon". For instance, this command would rename the file "ourholiday001.jpg" to "ourhoneymoon001.jpg".<br />
<br />
This example also illustrates how to use the find command to send a list of files (-type f) with the extension .jpg (-name '*.jpg') to rename via a pipe (|). rename then reads its file list from standard input.<br />
[Source:](https://stackoverflow.com/questions/20681210/incrementing-a-variable-inside-a-bash-loop)<br />

#### Grep for multiple things at once:
The '-e' option allows you to search for multiple things. It is kind of like an 'or' statement. Example below, find postfix or mailx.<br />
<span style="color: #3366ff;">rpm -qa |grep -e postfix -e mailx</span><br />

#### Find Graphics or Video Card Information:
<span style="color: #3366ff;">lspci -k | grep -EA3 'VGA|3D|Display'</span><br />

#### List or rename files that start with a dash (-):
List all files that start with a dash:
<span style="color: #3366ff;">ls -al -- -*</span><br />

Rename a file that starts with a dash:
<span style="color: #3366ff;">mv -- -oldfilename.txt newfilename.txt</span><br />

Create a file that starts with a dash:
<span style="color: #3366ff;">touch -- -somefile.txt</span><br />

Remove multiple text files that start with a dash (-):
<span style="color: #3366ff;">rm -f ./-*.txt</span><br />

List all the .txt files that begin with a dash and create a list of them to be renamed:<br />
<span style="color: #3366ff;">ls -1 |awk {'print "mv -- "$1" "$1'} > rname.sh;chmod +x rname.sh;vi rname.sh</span><br />
	Open the rname.sh in VI editor and remove the dash, type:<br />
		<span style="color: #3366ff;">:%s/\.txt\ \-/\.txt\ /g</span><br />
