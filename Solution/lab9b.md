# Solution to Lab9b

## Part 1: Git Basics

1. ```
   commit 6fbc2a24a8df50b8f6d6eeef004591748dabaed7 (HEAD -> master, dice)
   Author: Skye-ye <saber.ap.saikou@gmail.com>
   Date:   Fri Mar 22 00:09:10 2024 +0800
   
       Restrict input range for dice iterations and sides
   
   commit 67acf6a93514c9f1d16b92d31ef4170fd9d28674
   Author: Skye-ye <saber.ap.saikou@gmail.com>
   Date:   Fri Mar 22 00:08:40 2024 +0800
   
       Add dice rolling logic and output dice sum and sequence
   
   commit 7150ffda502c8f6d0c8108dbf70a49ec71ee2ca1
   Author: Skye-ye <saber.ap.saikou@gmail.com>
   Date:   Fri Mar 22 00:07:49 2024 +0800
   
       Add -s flag for number of sides on a die
   
   commit 69a8e1e39aaed63394936d8b46e217e58bb36fcd
   Author: Skye-ye <saber.ap.saikou@gmail.com>
   Date:   Fri Mar 22 00:10:18 2024 +0800
   
       dice rolling WIP
   
   commit b83229267596681e47e12594e61640b8e3a2005d (origin/master, origin/HEAD)
   Author: Owen Thompson <owent@berkeley.edu>
   Date:   Tue Oct 17 20:33:07 2023 -0700
   
       Fix script/lab numbering errors in lab7
   ```

2. `git diff HEAD~4 HEAD`

   ```
   diff --git a/b9/rand.py b/b9/rand.py
   index ca991ea..052b329 100644
   --- a/b9/rand.py
   +++ b/b9/rand.py
   @@ -23,7 +23,13 @@ def main():
        )
   
        # COMMIT 1: Add -s flag for number of sides on a die
   -
   +    parser.add_argument(
   +        "-s", "--sides",
   +        dest="sides",
   +        type=int,
   +        default=6,
   +        help="Number of sides on a die (max=20; ignored when flipping a coin)"
   +    )
   
        args = parser.parse_args()
   
   @@ -58,10 +64,26 @@ def flip_coin(iterations):
    def roll_dice(iterations, sides):
   
        # COMMIT 3: Restrict input range for dice iterations and sides
   +    if iterations > MAX_ITERATIONS or iterations < 0:
   +        print("Number of rolls must be in the range [0 - {}]"
   +                .format(MAX_ITERATIONS))
   +        return
   
   +    if sides > MAX_SIDES or sides < 1:
   +        print("Number of sides must be in the range [1 - {}]"
   +                .format(MAX_SIDES))
   +        return
   
        # COMMIT 2: Add dice rolling logic and output dice sum and sequence
   +    diceRecord, diceSum = [], 0
   +    for i in range(iterations):
   +        roll = random.randint(1, sides)
   +        diceRecord.append(roll)
   +        diceSum += roll
   
   +    print("{} roll(s) of a {}-sided die resulted in a sum of {}:"
   +            .format(iterations, sides, diceSum))
   +    print(*diceRecord, sep=', ')
   
        return
   ```

   

