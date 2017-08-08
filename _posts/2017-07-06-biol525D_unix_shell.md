# Biol525D unix shell
Marcelo Mora  
30 de junio de 2017  


This is the first of a series of posts about what I am learning in the BIol525D class. I leave the link of the class here [link](https://github.com/owensgl/biol525D)

This post has my personal notes about unix shell commands

I will divide this commands in 

1. general commands
2. regular expressions
3. loops and scripts


# General scripts


```bash

bash #open bash shell terminal

~/.bashrc #file to add paths of programs by default

PATH=/Linux/bin/bwa-0.7.15:$PATH #add program path 

alias bwa="bwa-0.7.15" #use alias to control which program version to use

pwd #print working directory o whereamI

mkdir #make directory

rmdir #remove directory

man #show manual

cp # copy

cp -r mydirectory mydestination #copy a directory to a destination 

ls /home #the / looks for the top and find ahome directory

ls home #looks for a home directory whithin my working directory

ls -thor #shows files in reverse order --new files at bottom with details 

ls --help #shows all options of ls command

rm -r mydirectory #removes directory

rmdir #removes only a empty directory

mv notes.txt mydirectory/ #move file

mv notes.txt mydirectory/notes2017.txt #move file and change the name

wc -l file.txt #count the lines

cat text.txt #print file 

sort -n text.txt #sort by first line
sort -k2 text.txt #sort alphabetically the second column

head -n 1 text.txt # print first line

#you cannot write in the same file as you picked stuff from
################## for example################## 

sort -n text.txt > text.txt #results empty file as content was deleted

################################################

whatevercommand file.txt > newfile.txt # overwrite 

whatevercommand file.txt >> newfile.txt # concatenate

cat "new file.txt" #files with spaces have to include ""

wc -l *.pdb | sort -n | head -n 1 #use pipes, in pipes the data stays in RAM memory. It is faster than storing in disk memmory 

```

#sed, awk and cut


```bash


 sed '3q;d' remix.line.csv > t.txt #select 3th line in a table and save it in a file


#script 

input=$1
output=$2

#get rows that are interesting and merge them into a file

sed 's/gi|162960935|ref|NC_007146.2|pilon/NP/g' $input.csv \ #replace pubmed id number with word "NP"
| sed 's/gi|16271976|ref|NC_000907.1|pilon/KW20/g'  \  #replace pubmed id number with word "KW20"
| sed 's/gi|148826757|ref|NC_009567.1|pilon/PittGG/g' \  #replace pubmed id number with word "PittGG"
| sed -i '/PittGG/d' > ../tables/$output.csv  # delete all lines with PittGG word


awk '{print $1,$4,$7,$8}' $x >> ~/uptake/temp/$2 #print specific columns and put them in a file 


prefix=`basename $sample .t.span.gz`

zcat temp/$prefix.t.span.gz | awk '$1 == "gi|162960935|ref|NC_007146.2|pilon" && $4 == "gi|162960935|ref|NC_007146.2|pilon"' >> temp/$prefix.t2.span.gz #extract lines in which columns 1 and 4 match a pubmed id

zcat temp/$prefix.t.span.gz | awk '$9 == "+" && $10 == "-"' | awk '$6  - $3 < 1000' >> temp/$prefix.t2.span.gz  # extract lines that column 9 matches a + and column 10 a - and then those in which the product of column 6 and 3 is less than a 1000

zcat temp/$prefix.t.span.gz | awk '$9 == "-" && $10 == "+"' | awk '$5  - $2 < 10'>> temp/$prefix.t2.span.gz | gzip > bedpe/$prefix.span.gz


# script to select a value or element in a string, separated by ","

for num in $1
do
i=$2
cat $1 | cut -d "," -f ${i}
done

```



# screen


```bash

screen #open screen

screen -S name #create a new screen

screen -r name #return to your screen, it must be deattached first

screen -d name #deattach screen 

control-a-n #change screens

echo $STY  #check which screen am I connected

```



#wild cards


```bash



? #match any letter

* #match any letter or empty space

^ # get something at the beggining of  line

$ # get something at the end of a line

[AB] # list of permited characters (A or B)

grep -v #reverse grep does not take a given thing

```



#loops and scripts


```bash

#example 1
for x in file1.dat file2.dat # x can be any name, files can be replaced by *.dat
do
head -n 3 $x   #$ in $x tell to use variable in x 

#example 2
for datafile in *[AB].txt  # take files 
do
echo $filename stats-$datafile
done



for datafile in *[AB].txt  # take files 
do
bash goodstats $datafile stats-$datafile
done


for x in `cat list.txt`
do
echo $x
done


##############################scripts#######################

bash script.sh #run script

"$1" # use the first parameter

for datafile in "$@"   # "$@" takes first paramenter then takes second and so on
do 
  echo $datafile
  bash goodstats -/j 100 -r $datafile stats-$datastats
done


#############################################################

#byobu is a way to open diiferent windows and run scripts without interrupting them if the connection is lost

sudo apt-get install byobu

byobu

#in a sesion you can have different windows

# f2 or f3 make different windows

#############################################################

```




