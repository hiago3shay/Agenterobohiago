# Agenterobohiago
Trabalho Robô IA

class AgenteRobo:
 def __init__(self):
     self.energia = 100
     self.bolsa = 0
     self.localizacao = [0, 0]
     self.objetivo_alcancado = False
     self.direcoes = {'Norte': (-1, 0), 'Sul': (1, 0), 'Leste': (0, 1), 'Oeste': (0, -1)}
     self.ambiente = [['A', 'B', 'C', 'D'],
                     ['E', 'F', 'G', 'H'],
                     ['I', 'J', 'K', 'L'],
                     ['M', 'N', 'O', 'P']]
 
 def aspirar_sujeira(self):
     linha, coluna = self.localizacao
     local_atual = self.ambiente[linha][coluna]
     self.ambiente[linha][coluna] = ' '
 
     self.bolsa += 1
     self.energia -= 1
     print("Limpando sujeira")
 
 def mover(self, direcao):
     linha, coluna = self.localizacao
     deslocamento = self.direcoes[direcao]
     nova_linha = linha + deslocamento[0]
     nova_coluna = coluna + deslocamento[1]
 
     if self.validar_localizacao(nova_linha, nova_coluna):
         self.localizacao = [nova_linha, nova_coluna]
         self.energia -= 1
 
 def validar_localizacao(self, linha, coluna):
     return 0 <= linha < 4 and 0 <= coluna < 4
 
 def voltar_para_casa(self):
     while self.localizacao != [0, 0]:
         self.mover(self.determinar_direcao_de_volta())
       
 def verificar_objetivo(self):
         if self.bolsa >= 10:
             self.bolsa = 0
             self.objetivo_alcancado = True
 
 def determinar_direcao_de_volta(self):
     linha, coluna = self.localizacao
     if linha > 0:
         return 'Norte'
     elif coluna > 0:
         return 'Oeste'
     else:
         return 'Sul'
 
 
 def limpar_quarto(self):
     while not self.objetivo_alcancado:
         if self.energia <= 0:
             print("Sem energia")
             break
 
         self.aspirar_sujeira()
         self.verificar_objetivo()
 
         if self.objetivo_alcancado:
             print("\nA Bolsa ficou cheia")
             self.voltar_para_casa()
             self.bolsa = 0
             print("\nBolsa esvaziada")
             print("\nLimpando novamente")
 
         if not self.objetivo_alcancado:
             self.mover(self.determinar_proxima_acao())
 
     print("\nO Quarto esta limpo!")
 
 def determinar_proxima_acao(self):
     import random
     direcoes_possiveis = list(self.direcoes.keys())
     return random.choice(direcoes_possiveis)
 
 
agente = AgenteRobo()
agente.limpar_quarto()

print(f"Localização: {agente.localizacao}, Energia:{agente.energia}, Bolsa: {agente.bolsa}")
