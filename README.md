# LI-Practicas 3 de Abril 2025
## Practica 1/2: Convertir un número ingresado de Celsius a Fahrenheit.
### Codigo
```
// Autor: DE HARO RAMIREZ ISAAC
// Fecha: 2025-04-02
// Descripción: Convierte una temperatura de Celsius a Fahrenheit en ARM64.

.global _start

.section .data
    mensaje_pedir:  .asciz "Ingresa la temperatura en Celsius: " // Ahora tiene ":" y un espacio
    mensaje_result: .asciz "Temperatura en Fahrenheit: "
    nueva_linea:    .asciz "\n"

.section .bss
    num: .skip 10   // Buffer para almacenar el número ingresado
    resultado: .skip 20 // Buffer para almacenar el resultado en ASCII

.section .text
_start:
    // Mostrar mensaje de solicitud con ": " al final
    mov x0, 1                  
    ldr x1, =mensaje_pedir     
    mov x2, 33                 
    mov x8, 64                 
    svc 0

    // Leer número del usuario
    mov x0, 0                  
    ldr x1, =num               
    mov x2, 10                 
    mov x8, 63                 
    svc 0

    // Convertir cadena a número
    ldr x1, =num               
    bl str_to_int              
    mov x3, x0                 // Guardamos el número en x3 (Celsius)

    // Convertir Celsius a Fahrenheit: (C * 9/5) + 32
    mov x4, x3                 // Copia Celsius a x4
    mov x5, 9                  
    mul x4, x4, x5             // x4 = C * 9
    mov x5, 5
    udiv x4, x4, x5            // x4 = (C * 9) / 5
    add x4, x4, 32             // x4 = ((C * 9) / 5) + 32

mostrar_resultado:
    // Mostrar mensaje de resultado
    mov x0, 1
    ldr x1, =mensaje_result
    mov x2, 25
    mov x8, 64
    svc 0

    // Convertir resultado a ASCII y mostrarlo
    mov x0, x4                 
    ldr x1, =resultado         
    bl int_to_str              

    mov x0, 1
    ldr x1, =resultado
    mov x2, 20                 
    mov x8, 64
    svc 0

    // Nueva línea
    mov x0, 1
    ldr x1, =nueva_linea
    mov x2, 1
    mov x8, 64
    svc 0

exit:
    mov x8, 93                 
    mov x0, 0
    svc 0

// -------------------------
// Función: str_to_int (Convierte cadena ASCII a número)
// -------------------------
str_to_int:
    mov x0, 0                  
    mov x2, 10                 

loop:
    ldrb w3, [x1], 1           
    cmp w3, '0'                
    blt done                   
    cmp w3, '9'                
    bgt done                   
    sub w3, w3, '0'            
    mul x0, x0, x2             
    add x0, x0, x3             
    b loop                     

done:
    ret

// -------------------------
// Función: int_to_str (Convierte entero a ASCII)
// -------------------------
int_to_str:
    mov x2, 10                 
    add x1, x1, 19             
    mov w3, 0x0A               
    strb w3, [x1], -1          

convert_loop:
    udiv x4, x0, x2            
    msub x5, x4, x2, x0        
    add x5, x5, '0'            
    strb w5, [x1], -1          
    mov x0, x4                 
    cbz x0, conversion_done    
    b convert_loop             

conversion_done:
    ret
```

## Practica 2/2: Escribir un programa en ensamblador ARM64 que ordene un arreglo de enteros en orden ascendente (Bubble Sort).
### Codigo
```
```

## Asciinema
