

class Mago():

    def __init__(self,nome='mago genérico',vida_max=100):
        self.vida_max = vida_max
        self.vida = vida_max
        self.nome = nome
        self.armas = {}
        self.armas['bola de fogo'] = {'valor':10,'tipo':'fogo'}
        self.armas['soco'] = {'valor':2,'tipo':'impacto'}
        self.armas['adaga'] = {'valor':5,'tipo':'lamina'}
        self.armas['espada'] = {'valor':10,'tipo':'lamina'}
        self.arma = 'bola de fogo'



    def tomar_dano(self,dano):
        valor_dano = dano['valor']
        if dano['tipo'] == 'fogo':
            valor_dano =  valor_dano - 9 
            if valor_dano < 0:
               valor_dano = 0
        if (self.vida > valor_dano):
            self.vida -= valor_dano
            print(self.nome + ' tomou '+str(valor_dano)+' de dano de '+ dano['tipo']  +' mas continua de pé')
            print('agora tem '+ str(self.vida)+' de vida')
            
        else:
            if self.vida != 0:
               print(self.nome + ' nao resistiu e caiu em batalha!')
            if self.vida == 0:
               print('pare de atacar o cadaver de '+ self.nome)
            self.vida = 0
    
    def selecionar_arma(self,nome_arma):
        if nome_arma in self.armas:
            self.arma = nome_arma

    def atacar(self):
        dano = self.armas[self.arma]
        self.adversario.tomar_dano(dano)

    def lutar_com(self,adversario):
          self.adversario = adversario

          
class Lutador():

    def __init__(self,nome='mago genérico',vida_max=100):
        self.vida_max = vida_max
        self.vida = vida_max
        self.nome = nome
        self.armas = {}
        self.armas['bola de fogo'] = {'valor':10,'tipo':'fogo'}
        self.armas['soco'] = {'valor':2,'tipo':'impacto'}
        self.armas['adaga'] = {'valor':7,'tipo':'lamina'}
        self.armas['espada'] = {'valor':10,'tipo':'lamina'}
        self.arma = 'espada'



    def tomar_dano(self,dano):
        valor_dano = dano['valor']
        if dano['tipo'] == 'impacto':
            valor_dano =  valor_dano - 1 
            if valor_dano < 0:
               valor_dano = 0
        if (self.vida > valor_dano):
            self.vida -= valor_dano
            print(self.nome + ' tomou '+str(valor_dano)+' de dano de '+ dano['tipo']  +' mas continua de pé')
            print('agora tem '+ str(self.vida)+' de vida')
            
        else:
            if self.vida != 0:
               print(self.nome + ' nao resistiu e caiu em batalha!')
            if self.vida == 0:
               print('pare de atacar o cadaver de '+ self.nome)
            self.vida = 0
    
    def selecionar_arma(self,nome_arma):
        if nome_arma in self.armas:
            self.arma = nome_arma

    def atacar(self):
        dano = self.armas[self.arma]
        self.adversario.tomar_dano(dano)

    def lutar_com(self,adversario):
          self.adversario = adversario

class Barbaro():

    def __init__(self,nome='mago genérico',vida_max=100):
        self.vida_max = vida_max
        self.vida = vida_max
        self.nome = nome
        self.armas = {}
        self.armas['bola de fogo'] = {'valor':0,'tipo':'fogo'}
        self.armas['soco'] = {'valor':2,'tipo':'impacto'}
        self.armas['adaga'] = {'valor':5,'tipo':'lamina'}
        self.armas['espada'] = {'valor':10,'tipo':'lamina'}
        self.arma = 'espada'


    def tomar_dano(self,dano):#barbaro dá dano dobrado se machucado
        valor_dano = dano['valor']
        
        if (self.vida > valor_dano):
            self.vida -= valor_dano
            print(self.nome + ' tomou '+str(valor_dano)+' de dano de '+ dano['tipo']  +' mas continua de pé')
            print('agora tem '+ str(self.vida)+' de vida')
        
        else:
            if self.vida != 0:
               print(self.nome + ' nao resistiu e caiu em batalha!')
            if self.vida == 0:
               print('pare de atacar o cadaver de '+ self.nome)
            self.vida = 0
    
    def selecionar_arma(self,nome_arma):
        if nome_arma in self.armas:
            self.arma = nome_arma

    def atacar(self):
        dano = self.armas[self.arma]
        self.adversario.tomar_dano(dano)

    def lutar_com(self,adversario):
          self.adversario = adversario


