# amostra cultural gabrriel
import os
import random
import sys
import time

# Configurações da animação
LARGURA = 80  # Número de colunas no terminal
ALTURA = 24  # Número de linhas no terminal
CARACTERES = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz@#$%"


def animacao_matrix():
    # Inicializa as posições iniciais de cada "gota" de texto
    colunas = [random.randint(-ALTURA, 0) for _ in range(LARGURA)]

    # Código para limpar o terminal dependendo do sistema operacional
    os.system("cls" if os.name == "nt" else "clear")

    try:
        while True:
            linha_atual = ""
            for x in range(LARGURA):
                # Se a gota passou do topo e ainda está na tela
                if colunas[x] >= 0 and colunas[x] < ALTURA:
                    # Escolhe um caractere aleatório
                    char = random.choice(CARACTERES)
                    # Adiciona a cor verde clássica usando códigos ANSI
                    linha_atual += f"\033[32m{char}\033[0m"
                else:
                    linha_atual += " "

                # Move a gota para baixo
                colunas[x] += 1

                # Se a gota saiu da tela, reinicia ela no topo aleatoriamente
                if colunas[x] >= ALTURA:
                    colunas[x] = random.randint(-5, 0)

            # Imprime a linha e move o cursor de volta para o início
            sys.stdout.write(linha_atual + "\n")
            sys.stdout.flush()

            # Controla a velocidade da animação (menor = mais rápido)
            time.sleep(0.05)

            # Move o cursor para o topo do terminal para sobrescrever o texto
            sys.stdout.write(f"\033[{ALTURA}A")

    except KeyboardInterrupt:
        # Fecha suavemente quando o usuário aperta Ctrl+C
        print("\nAnimação encerrada.")


if __name__ == "__main__":
    animacao_matrix()
