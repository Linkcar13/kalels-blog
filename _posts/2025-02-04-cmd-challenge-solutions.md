---
title: "Command Challenge: command Line Practice"
categories: [Linux]
tags: [Linux]
date: 2025-02-04 00:00:00 -0500
math: false
mermaid: true
pin: true
image:
  path: assets/img/cmd-challenge/cmd-challenge.png
---
---

Mastering Linux commands is a continuous journey, and Command Challenge offers a fun way to test and refine these skills. This blog serves as a personal journal where I document my progress, solutions, and experiences tackling the challenges. The goal is to strengthen command-line proficiency while keeping track of insights gained along the way. Whether overcoming tricky tasks or discovering new commands, this space reflects the learning process and evolution in working with Linux.

## First Challenge

---

> 🐌  
> Your first challenge is to print "hello world" on the terminal in a single command.  
> 💡 Hint: There are many ways to print text on the command line, one way is with the 'echo' command. Try it below and good luck!

### Solutions

```bash
echo "hello world" #principal solution
printf "hello world" #alternative
```

## Second Challenge

---

> 🦋  
> Print the current working directory.

### Solutions

```bash
pwd #principal solution
echo  $PWD #alternative
```

## Third Challenge

---

> 🐛  
> List names of all the files in the current directory, one file per line.

### Solutions

```bash
ls #principal
for f in *;do echo "$f";done #oneline bash scripting
```

## Fourth Challenge

---

> 🦗  
> There is a file named `access.log` in the current directory. Print the contents.

### Solutions

```bash
cat access.log #principal
while read line; do echo $line; done < access.log #oneline bash scripting
grep '.*' access.log #mediante filtrado del archivo
```

## Fifth Challenge

---

> 🕸️  
> Print the last 5 lines of "access.log".

### Solutions

```bash
tail -5 access.log #principal
## dado que el archivo tiene 10 lineas
sed -n '6,10p' access.log ## alternative if you know the lenght of file
awk '{if (NR>5) print $0}' access.log ## alternative if you know the lenght of file
```

## Sixth Challenge

---

> 🐬  
> Create an empty file named `take-the-command-challenge` in the current working directory.

### Solutions

```bash
touch take-the-command-challenge #principal
cat > take-the-command-challenge ## alternative with standard output
type NUL > take-the-command-challenge ## alternative with NUL reserved word and standar output
```

## Seventh Challenge

---

> 🐬 ## Create a directory named `tmp/files` in the current working directory  
> 💡_Hint: The directory "`tmp/`" doesn't exist, with one command you need to create both "`tmp/`" and "`tmp/files`"_

### Solutions

```bash
mkdir tmp && mkdir tmp/files #principal
mkdir -p tmp/files # principal
mkdir {tmp/,tmp/files}
```

## Eighth Challenge

---

> 🐬 Copy the file named `take-the-command-challenge` to the directory `tmp/files`

### Solutions

```bash
cp take-the-command-challenge tmp/files ##principal
```

## Ninth Challenge

---

> 🐟 Move the file named `take-the-command-challenge` to the directory `tmp/files`

### Solutions

```bash
mv take-the-command-challenge tmp/files 2>/dev/null ##principal
```

## Tenth Challenge

---

> 🐟 A symbolic link is a type of file that is a reference to another file.  
> Create a symbolic link named `take-the-command-challenge` that points to the file `tmp/files/take-the-command-challenge`.

### Solutions

```bash
ln -s tmp/files/take-the-command-challenge take-the-command-challenge ##principal
cp -s tmp/files/take-the-command-challenge take-the-command-challenge ## copia de archivo simbolica
```

## Eleventh Challenge

---

> 🐟 Delete all of the files in this challenge directory including all subdirectories and their contents.  
> 💡Hint: There are files and directories that start with a dot "`.`", "`rm -rf *`" won't work here!

### Solutions

```bash
rm -rf * .* #principal
find . -type f,d -delete # secundario con find
```

## Twelfth Challenge

---
> remove files with extension
> There are files in this challenge with different file extensions. Remove all files with the .doc extension recursively in the current working directory.

```bash
find -name "*.doc" -delete #principal
find -name "*.doc" | xargs rm # secundario con find
```
