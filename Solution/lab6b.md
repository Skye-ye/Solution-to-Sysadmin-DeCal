# Solution to Lab6b

## Exercise 1

**Why do you think this behavior occurs?**

### Answer
The `sleep` process is not associated with the TTY of the first terminal.

## Exercise 2

**What resource specifically does the `yes` command exhaust? **

### Answer

CPU resource

## Exercise 3

**What is the `sleep` process's parent?**

### Answer

`bash`

## Exercise 4

**Modify it to run every five minutes and make a note of the line you wrote. Then, quit out of the editor.**

### Answer

`*/5 * * * * date +"\%T" >> $HOME/timestamps.txt`

## Exercise 5

**What happens when you suspend the `job` command?**

### Answer

The `job` script stops running and the `~/count` file stops to update.

## Exercise 6

**What happens after running the `bg` command?**

### Answer

The `job` script starts running **background** from exactly the point it stopped.

## Exercise 7

**What is another way we can kill the job?**

### Answer

`kill %i` (where `i` is the number in the brackets)
