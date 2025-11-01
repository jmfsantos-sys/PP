markdown
# Multiplicação de Matrizes (DGEMM) com MPI

Projeto 2

> Disciplina: DEC107 — Processamento Paralelo
> 
> Curso: Bacharelado em Ciência da Computação
> 
> Autores: João Manoel Fidelis Santos e Maria Eduarda Guedes Alves
> 
> Data: 13/10/2025

## Arquivos

> main.c: Contém o programa principal (driver) que executa os testes MPI, OpenMP, BLAS e sequencial, além de orquestrar a validação de corretude.

> funcoes.h: Arquivo de cabeçalho com as declarações de funções, tipo func_matriz, e inclusão de todas as bibliotecas necessárias (MPI, OpenMP, BLAS, etc.).

> funcoes.c: Implementação de todas as funções de multiplicação (DGEMM), funções auxiliares (alocação, impressão) e a função valida_resultado.

> Makefile.mak: Arquivo de compilação que constrói o executável híbrido main.
 generate_plots.py: Script Python para analisar os logs (.txt) e gerar os gráficos de desempenho (.png).

## Objetivos do Projeto

> Implementar uma versão paralela distribuída da DGEMM utilizando MPI, explorando a comunicação entre processos distintos via troca de mensagens.

> Avaliar o desempenho obtido em comparação com:
    1. A versão sequencial (referência de desempenho e corretude).
    2. A versão paralela com OpenMP (comparação de speedup e eficiência).

> Incluir testes de corretude e análise de precisão numérica, ausentes no Projeto 1.

## Instalação

O projeto foi desenvolvido para um ambiente Linux (Ubuntu, via WSL) e requer as seguintes bibliotecas:

1. Compiladores e MPI:
    
    sudo apt update
    sudo apt upgrade -y
    sudo apt install -y build-essential
    sudo apt install -y openmpi-bin libopenmpi-dev
    
2. Biblioteca de Álgebra Linear (BLAS):
    
    # O projeto usa OpenBLAS para a comparação de desempenho
    sudo apt install -y libopenblas-dev
    
3. Bibliotecas Python (para gráficos):
    
    # Instala o Python e o gerenciador de pacotes
    sudo apt install -y python3 python3-pip

    # Instala os pacotes necessários usando o gerenciador do sistema (Recomendado para ambientes WSL/Ubuntu modernos)
    sudo apt install -y python3-pandas python3-matplotlib python3-numpy
    

## Compilar, Executar e Analisar

O fluxo de trabalho completo é dividido em três etapas:

### 1. Compilar (Gerar o executável main)

Use o comando make:

# A flag -f é usada porque o arquivo se chama "Makefile.mak"
make -f Makefile.mak

Isso irá compilar main.c e funcoes.c e criar o executável main.

### 2. Executar (Gerar o Log de Teste)

Execute o programa compilado usando mpirun.

# Usamos 6 processos MPI para corresponder ao número de núcleos físicos do hardware (AMD Ryzen 5 5600G)
mpirun -np 6 ./main

### 3. Analisar (Gerar os Gráficos)

Após a execução, use o script Python para analisar os logs e gerar os gráficos.

python3 generate_plots.py

O script irá processar automaticamente os arquivos teste6_par_openMP.txt (se existir) e teste7_par_mpi.txt, salvando todos os gráficos .png nas suas respectivas pastas (plots_teste6_par_openMP/ e plots_teste7_par_mpi/).
