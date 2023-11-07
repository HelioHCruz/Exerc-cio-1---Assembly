# Exercício-1---Assembly Helio Henrique Cruz - FEAP AVARÉ -  Engenharia da Computação
section .data
    msgPrompt db "Digite seu nome: ", 0
    msgGreetings db "Olá", 0
    buffer resb 64 ; buffer para armazenar o nome do usuário

section .bss
    name resb 64 ; local para armazenar o nome do usuário

section .text
    global _start

_start:
    ; Escreve a mensagem de prompt
    mov eax, 4        ; syscall write
    mov ebx, 1        ; descritor de arquivo (stdout)
    mov ecx, msgPrompt
    mov edx, msgPromptLen
    int 0x80          ; chama o sistema

    ; Lê a entrada do usuário
    mov eax, 3        ; syscall read
    mov ebx, 0        ; descritor de arquivo (stdin)
    mov ecx, buffer
    mov edx, 64       ; tamanho máximo para a entrada
    int 0x80          ; chama o sistema

    ; Copia o nome para a área de armazenamento
    mov esi, buffer   ; origem
    mov edi, name     ; destino
    call copy_string

    ; Exibe a mensagem de saudações
    mov eax, 4        ; syscall write
    mov ebx, 1        ; descritor de arquivo (stdout)
    mov ecx, msgGreetings
    mov edx, msgGreetingsLen
    int 0x80          ; chama o sistema

    ; Exibe o nome
    mov eax, 4        ; syscall write
    mov ebx, 1        ; descritor de arquivo (stdout)
    mov ecx, name
    mov edx, 64       ; tamanho máximo do nome
    int 0x80          ; chama o sistema

    ; Sai do programa
    mov eax, 1        ; syscall exit
    xor ebx, ebx      ; código de saída
    int 0x80          ; chama o sistema

; Função para copiar uma string de origem para destino
copy_string:
    ; Entrada: ESI = origem, EDI = destino
    ; Saida: Nenhuma
    copy_loop:
        mov al, [esi]
        cmp al, 0
        je copy_done
        mov [edi], al
        inc esi
        inc edi
        jmp copy_loop
    copy_done:
        ret

section .data
    msgPrompt db "Digite seu nome: ", 0
    msgGreetings db "Olá", 0
    buffer resb 64 ; buffer para armazenar o nome do usuário

section .bss
    name resb 64 ; local para armazenar o nome do usuário

section .text
    global _start

_start:
    ; Escreve a mensagem de prompt
    mov eax, 4        ; syscall write
    mov ebx, 1        ; descritor de arquivo (stdout)
    mov ecx, msgPrompt
    mov edx, msgPromptLen
    int 0x80          ; chama o sistema

    ; Lê a entrada do usuário
    mov eax, 3        ; syscall read
    mov ebx, 0        ; descritor de arquivo (stdin)
    mov ecx, buffer
    mov edx, 64       ; tamanho máximo para a entrada
    int 0x80          ; chama o sistema

    ; Copia o nome para a área de armazenamento
    mov esi, buffer   ; origem
    mov edi, name     ; destino
    call copy_string

    ; Exibe a mensagem de Olá
    mov eax, 4        ; syscall write
    mov ebx, 1        ; descritor de arquivo (stdout)
    mov ecx, msgGreetings
    mov edx, msgGreetingsLen
    int 0x80          ; chama o sistema

    ; Exibe o nome
    mov eax, 4        ; syscall write
    mov ebx, 1        ; descritor de arquivo (stdout)
    mov ecx, name
    mov edx, 64       ; tamanho máximo do nome
    int 0x80          ; chama o sistema

    ; Sai do programa
    mov eax, 1        ; syscall exit
    xor ebx, ebx      ; código de saída
    int 0x80          ; chama o sistema

; Função para copiar uma string de origem para destino
copy_string:
    ; Entrada: ESI = origem, EDI = destino
    ; Saida: Nenhuma
    copy_loop:
        mov al, [esi]
        cmp al, 0
        je copy_done
        mov [edi], al
        inc esi
        inc edi
        jmp copy_loop
    copy_done:
        ret
