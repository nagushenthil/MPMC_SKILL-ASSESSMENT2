# MPMC_SKILL-ASSESSMENT2
# GENERATE A 5 SECOND DELAY USING TIMER0 IN MODE1 AND TOGGLE PORT 2.7 CONTINUOUSLY
## AIM
To write an Assembly language program in 8051 to generate a 5 second delay using Timer 0 (Mode 1) and continuously toggle bit P2.7.
``

## APPARATUS REQUIRED
- Personal computer with KEIL Software

---

## ALGORITHM

1. Start the program.


2. Configure Timer 0 in Mode 1 (16-bit timer).


3. Load initial count in TH0 and TL0 for 50 ms delay.


4. Run the timer and wait for TF0 flag to be set.


5. Stop the timer and clear TF0 flag.


6. Repeat the delay routine 100 times to get approximately 5 seconds.


7. Toggle bit P2.7.


8. Repeat the above steps continuously.
---

## FLOWCHART
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/fec8074a-dfaa-46e5-96d2-0277368ea5c9" />



---

## PROGRAM
```asm
ORG 0000H

MAIN:  
    MOV P2, #00H           
HERE:  
    ACALL DELAY_5S         
    CPL P2.7               
    SJMP HERE              

DELAY_5S:
    MOV R5, #100           
BACK:
    ACALL DELAY_50MS
    DJNZ R5, BACK
    RET

DELAY_50MS:
    MOV TMOD, #01H         
    MOV TH0, #3CH          
    MOV TL0, #0B0H         
    SETB TR0               
WAIT:
    JNB TF0, WAIT          
    CLR TR0                
    CLR TF0                
    RET

END

```
## OUTPUT

<img width="1920" height="1200" alt="Screenshot (62)" src="https://github.com/user-attachments/assets/2e466d1d-716c-4875-a626-0ce8a37974f2" />



---


## RESULT

The program is successfully assembled and executed in Keil µVision.

After simulation:

Port 2.7 (P2.7) of the 8051 microcontroller toggles its state every 5 seconds.

This means the bit P2.7 changes from 0 → 1 → 0 → 1... continuously, creating a square wave with a period of 10 seconds (5s ON + 5s OFF).

Hence, the output is a continuous toggling of P2.7 every 5 seconds.

---
