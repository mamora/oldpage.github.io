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




