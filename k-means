#
# IAC 2023/2024 k-means
# 
# Grupo: 16
# Campus: Alameda
#
# Autores:
# 109685, Joao Sergio Abreu Viegas
# 110210, Tomas Ribeiro Lopes
# 103479, Afonso Matos
#
# Tecnico/ULisboa


# ALGUMA INFORMACAO ADICIONAL PARA CADA GRUPO:
# - A "LED matrix" deve ter um tamanho de 32 x 32
# - O input e' definido na seccao .data. 
# - Abaixo propomos alguns inputs possiveis. Para usar um dos inputs propostos, basta descomentar 
#   esse e comentar os restantes.
# - Encorajamos cada grupo a inventar e experimentar outros inputs.
# - Os vetores points e centroids estao na forma x0, y0, x1, y1, ...


# Variaveis em memoria
.data

#Input A - linha inclinada
#n_points:    .word 9
#points:      .word 0,0, 1,1, 2,2, 3,3, 4,4, 5,5, 6,6, 7,7 8,8

#Input B - Cruz
#n_points:    .word 5
#points:     .word 4,2, 5,1, 5,2, 5,3 6,2

#Input C
#n_points:    .word 23
#points: .word 0,0, 0,1, 0,2, 1,0, 1,1, 1,2, 1,3, 2,0, 2,1, 5,3, 6,2, 6,3, 6,4, 7,2, 7,3, 6,8, 6,9, 7,8, 8,7, 8,8, 8,9, 9,7, 9,8

#Input D
n_points:    .word 30
points:      .word 16, 1, 17, 2, 18, 6, 20, 3, 21, 1, 17, 4, 21, 7, 16, 4, 21, 6, 19, 6, 4, 24, 6, 24, 8, 23, 6, 26, 6, 26, 6, 23, 8, 25, 7, 26, 7, 20, 4, 21, 4, 10, 2, 10, 3, 11, 2, 12, 4, 13, 4, 9, 4, 9, 3, 8, 0, 10, 4, 10

#Input D4
#n_points:    .word 35
#points:      .word 16, 1, 17, 2, 18, 6, 20, 3, 21, 1, 17, 4, 21, 7, 16, 4, 21, 6, 19, 6, 4, 24, 6, 24, 8, 23, 6, 26, 6, 26, 6, 23, 8, 25, 7, 26, 7, 20, 4, 21, 4, 10, 2, 10, 3, 11, 2, 12, 4, 13, 4, 9, 4, 9, 3, 8, 0, 10, 4, 10, 20,20, 20,23, 20, 26, 20, 27, 29, 24


# Valores de centroids e k a usar na 1a parte do projeto:
#centroids:   .word 0,0
#k:           .word 1

# Valores de centroids, k e L a usar na 2a parte do prejeto:
centroids:   .word 0,0, 10,0, 0,10
k:           .word 3
L:           .word 10

# Abaixo devem ser declarados o vetor clusters (2a parte) e outras estruturas de dados
# que o grupo considere necessarias para a solucao:
#clusters:
    
    ## OPTIMIZATION
    # Apenas declaramos um unico vetor para controlar a distribuicao de pontos
    # pelos clusters, no qual e' guardado o indice [0,k] do centroid mais proximo 
    # sendo assim bastante eficiente em termos de memoria, necessitando apenas percorrer
    # o vetor input multiplas vezes, atualizando o cluster_index conforme.
    # Esta otimizacao tambem permitiu obter um codigo mais sucinto.
    
cluster_index: .word 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0, 0,0

#variaveis

random_dif: .word 0

#constantes:
    
.equ        multiplicando1 75
.equ        incremento1    74
.equ        multiplicando2 1664525
.equ        incremento2    1013904223
.equ        multiplicando3 22695477
.equ        incremento3    1


#Definicoes de cores a usar no projeto 

colors:      .word 0xff0000, 0x00ff00, 0x0000ff, 0x00fff00  # Cores dos pontos do cluster 0, 1, 2, etc.

.equ         black      0
.equ         white      0xffffff

# Codigo
 
.text
    # Chama funcao principal da 1a parte do projeto
    #jal mainSingleCluster
    # Descomentar na 2a parte do projeto:
    jal mainKMeans
    
    #Termina o programa (chamando chamada sistema)
    li a7, 10
    ecall
    
