1. Write an assembly language program to perform addition of 8-bit data.

org 100h          ; Origin for .COM file (starts execution at address 100h)

; Define two 16-bit numbers to add
num1 dw 1234h     ; First number (4660 in decimal)
num2 dw 5678h     ; Second number (22136 in decimal)

start:
    ; Load the first 16-bit number into AX
    mov ax, [num1]
    
    ; Add the second 16-bit number to AX
    add ax, [num2]

    ; Result is now in AX, handle carry flag for overflow
    ; Convert the result to ASCII for printing
    mov bx, ax          ; Save the result in BX
    mov ah, 0           ; Clear AH (high byte of AX)

    ; Print the high byte of AX (higher 8 bits)
    mov al, ah          ; Move high byte to AL
    call print_hex      ; Print high byte

    ; Print the low byte of AX (lower 8 bits)
    mov al, bl          ; Move low byte to AL
    call print_hex      ; Print low byte

    ; Exit the program
    mov ah, 4Ch         ; DOS function to exit
    int 21h             ; Call DOS interrupt

; Subroutine to print a byte as a hexadecimal value
print_hex:
    ; Convert AL to ASCII hexadecimal representation
    mov ah, al          ; Copy value to AH
    and al, 0F0h        ; Mask high nibble
    shr al, 4           ; Shift to get high nibble
    add al, '0'         ; Convert to ASCII ('0' - '9')
    cmp al, '9'         ; Check if greater than '9'
    jbe print_hex_low   ; Jump if below or equal to '9'
    add al, 7           ; Adjust if needed (i.e., 'A' to 'F')

print_hex_low:
    mov dl, al          ; Move high nibble to DL for printing
    mov ah, 02h         ; DOS function to print character
    int 21h             ; Call DOS interrupt

    ; Print the low nibble
    mov al, ah          ; Restore value to AL
    and al, 0Fh         ; Mask low nibble
    add al, '0'         ; Convert to ASCII ('0' - '9')
    cmp al, '9'         ; Check if greater than '9'
    jbe print_hex_done  ; Jump if below or equal to '9'
    add al, 7           ; Adjust if needed (i.e., 'A' to 'F')

print_hex_done:
    mov dl, al          ; Move low nibble to DL for printing
    mov ah, 02h         ; DOS function to print character
    int 21h             ; Call DOS interrupt
    ret                 ; Return from subroutine



![image](https://github.com/user-attachments/assets/56465356-5999-4232-a870-0807017acf4a)





2. Write a program in assembly language to perform addition of 16-bit data.


\\code\\
org 100h

num1 dw 1234h
num2 dw 5678h

start:
    mov ax, num1
    add ax, num2

    mov bx, ax
    mov ah, bl
    and ah, 0fh
    shr ah, 4
    add ah, 30h
    cmp ah, 39h
    jle print_first_digit_high
    add ah, 7

print_first_digit_high:
    mov dl, ah
    mov ah, 02h
    int 21h

    mov ah, bl
    and ah, 0fh
    add ah, 30h
    cmp ah, 39h
    jle print_second_digit_high
    add ah, 7

print_second_digit_high:
    mov dl, ah
    mov ah, 02h
    int 21h

    mov ah, bh
    and ah, 0fh
    shr ah, 4
    add ah, 30h
    cmp ah, 39h
    jle print_first_digit_low
    add ah, 7

print_first_digit_low:
    mov dl, ah
    mov ah, 02h
    int 21h

    mov ah, bh
    and ah, 0fh
    add ah, 30h
    cmp ah, 39h
    jle print_second_digit_low
    add ah, 7

print_second_digit_low:
    mov dl, ah
    mov ah, 02h
    int 21h

    mov ah, 4ch
    int 21h

![image](https://github.com/user-attachments/assets/61493f17-23b3-4ecc-8112-9e9f5d533175)