import unittest
class TesteLutas(unittest.TestCase):
    


    def test_01_ataque_magia(self):
       merlin = Mago('merlin',120)
       morgana = Mago('morgana')
       merlin.lutar_com(morgana)
       merlin.atacar()#merlin atacou com bola de fogo por padrao. Morgana resiste 9 
       #de dano e toma só um
       self.assertEqual(morgana.vida,99)

    def test_02_ataque_soco(self):
       merlin = Mago('merlin',120)
       morgana = Mago('morgana')
       merlin.selecionar_arma('soco')
       merlin.lutar_com(morgana)
       merlin.atacar()
       self.assertEqual(morgana.vida,98)
    
    def test_03_ataque_ate_a_morte(self):
       merlin = Mago('merlin',120)
       morgana = Mago('morgana',20)
       merlin.selecionar_arma('adaga')
       merlin.lutar_com(morgana)
       merlin.atacar()
       self.assertEqual(morgana.vida,15)
       merlin.atacar()
       self.assertEqual(morgana.vida,10)
       merlin.atacar()
       self.assertEqual(morgana.vida,5)
       merlin.selecionar_arma('soco')
       merlin.atacar()
       self.assertEqual(morgana.vida,3)
       merlin.atacar()
       self.assertEqual(morgana.vida,1)
       merlin.atacar()
       self.assertEqual(morgana.vida,0)
       merlin.atacar()
       self.assertEqual(morgana.vida,0)

    def test_04_mago_contra_lutador_tipos_de_dano(self):
       merlin = Mago('merlin',120)
       arthur = Lutador('arthur',150)
       merlin.lutar_com(arthur)
       merlin.atacar()
       self.assertEqual(arthur.vida,140)
       merlin.selecionar_arma('soco')
       merlin.atacar()
       self.assertEqual(arthur.vida,139)
       merlin.selecionar_arma('adaga')
       merlin.atacar()
       self.assertEqual(arthur.vida,134)

    def test_05_lutador_prefere_espada(self):
       arthur = Lutador('arthur',150)
       self.assertEqual(arthur.arma,'espada')

    def test_06_lutador_contra_mago_tipos_de_dano(self):
       merlin = Mago('merlin',120)
       arthur = Lutador('arthur',150)
       arthur.lutar_com( merlin)
       arthur.atacar()
       self.assertEqual(merlin.vida,110)
       arthur.selecionar_arma('bola de fogo')
       arthur.atacar()
       self.assertEqual(merlin.vida,109)
       arthur.selecionar_arma('adaga')
       arthur.atacar()
       self.assertEqual(merlin.vida,102)

    def test_07_mago_contra_barbaro_tipos_de_dano(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       merlin.lutar_com(conan)
       merlin.atacar()
       self.assertEqual(conan.vida,190)
       merlin.selecionar_arma('soco')
       merlin.atacar()
       self.assertEqual(conan.vida,188)
       merlin.selecionar_arma('adaga')
       merlin.atacar()
       self.assertEqual(conan.vida,183)

    def test_08_barbaro_sem_dano_contra_mago(self):#Barbaro sem dano toma dano integralmente!!!
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)#'''''''''''''
       conan.lutar_com(merlin)
       conan.atacar()
       self.assertEqual(merlin.vida,110)#'''''''''''''''''''''''''''
       conan.selecionar_arma('adaga')
       conan.atacar()
       self.assertEqual(merlin.vida,103)
       conan.selecionar_arma('soco')
       conan.atacar()
       self.assertEqual(merlin.vida,101)
       conan.selecionar_arma('bola de fogo')
       conan.atacar()
       self.assertEqual(merlin.vida,101)

    def test_09_barbaro_com_dano_contra_mago(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       merlin.lutar_com(conan)
       merlin.atacar()
       conan.lutar_com(merlin)
       conan.atacar()
       self.assertEqual(merlin.vida,100)
       conan.selecionar_arma('adaga')
       conan.atacar()
       self.assertEqual(merlin.vida,86)
       conan.selecionar_arma('soco')
       conan.atacar()
       self.assertEqual(merlin.vida,82)
    
    def test_10_barbaro_com_dano_contra_mago_2(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       merlin.lutar_com(conan)
       merlin.atacar() #barbaro dessa vez sofre 2 ataques
       conan.lutar_com(merlin)
       conan.atacar()
       self.assertEqual(merlin.vida,100)
       merlin.atacar() #segundo ataque que o barbaro sofre
       conan.atacar()
       self.assertEqual(merlin.vida,80) #o dano da espada nao pode dobrar 2 vezes

    
    def test_11_lutador_atacando_com_fogo(self):
       merlin = Mago('merlin',120)
       arthur = Lutador('arthur',150)
       arthur.lutar_com( merlin)
       arthur.selecionar_arma('bola de fogo')
       arthur.atacar()
       self.assertEqual(arthur.vida,130)
    
    def test_12_barbaro_atacando_com_fogo(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       conan.lutar_com( merlin)
       conan.selecionar_arma('bola de fogo')
       conan.atacar()
       self.assertEqual(conan.vida,180)
       conan.atacar()
       self.assertEqual(conan.vida,160)
       self.assertEqual(merlin.vida,120)
    
    def test_13_mago_nao_usa_espada(self):
       merlin = Mago('merlin',120)
       arma_anterior = merlin.arma
       merlin.selecionar_arma('espada')
       arma_atual = merlin.arma
       self.assertEqual(arma_anterior,arma_atual)

    def test_14_curar(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       arthur= Lutador('Arthur',150)
       conan.lutar_com(merlin)
       arthur.lutar_com(conan)
       merlin.lutar_com(arthur)
       conan.atacar()
       arthur.atacar()
       merlin.atacar()
       self.assertTrue(conan.vida < 200)
       self.assertTrue(arthur.vida < 150)
       self.assertTrue(merlin.vida < 120)
       conan.curar()
       self.assertEqual(conan.vida,200)
       arthur.curar()
       self.assertEqual(arthur.vida,150)
       merlin.curar()
       self.assertEqual(merlin.vida,120)

    def test_15_barbaro_curado_da_menos_dano(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       conan.lutar_com(merlin)
       merlin.lutar_com(conan)
       merlin.atacar()
       conan.atacar()
       self.assertEqual(merlin.vida,100)
       conan.curar()
       conan.atacar()
       self.assertEqual(merlin.vida,90)

    def test_16_veneno(self):
       merlin = Mago('merlin',120)
       merlin.envenenar()
       conan = Barbaro('conan',200)
       merlin.lutar_com(conan)
       merlin.atacar()
       self.assertEqual(merlin.vida,110)#merlin tomou o dano do veneno
       merlin.atacar()
       self.assertEqual(merlin.vida,100)
    
    def test_17_antidoto(self):
       merlin = Mago('merlin',120)
       merlin.envenenar()
       conan = Barbaro('conan',200)
       merlin.lutar_com(conan)
       merlin.atacar()
       self.assertEqual(merlin.vida,110)#merlin tomou o dano do veneno
       merlin.atacar()
       self.assertEqual(merlin.vida,100)
       merlin.tomar_antidoto()#sem mais dano
       merlin.atacar()
       self.assertEqual(merlin.vida,100)
    
    def test_18_veneno_para_barbaro(self):
       merlin = Mago('merlin',120)
       conan = Barbaro('conan',200)
       conan.envenenar()
       conan.lutar_com(merlin)
       conan.atacar()
       self.assertEqual(conan.vida,200)#conan nao tomou o dano do veneno
       conan.atacar()
       self.assertEqual(conan.vida,200)#idem


def runTests():
            suite = unittest.defaultTestLoader.loadTestsFromTestCase(TesteLutas)
            unittest.TextTestRunner(verbosity=2,failfast=True).run(suite)