### printPoint
# Pinta o ponto (x,y) na LED matrix com a cor passada por argumento
# Nota: a implementacao desta funcao ja' e' fornecida pelos docentes
# E' uma funcao auxiliar que deve ser chamada pelas funcoes seguintes que pintam a LED matrix.
# Argumentos:
# a0: x
# a1: y
# a2: cor

printPoint:
    li a3, LED_MATRIX_0_HEIGHT
    sub a1, a3, a1
    addi a1, a1, -1
    li a3, LED_MATRIX_0_WIDTH
    mul a3, a3, a1
    add a3, a3, a0
    slli a3, a3, 2
    li a0, LED_MATRIX_0_BASE
    add a3, a3, a0   # addr
    sw a2, 0(a3)
    jr ra
    

### cleanScreen
# Limpa todos os pontos do ecra
# Argumentos: nenhum
# Retorno: nenhum

cleanScreen:
    ## OPTIMIZATION
    # Primeiramente percorriamos todos os x's e y's de [0 ,32] em dois ciclos,
    # obtendo uma funcao de complexidade O(n^2), mas muito demorada na sua execucao, 
    # com n^2 chamadas do printPoint. Apos compreender como a led matrix funciona, 
    # mantivemos a mesma complexidade apenas iterando sobre o LED_MATRIX_0_BASE diretamente,
    # bastando aumentar o offset para cada led, atingindo assim uma funcao muito mais rapida.
    
    li t0, LED_MATRIX_0_BASE # Endereco do vetor de LED's
    li t1, white # Cor do fundo
    li t2, 4096 # 4*32*32 numero maximo do offset dos registos da led matrix
    li t3, 0 # i = 0
    
    loopCleanScreen:
        add t5, t0, t3 # Adiciona o offset ao led_matrix_base
        sw t1, 0(t5) # Guarda com a cor branca
        addi t3, t3, 4 # i++ (offset de 4 bytes seguinte)
        blt t3, t2, loopCleanScreen # while i < 4*32*32
        
    jr ra

    
### printClusters
# Pinta os agrupamentos na LED matrix com a cor correspondente.
# Argumentos: nenhum
# Retorno: nenhum

printClusters:
        la s3, colors # Vetor de cores
        lw s1, k
        
        li s2, 0 # i = 0
        loopPrintClusters1:
            la, t0, points
            lw t1, n_points
            la s0, cluster_index
            
            lw a2, 0(s3) # Cor
            li t2, 0 # j = 0
            loopPrintClusters2:
                add t3, zero, t2 # t3 = j
                slli t6, t3, 2 # i*4 (avancar 1 word no index)
                slli t3, t3, 3 # i*8 (avancar 2 words no points)
                add t4, t0, t3 # points[i]
                add t5, s0, t6 # cluster_index[i]
                
                lw t6 ,0(t5) # cluster_index
            
                bne t6, s2, repetir # if index != j
            
                lw a0, 0(t4) # Load (x,_)
                lw a1, 4(t4) # Load (_,y)
                
                addi sp, sp, -44
                sw t0, 0(sp)
                sw t1, 4(sp)
                sw t2, 8(sp)
                sw t3, 12(sp)
                sw s0, 16(sp)
                sw s1, 20(sp)
                sw s2, 24(sp)
                sw a0, 28(sp)
                sw a1, 32(sp)
                sw a2, 36(sp)
                sw ra, 40(sp)
                jal printPoint # Pinta o ponto
                lw ra, 40(sp)
                lw a2, 36(sp)
                lw a1, 32(sp)
                lw a0, 28(sp)
                lw s2, 24(sp)
                lw s1, 20(sp)
                lw s0, 16(sp)
                lw t3, 12(sp)
                lw t2, 8(sp)
                lw t1, 4(sp)
                lw t0, 0(sp)
                addi sp, sp, 44
                
                repetir:
                    addi t2, t2, 1 # j++
                    blt t2, t1, loopPrintClusters2 # while j < n_points
                    
            addi s2, s2, 1 # i++
            addi s3, s3, 4 # colors[i++] proxima cor para o proximo cluster
            blt s2, s1, loopPrintClusters1 # while i < k
    
    fim:
        li s0, 0 # Preservar estado inicial da funcao
        li s1, 0
        li s2, 0
        li s3, 0
        
        jr ra

### printCentroids
# Pinta os centroides na LED matrix
# Nota: deve ser usada a cor preta (black) para todos os centroides
# Argumentos: nenhum
# Retorno: nenhum

