java cLab 4
Pointers

Structures
Part I: Nov. 4, 2024
Part II: Nov. 4, 2024
Faculty of Computing, HIT Weihai
Dept. of Computer Science  Technology
4-1/2-0
Pointers as Function Arguments
• Problem: how to exchange two variables using a function (p.95)
• Language points
➢Suppose main (the caller) calls swap (the callee)
➢Argument(s) passed from caller to callee by value
➢NOT vice versa
4-1-1
Faculty of Computing, HIT Weihai, 2024FA
Pointers as Function Arguments
• Problem: how to exchange two variables using a function (p.95)
• Language points
➢Suppose main (the caller) calls swap (the callee)
➢Argument(s) passed from caller to callee by value
➢NOT vice versa
• This program fails because of the wrong idea:
Since the value of a goes to x, afterwards the value of x will 
also go back to a automatically; same is true for b and y
a and x are the same variable (not only equal, but they are 
just one variable); b and y too 
4-1-2
Faculty of Computing, HIT Weihai, 2024FA
Assignment 0: See How It is Wrong
• Use GDB to step through the following program
4-1-3
Faculty of Computing, HIT Weihai, 2024FA
void swap(int x, int y)
{
 int temp;
 temp = x;
 x = y;
 y = temp;
}
#include 
int main()
{
 int x = 3, y = 4;
 swap(x, y);
 printf("%d %d", x, y);
}
Assignment 0: See How It is Wrong
• Use GDB to step through the following program
➢ Job 1:
✓ When in main, check out the address of x:
(gdb) p x
✓ When in swap, check out the address of x
✓ Consider: are they the same variable?
➢ Job 2:
✓ Just before leaving swap, check out the value of x:
(gdb) p x
✓ Immediately after getting back to main, check out the value of x
➢ Carefully record the above results and give your observation in the 
lab report.
4-1-4
Faculty of Computing, HIT Weihai, 2024FA
Assignment 1: Get the Task Done
• (p.96) By receiving the addresses of arguments from the caller, 
the callee manages to reach the original arguments, i.e. a and b
• Step through this program
4-1-5
Faculty of Computing, HIT Weihai, 2024FA
int main()
{
 int a = 3, b = 4;
 swap(a, b);
 printf("%d %d", a, b);
}
void swap(int *px, int *py)
{
 int temp;
 temp = *px;
 *px = *py;
 *py = temp;
}
Assignment 1: Get the Task Done
(Cont.)
• (p.96) By receiving the addresses of arguments from the caller, 
the callee manages to reach the original arguments, i.e. a and b
• Step through this program
➢ When in main, check out the addresses of a and b
➢ When in swap, see if you could still visit a (or b) directly:
(gdb) p a
✓ The reason is because we are now beyond the scope of a and b (§4.4)
✓ Sounds weird, but you just have to remember this rule
➢ However, we are sure to be able to visit a through its address, which is 
now held in pointer px:
✓ Try: (gdb) p px and (gdb) p *px
➢ Carefully record the above results and give your observation in the lab 
report.
4-1-6
Faculty of Computing, HIT Weihai, 2024FA
Assignmen代 写program、C/C++
代做程序编程语言t 2: Further Thinking
• Run the following program and try to explain why
• To troubleshoot, step through it using proper GDB commands
• Report your work.
4-1-7
Faculty of Computing, HIT Weihai, 2024FA
int main()
{
 int a = 3, b = 4;
 swap(a, b);
 printf("%d %d", a, b);
}
void swap(int *px, int *py)
{
 int *temp;
 temp = px;
 px = py;
 py = temp;
}
Arrays of Structures
• Consider the following array of structures:
athlete PRCplayers[] = {
 { "CHANG Yuan", 'F', 0x970624, "boxing", "100" },
 { "JI Bowen", 'M', 0x020222, "canoe", "100" },
 { "LIU Qingyi", 'F', 0x051019, "breaking", "001" }, 
 { "LIU Yang", 'M', 0x940910, "gymnastics", "110" }, 
 { "MA Long", 'M', 0x881020, "table tennis", "100" },
 { "PAN Zhanle", 'M', 0x040804, "swimming", "210" },
 { "SHENG Lihao", 'M', 0x041204, "shooting", "200" }, 
 { "WANG Zongyuan", 'M', 0x011024, "diving", "110" },
 { "WANG Chang", 'M', 0x010507, "badminton", "010" },
 { "ZHANG Yufei", 'F', 0x980419, "swimming", "015" },
};
4-2-1
Faculty of Computing, HIT Weihai, 2024FA
typedef struct {
 char *name;
 char gender;
 unsigned birthday;
 char *sport; 
 char *GSBmedals;
} athlete;
Arrays of Structures
– Comprehensive Problem Solving
• Assignment 3 (choose any ONE task):
➢ Calculate the average number of medals per capita
➢ Find out who has/have won the most gold medals
➢ Find out the youngest male athlete
➢ See if player SUN Yingsha is in this array, using binary search
➢ Rearrange the array into descending order by age, using any algorithm
➢ Show which athletes come from the same sport team, and which sport(s)
➢ Given the subscripts of any two players (0 for CHANG Yuan, …, 9 for 
ZHANG Yufei), calculate how many days one is older than the other
➢ Change all surnames from capital letters to lower case except for the 
initial letter; and show the full names of all players on the screen
• Report your work.
4-2-2
Faculty of Computing, HIT Weihai, 2024FA
Examples
• Insert the following element into the array:
{ "ZHENG Qinwen", 'F', 0x021008, "tennis", "100" }
➢ Step 1: find the proper position
➢ Step 2: move all elements behind it to make room for the insertion
➢ Step 3: put the new record into this vacated position
➢ Step 4: show the whole array (one more record than before)
4-2-3
Faculty of Computing, HIT Weihai, 2024FA
Examples – insert.c
• Language points
➢When applied to an array, sizeof() evaluates to the total 
number of bytes in this array; when applied to a structure, 
the result is the # of bytes in this type of structure
➢Structure variables CANNOT be compared directly
✓if (plyr == *pplyr) /* wrong! */
➢Bounds check: should loop condition be > or >=?
✓for (pplyr += n-1; n > 0; n--)
➢printf("%-15s\t%c\t%06x\t%-15s\t%s\n");
✓SHENG Lihao M 041204 badminton_______200
✓WANG Zongyuan M 011024 diving 110
4-2-4
Faculty of Computing, HIT Weihai, 2024FA
_______
__________
_____
___

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
