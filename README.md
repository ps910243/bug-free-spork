Objective:
The objective of the project is to create an interactive electronic dice using assembly language for the 8086 microprocessor, providing a fun and educational programme that emulates the randomness of rolling a traditional six-sided die, thereby solving the problem of needing a dice for dice-based games.
 
Abstract:
The core of the project is the assembly language program developed for the 8086 microprocessor. This program generates random numbers in the range of 1 to 6, mimicking the randomness of rolling a physical die. Users interact with the program to initiate a simulated roll, and the result is displayed as if they had rolled a physical die. While the project does not include the physical hardware, it provides a software-based solution for dice-based games, simulations, or educational purposes.
The significance of this project lies in its ability to offer a purely software-driven alternative for dice-based applications. It addresses the need for a digital solution that emulates the randomness of rolling a die, making it suitable for a wide range of applications while promoting assembly language programming skills and knowledge.
The project's main findings and outcomes include:
• Development of an assembly language program capable of generating random numbers and emulating dice rolls.
• Creation of a user-friendly interface for initiating the simulated dice rolls.
• A valuable educational experience in assembly language programming for the 8086 microprocessor.
• Provision of a software-based solution for dice-based games, simulations, or educational tools.
This project, although limited to software, successfully provides a digital alternative for dice-based applications and contributes to the development of assembly language programming skills.
 
 
Hardware / Software Requirements:
emu8086
 
 
 
 
Working Principle:
Data Segment:
• In this section, you declare data variables and messages for your program.
• COUNT is used to keep track of how many times '6' is rolled consecutively.
• CHOICE stores the user's input (1 for rolling the dice, 0 for stopping).
• RINT is an unused variable.
• MSG1, MSG2, MSG3, MSG4, and MSG5 are messages to be displayed.
• REC is an array to record the random numbers generated during the rolls.
Code Segment:
• The code execution starts at the START label in the code segment.
Display Messages:
• The program begins by displaying "ENTER 1-ROLL THE DICE 0 -TO STOP" and "ENTER YOUR CHOICE" messages to prompt the user for input.
User Input:
• The program reads the user's input (either '0' to exit or '1' to roll the dice) using INT 21H with AH=01H and stores it in the CHOICE variable.
Check for Exit:
• The program checks if the user's choice is '0'. If it is, the program jumps to the EXIT section to terminate the program. If not, it proceeds to roll the dice.
Generate a Random Number:
• The program generates a random number to simulate a dice roll:
• It obtains the system time using INT 21H with AH=2CH.
• It divides the value of AX by 6 (using DIV CX) to get a remainder between 0 and 5.
• It adds 1 to the remainder in DL to obtain a random number between 1 and 6, which simulates a dice roll.
Count Successive Sixes:
• The program checks if the generated random number is '6'.
• If it's a '6', it increments the COUNT variable to keep track of successive '6's.
Display "BINGO" Message:
• If the random number is '6' and there have been three successive '6's (as indicated by COUNT equaling 3), the program displays a "BINGO" message.
Jump Back to Menu:
• The program then jumps back to the menu (the UP label) to allow the user to continue rolling the dice or exit.
Exit:
• If the user chooses to exit (by entering '0'), the program displays an "EXIT" message using INT 21H with AH=09H and then terminates the program using INT 21H with AH=4CH.
 
Programme:
 
ASSUME CS:CODE, DS:DATA
 
DATA SEGMENT
   CHOICE DB 0      ; Initialize CHOICE to 0
   MSG1 DB 10, 13, "ENTER 1-ROLL THE DICE 0 -TO STOP$"
   MSG2 DB 10, 13, "ENTER YOUR CHOICE$"
   MSG3 DB 10, 13, "RANDOM NUMBER GENERATED IS $"
   MSG4 DB 10, 13, "-------EXIT !!!!------$"
   REC DB 100 DUP(0)
DATA ENDS
 
CODE SEGMENT
START:
   MOV AX, DATA
   MOV DS, AX
   LEA SI, REC
   INC SI
   INC SI
   INC SI
UP:
   LEA DX, MSG1
   MOV AH, 09H
   INT 21H
   LEA DX, MSG2
   MOV AH, 09H
   INT 21H
   MOV AH, 01H
   INT 21H
   MOV CHOICE, AL  ; Store the user's choice in CHOICE
   CMP AL, '0'
   JE EXIT
   LEA DX, MSG3
   MOV AH, 09H
   INT 21H
   MOV AH, 2CH
   INT 21H
   MOV AX, DX
   MOV DX, 0
   MOV CX, 6
   DIV CX
ADD DL, '0'
   ADD DL, 1
   MOV [SI], DL
   INC SI
   MOV AH, 02H
   INT 21H
   JMP UP
EXIT:
   LEA DX, MSG4
   MOV AH, 09H
   INT 21H
   MOV AH, 4CH
   INT 21H
CODE ENDS
END START
 
Flowchart:
Start/End Terminal
|
Initialization Process Block
|
Input/Output Block (Display menu, Read user choice)
|
Decision Block (User choice: '0' or '1')
|
|--- 0: Input/Output Block (Display "EXIT" message)
|       |
|       End Terminal
|
|--- 1: Process Block (Generate a random number)
|       |
|       Process Block (Display the random number)
|       |
|       Input/Output Block (Display "RANDOM NUMBER GENERATED IS")
|       |
|       Input/Output Block (Display the generated random number)
|       |
|       Input/Output Block (Prompt to roll again or exit)
|       |
|       Decision Block (Repeat or Exit)
|           |
|           |--- Yes: Loop back to Input/Output Block (Menu)
|           |
|           |--- No: Input/Output Block (Display "EXIT" message)
|               |
|               End Terminal
|
End Terminal