printCentroids:
    la t0, centroids
    li a2, black # Cor do centroid
    li t2, 0 # i = 0
    lw s0, k
    
    addi sp, sp, -4 # Guardar ra antes do loop
    sw ra, 0(sp)
        
    print:  
        add t3, zero, t2 # t3 = i
        slli t3, t3, 3 # i*8
        add t4, t0, t3 # centroids[i]
        lw a0, 0(t4) # (x,_)
        lw a1, 4(t4) # (_,y)
        
        addi sp, sp, -16
        sw t0, 0(sp)
        sw t2, 4(sp)
        sw a2, 8(sp)
        sw s0, 12(sp) 
        jal printPoint # Pinta o centroid
        lw s0, 12(sp)
        lw a2, 8(sp)
        lw t2, 4(sp)
        lw t0, 0(sp)
        addi sp, sp, 16
    
        addi t2, t2, 1 # i++
        blt t2, s0, print # while i < k volta ao loop
    
    lw ra, 0(sp) # Restore do ra
    addi sp, sp, 4
    
    li s0, 0 # Preservar estado inicial da funcao
    
    jr ra

### calculateCentroids
# Calcula os k centroides, a partir da distribuicao atual de pontos
# associados a cada agrupamento (cluster)
# Argumentos: nenhum
# Retorno: nenhum

calculateCentroids:
        lw s1, k
        la s9, centroids
        li s2, 0 # i = 0
        
        loopCalculateCentroids1:
            la t0, points
            lw t1, n_points
            la s0, cluster_index
            li s5, 0 # Reset aos acumuladores
            li s3, 0
            li s4, 0
            li t2, 0 # j = 0
            loopCalculateCentroids2:
                add t3, zero, t2 # t3 = j
                slli t6, t3, 2 # i*4 (avancar 1 word no index)
                slli t3, t3, 3 # i*8 (avancar 2 words no points)
                add t4, t0, t3 # points[i]
                add t5, s0, t6 # cluster_index[i]
                
                lw t6 ,0(t5) # cluster_index
            
                bne t6, s2, repetirCalculateCentroids # if index != j
            
                lw a0, 0(t4) # Load (x,_)
                lw a1, 4(t4) # Load (_,y)
                
                add s3, s3, a0 # Somar (x,_)
                add s4, s4, a1 # Somar (_,y)
                
                addi s5, s5, 1 # Numero de pontos no cluster
                
                repetirCalculateCentroids:
                    addi t2, t2, 1 # j++
                    blt t2, t1, loopCalculateCentroids2 # while j < n_points
             
            beqz s5, proximo # If n_cluster == 0 
                    
            div a0, s3, s5 # Soma x's / n_cluster
            div a1, s4, s5 # Soma y's / n_cluster
            
            lw s6, 0(s9) # (x,_) centroid
            lw s7, 4(s9) # (_,y) centroid
        
            bne s6, a0, store
            addi s8, s8, 1 # Contador de coordenadas que nao foram alteradas
            bne s7, a1, store
            addi s8, s8, 1
            j proximo
            
            store:
                sw a0, 0(s9) # Store no  centroid
                sw a1, 4(s9)
           
            proximo:
                addi s9, s9, 8 # Proximo centroid   
                addi s2, s2, 1 # i++
                blt s2, s1, loopCalculateCentroids1
                
         # Verificacao de termino do programa
         # Se todos os centroids se mantiverem inalterados, termina
         
         verificacaoFinal:
             slli t1, s1 1 # Numero total de coordenadas dos centroids (k*2)
             beq s8, t1, fimPrograma
    
        li s0, 0 # Preservar estado inicial da funcao
        li s1, 0
        li s2, 0
        li s3, 0
        li s4, 0
        li s5, 0
        li s6, 0
        li s7, 0
        li s8, 0
        li s9, 0
        
        jr ra
        
    fimPrograma:
        addi sp, sp, -4
        sw ra, 0(sp)
        jal printCentroids # Certificar que os centroids estao printados
        lw ra, 0(sp)
        addi sp, sp, 4
        
        li a0, 130 # Codigo de exit (terminated by control)
        li a7, 93 # Exit2 para discernir da saida normal
        ecall
        


### mainSingleCluster
# Funcao principal da 1a parte do projeto.
# Argumentos: nenhum
# Retorno: nenhum

mainSingleCluster:

    #1. Coloca k=1 (caso nao esteja a 1)
    la t1, k # Saved durante todo o programa
    lw s0, 0(t1)
    li t0, 1
    bne s0, t0, k1 # Se k != 1
    j skip_k1
    k1:
        sw t0, 0(t1) # k = 1
skip_k1:
    
    #2. cleanScreen    
    addi sp, sp, -4
    sw ra, 0(sp)
    jal cleanScreen
    
    #3. printClusters    
    jal printClusters
    
    #4. calculateCentroids    
    jal calculateCentroids
    
    #5. printCentroids
    jal printCentroids
    lw ra, 0(sp)
    addi sp, sp, 4
    
    #6. Termina
    jr ra



### manhattanDistance
# Calcula a distancia de Manhattan entre (x0,y0) e (x1,y1)
# Argumentos:
# a0, a1: x0, y0
# a2, a3: x1, y1
# Retorno:
# a0: distance

manhattanDistance:
    sub a0, a0, a2 # x0 - x1
    sub a1, a1, a3 # y0 - y1
    
    bge a0, zero, modulo2 # If x > 0
    neg a0, a0 # else x = |x|
    
    modulo2:
        bge a1, zero, retorno # If y > 0
        neg a1, a1 # else y = |y|
    
    retorno:
        add a0, a0, a1 # |x| + |y|
    
    jr ra


### nearestCluster
# Determina o centroide mais perto de um dado ponto (x,y).
# Argumentos:
# a0, a1: (x, y) point
# Retorno:
# a0: cluster index

nearestCluster:
    la t1, centroids
    mv t2, t1 # Guarda o estado inicial do vetor
    
    li t3, 0 # Contador para o indice dos vetores
    li t4, 0 # i = 0
    lw s0, k
    
    loopNearestCluster:
        slli t5, t4, 3 # i*8
        add t2, t1, t5 # centroids[i]
        lw a2 ,0(t2) # (x,_)
        lw a3 ,4(t2) # (_,y)
    
        addi sp, sp, -12 # Guardar o ponto no stack
        sw ra, 0(sp)
        sw a0, 4(sp)
        sw a1, 8(sp)
        jal manhattanDistance
    
        beqz s9, primeira # Se for a 1a distancia
        bgtz s9, segundas
    
        primeira:
            mv s9, a0 # Guardar a 1a distancia num Saved
            j continuar
        
        segundas:
            bge a0, s9, continuar # So mudar se a0 < s3
            
            mv s9, a0 # Atualiza a menor distancia
            mv t3, t4 # Coloca o indice do vetor com a menor distancia (atual)
    
        continuar:       
            addi t4, t4, 1 # i++
        
            lw a1, 8(sp) # Restore ao ponto do stack
            lw a0, 4(sp)
            lw ra, 0(sp)
            addi sp, sp, 12
        
            blt t4, s0, loopNearestCluster # while i < k

    mv a0, t3 # Coloca o indice do vetor no a0 (retorno)
    li s3, 0 # Preservar o estado inicial da funcao
    li s0, 0
    li s9, 0
    
    jr ra

# ----------------------- Funcoes 2a Parte -----------------------

### random
# Gera um numero pseudo-aleatorio menor do que 32.
# Argumentos: nenhum
# Retorno:
#a0: random [0,31]

random:
    # Salvar registros temporarios na pilha
    addi sp, sp, -12
    sw t0, 0(sp)
    sw t1, 4(sp)
    sw t2, 8(sp)
    
    li t0, LED_MATRIX_0_WIDTH  # Tamanho do matriz
    
    # Estes pr�ximos labels t�m como objetivo
    # modificar o incremento e multiplicando
    # para quando o random for chamado em momentos muito proximos
    # evitar com que o valor de retorno seja igual
    lw t1, random_dif
    
    beqz t1, randomb2
    bgtz t1, randomb3
    
    randomb1:
        addi t1, t1, 1
        la t2, random_dif
        sw t1, 0(t2)
        
        li t1, multiplicando1
        li t2, incremento1
        
        j cong_linear
    
    randomb2:
        addi t1, t1, 1
        la t2, random_dif
        sw t1, 0(t2)
        
        li t1, multiplicando2
        li t2, incremento2
        
        j cong_linear
        
    randomb3:
        li t1, -1
        la t2, random_dif
        sw t1, 0(t2)

        li t1, multiplicando3
        li t2, incremento3
    
    cong_linear:
        li a7, 30 # Get time
        ecall
    
        mul a0, a0, t1  # a0 * mult
        add a0, a0, t2  # a0 * mult + incr
    
        rem a0, a0, t0 # mod(a0, matrix size)

    bgez a0, fimRandom
    neg a0, a0       # Se a0 < 0, torna positivo

    fimRandom:
        lw t0, 0(sp)
        lw t1, 4(sp)
        lw t2, 8(sp)
        addi sp, sp, 12
        jr ra


### createCentroids
# Gera k pontos pseudo-aleatorios para os centroids iniciais.
# Argumentos: nenhum
# Retorno: nenhum

createCentroids:
    la t0, centroids
    lw t1, k
    li t2, 0 # i = 0
    
    addi sp,sp, -4
    sw ra, 0(sp)
    
    blt t2, t1, criar  # while i < n_centroids (k)
    
    criar:
        add t3, zero, t2 # t3 = i
        slli t3, t3, 3 # i*8
        add t4, t0, t3 # centroids[i]
        lw t5, 0(t4) # (x,_)
        lw t6, 4(t4) # (_,y)
        
        jal random # Gerar random (x,_)
        
        sw a0, 0(t4) # Store (x,_)
        
        jal random # Gerar random (_,y)
        
        sw a0, 4(t4) # Store (_,y)
        
        addi t2, t2, 1 # i++
        
        blt t2, t1, criar # while i < n_centroids
        
    lw ra, 0(sp)
    addi sp, sp, 4
    
    jr ra


### calculateClusters
# Cria os k clusters, a partir da distribuicao atual de pontos e associa-os a cada agrupamento (cluster)
# Argumentos: nenhum
# Retorno: nenhum

calculateClusters:
    la t0, points # Vetor com os pontos
    lw t1, n_points # Tamanho do vetor
    li t2, 0 # i = 0
    la s0, cluster_index # Endereco do vetor com os indices para cada ponto
        
    loopCalculateClusters:
        add t3, zero, t2 # t3 = i
        slli t6, t3, 2 # i*4 (avancar 1 word no index)
        slli t3, t3, 3 # i*8 (avancar 2 words no points)
        add t4, t0, t3 # points[i]
        add t5, s0, t6 # cluster_index[i]
        
        lw a0, 0(t4) # (x,_)
        lw a1, 4(t4) # (_,y)
        
        addi sp, sp, -24
        sw ra, 0(sp)
        sw t0, 4(sp) # Preservar o ponto
        sw t1, 8(sp)
        sw t2, 12(sp) # Preservar o n_points
        sw t5, 16(sp) # Preservar o i
        sw s0, 20(sp) # Preservar os enderecos dos vetores
        jal nearestCluster # Calcular o indice centroid mais proximo
        lw s0, 20(sp)
        lw t5, 16(sp)
        lw t2, 12(sp)
        lw t1, 8(sp)
        lw t0, 4(sp)
        lw ra, 0(sp)
        addi sp, sp, 24
        
        sw a0, 0(t5) # Guardar o indice do vetor no cluster_index
        
        addi t2, t2, 1 # i++
        blt t2, t1, loopCalculateClusters # while i < n_points
               
    li s0, 0 # Preservar estado inicial da funcao
                
    jr ra

### mainKMeans
# Executa o algoritmo *k-means*.
# Argumentos: nenhum
# Retorno: nenhum

mainKMeans:  
    
    la t0, L # Endereco do L
    lw t1, 0(t0) # L
    beqz t1, termina # if L = 0
    
    #1. createCentroids
    addi sp, sp, -4
    sw ra, 0(sp)
    jal createCentroids 
    
    loopKmeans:
        
        #2. cleanScreen
        jal cleanScreen
        
        #3. printCentroids
        jal printCentroids   
    
        #4. calculateClusters
        jal calculateClusters
    
        #5. printClusters    
        jal printClusters
  
        #6. calculateCentroids
        jal calculateCentroids
    
        #7. loop
        la t0, L # Endereco do L
        lw t1, 0(t0) # L
        addi t1, t1, -1 # L--
        sw t1, 0(t0) # Atualizar o L
        bgtz t1, loopKmeans # while L > 0
    
    lw ra, 0(sp) # Restore ra do stack
    addi sp, sp, 4
    
    #8. Termina
    termina:    
        jr ra
