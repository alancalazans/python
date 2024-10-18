# Notas de Python 3

## PIP e VENV

## Instalando PIP e VENV

### Arch Linux

```bash
$ sudo pacman -S python-pip
```

### CentOS

```bash
$ sudo dnf install python3-pip python3-wheel
```

Para adicionalmente atualizar `setuptools`:

```bash
$ sudo dnf upgrade python3-setuptools
```

### Debian e Ubuntu

```bash
$ sudo apt update
$ sudo apt install python3-venv python3-pip
```

### Fedora

```bash
$ sudo dnf install python3-pip python3-wheel
```

### OpenSUSE

```bash
$ sudo zypper install python3-pip python3-setuptools python3-wheel
```

### Criando ambiente virtual

- **No Linux**

```bash
$ python3 -m venv myenv
```

> **Obs.:** `myenv` é o nome do ambiente virtual.

### Carregando ambiente virtual

- **No Linux**

```bash
$ source myenv/bin/activate
```

- **No Windows**

```powershell
C:\> myenv\Scripts\activate.bat
```

> **Obs.:** No Windows é necessário realizar um procedimento (uma única vez) para carregar o ambiente virtual:
>
> 1. Abra o powershell como administrador e insira este comando e tecle \<ENTER\>:
>
> ```powershell
> C:\> Set-ExecutionPolicy Unrestricted -Force
> ```

### Atualizando o PIP

- **No Linux**

```bash
(myenv) $ pip install --upgrade pip
```

>**Obs.:** Atualizando `pip` e `setuptools`
>
>```bash
>(myvenv) $ pip install -U pip setuptools
>```

- **No Windows** (atualiza `pip`, `setuptools` e `whell`)

```powershell
(myvenv) C:\> python.exe -m pip install -U pip setuptools wheel
```

**Checando a versão**

```bash
(myenv) $ pip --version
```

### Confirmando que esta no ambiente virtual:

> **Obs.:** A principio quando se observa, antes do prompt do console, entre parenteses, o nome do ambiente virtual isto indica que este esta carregado, entretando, ainda há os comandos abaixo:

- **No Linux**

```bash
(myenv) $ which python
```

- **No Windows**

```powershell
(myenv) C:\> where python
```

### Saindo do ambiente virtual

```bash
$ deactivate
```

### Instalando pacotes

**Neste exemplo é instalado o pacote que trata das requisições `http`**

```bash
(myenv) $ pip install requests
```

**Instalando versões específicas**

```bash
(myenv) $ pip install 'requests==2.18.4'
```

**Para instalar versões de pré-lançamento**

```bash
(myenv) $ pip install --pre requests
```

**Instalando extras**

```bash
(myenv) $ pip install 'requests[security]'
```

### Instalando a partir do código fonte

**Por exemplo entrando na pasta do fonte e instalando**

```bash
(myenv) $ cd google-auth
(myenv) $ pip install .
```

> Instalando código fonte em desenvolvimento (qualquer mudança no código fonte afetará o pacote instalado sem necessidade de reinstalação).
>
> ```bash
> (myenv) $ pip install --editable .
> ```

### Instalando de arquivos locais

```bash
(myenv) $ pip install requests-2.18.4.tar.gz
```

> Se você tiver um diretório contendo arquivos de vários pacotes, você pode dizer ao pip para procurar por pacotes lá e não usar o Python Package Index (pypi) de forma alguma:
>
> ```bash
> (myenv) $ pip install --no-index --find-links=/local/dir/requests
> ```

### Pacotes originário de url

```bash
(myenv) $ pip install --index-url http://index.example.com/simple/AlgumPacote
```

### Atualizando pacotes

```bash
(myenv) $ pip install --upgrade requests
```

### Usando arquivos de requisitos

Arquivos de requisitos são usados para a instalação de vários pacotes de uma só vez.

- Congelando (criando) o arquivo de requisitos:

```bash
(myenv) $ pip freeze > requirements.txt
```

- Agora instalando pacotes a partir de arquivo requirements.txt

```bash
(myenv) $ pip install -r requirements.txt
```

### Desinstalando pacotes

- Listando pacotes instalados:

```bash
(myenv) $ pip list
```

- Desinstalando um pacote:

```bash
(myenv) $ pip uninstall youtube-dl
```

- Desinstalando todos os pacotes:

```bash
(myenv) $ pip freeze | xargs pip uninstall -y
```

### Desinstalando dependências inutilizadas em Python com o pip

- O pacote `pip-check-reqs` varre todo o código fonte do nosso projeto buscando todas as importações presentes criando uma árvore de dependências e verifica a existência de dependências extras presentes no arquivo `requeriments.txt` e as mostrará caso existam.

- Instalando `pip-check-reqs`:

```bash
(myenv) $ pip install pip-check-reqs
```

- Agora para mostrar todos os pacotes extras

```bash
(myenv) $ pip-extra-reqs .
```

> **Obs.:**
>
> Ao invés do ponto pode vir o nome do `script.py`.
>
> A instrução listará os pacotes extras que podemos remover. Podemos criar um arquivo por exemplo `excluir.txt` com apenas os nomes dos pacotes para remover e executar o comando abaixo:
>
> ```bash
> (myenv) $ cat exclude.txt | xargs pip uninstall -y
> ```

### Removendo lista de bibliotecas

```bash
(myenv) $ pip freeze | grep -v "^-e"| xargs pip uninstall -y
```

### Pipreqs

varre os scripts do projeto em busca de pacotes de dependências necessárias ao projeto e gera um arquivo `requirements.txt` com estas dependências.

- Instalação do `pipreqs`

```bash
(myenv) $ pip install pipreqs
```

- Agora para criar o `requirements.txt` com as dependências:

```bash
(myenv) $ pipreqs .
```

> Quando se esta na pasta do projeto ou:
>
> ```bash
> (myenv) $ pipreqs PastaDoProjeto/
> ```

- Caso o arquivo `requirements.txt` já exista na pasta use o comando:

```bash
(myenv) $ pipreqs . --force
```

> Desta forma o arquivo `requirements.txt` será subscrito.

## Python

## Comentários e Strings

```python
# Este é um comentário de uma linha.
"""
Este é um comentário
de múltiplas linhas.
"""
texto = """
Aspas triplas
também são usadas
para string de
múltiplas linhas.
"""

print(texto)  # -> Saída:
              # Aspas triplas
              # também são usadas
              # para string de
              # múltiplas linhas.
```

```python
# Variáveis do tipo string:
course = 'Curso'
language = 'Python'

# -> Formatando a saída <-
# Variável `result` irá conter "Curso de Python":
result = f'{course} de {language}'
# ou
result = '{} de {}'.format(course, language)
print(result) # -> Curso de Python

# Outra forma de formatar saída:
print('{b}, {a}'.format(a=course, b=language)) # -> Python, Curso

# Todos os caracteres em maiúsculo:
print(result.upper()) # -> CURSO DE PYTHON

# Todos os caracteres em mínusculo:
print(result.lower()) # -> curso de python

# Indices dos elementos:
# 012345678901234
# |||||||||||||||
# Curso de Python

# -> Busca <-
# Imprimir o indice onde inicia a palavra `Python`:
print(result.find('Python')) # -> 9

# -> Substring <-
# A partir do indice zero imprimir 5 elementos:
print(result[0:5]) # -> Curso

# Invertendo string:
print(result[::-1]) # -> nohtyP ed osruC

# Qtde de letras 'o' na frase armazenda em `result`:
print(result.count('o')) # -> 2

# Substitui todos as letras `o` por `x`:
print(result.replace('o', 'x')) # -> Cursx de Pythxn

# Cria uma lista de elementos quebrando
# a frase nos espaços:
print(result.split(' ')) # -> ['Curso', 'de', 'Python']
```

## Listas

```python
# Criando uma lista
# Indices:    0      1    2     3
#             |      |    |     |
myList = ["Strings", 15, 15.6, True]
print(myList) # -> ["Strings", 15, 15.6, True]

# A partir do indice zero imprimir tres elementos:
print(myList[0:3]) # -> ['Strings', 15, 15.6]

# Acrescente ao final o número `6`:
myList.append(6)
print(myList) # -> ["Strings", 15, 15.6, True, 6]

# Insirindo a frase `outra string`
# na posição de indice 1:
myList.insert(1, "outra string")
# Indices:              0             1        2    3     4    5
#                       |             |        |    |     |    |
print(myList) # -> ['Strings', 'outra string', 15, 15.6, True, 6]

print(myList[1]) # -> outra string

# Remova o elemento `15` da lista
myList.remove(15)
print(myList) # -> ['Strings', 'outra string', 15.6, True, 6]

# Removendo último elemento da lista (`6`) e
# atribuindo a variável `lastValue`:
lastValue = myList.pop()

print(myList) # -> ['Strings', 'outra string', 15, 15.6, True]

# Variável `lastValue` contém o valor `6`:
print(lastValue) # -> 6

# Criando uma lista de números desordenada:
myList = [1,9,22,6,8,65,14,99]

# Ordenando a lista:
myList.sort()
print(myList) # -> [1, 6, 8, 9, 14, 22, 65, 99]

# Invertendo a ordem da lista:
myList.sort(reverse = True)
print(myList) # [99, 65, 22, 14, 9, 8, 6, 1]

# Criando uma nova lista `myListTwo` e com
# esta estender a primeira `myList`:
myListTwo = [22, 23]
myList.extend(myListTwo)
print(myList) # -> [99, 65, 22, 14, 9, 8, 6, 1, 22, 23]

# Método `append` é diferente do método `extend`
myList = [1, 9, 22, 6, 8, 65, 14, 99]
myList.append(myListTwo)
print(myList) # -> [1, 9, 22, 6, 8, 65, 14, 99, [22, 23]]
```

## Tuplas

Tuplas podem armazenar todo tipo de dados ***(inteiros, boleanos, strings, listas, outras tuplas)***. As tuplas são imutáveis.

```python
# Indices:  0   1   2   3   4   5   6   7   8   9
#           |   |   |   |   |   |   |   |   |   |
result  = ('O','l','á',' ','P','e','s','s','o','a')
print(result) # -> ('O','l','á',' ','P','e','s','s','o','a')

# A partir do indice zero imprimir 3 elementos:
print(result[0:3]) # -> ('O','l','á')

# A partir do indice zero imprimir 10 elementos:
print(result[0:10]) # -> ('O','l','á',' ','P','e','s','s','o','a')

# Indices: 0     1       2
#          |     |       |
myTuple = (1, "string", True)
print(myTuple) # -> (1, 'string', True)
print(myTuple[0]) # -> 1

# A partir do indice zero imprimir 2 elementos:
print(myTuple[0:2]) # -> (1, 'string')
```

> **Obs.:** Tuplas podem ser usadas para armazer valores que podem funcionar como constantes para, por exemplo, inicializar base de dados.

## Dicionários

Dicionários assim como as tuplas podem armazenar todo tipo de dados, entretanto,  os dicionários são mutáveis e os elementos não são acessados por indices mas por chaves.

```python
dicionario = {'a' : True, 5 : "Esta é uma string"}
print(dicionario) # -> {'a' : True, 5 : 'Esta é uma string'}

# A chave 'a' repetida retém o
# último valor a ela atribuído:
dicionario = {'a' : True, 5 : "Esta é uma string", 'a' : 100}
print(dicionario) # -> {'a': 100, 5: 'Esta é uma string'}

# Acrescentando novos pares (chave : valor):
dicionario['c'] = 'nova string'
print(dicionario) # -> saída:
                  # {'a': 100, 5: 'Esta é uma string',
                  #  'c': 'nova string'}

# Se a chave existe atualiza senão cria:
dicionario['a'] = False
print(dicionario) # -> saída:
                  # {'a': False, 5: 'Esta é uma string',
                  #  'c': 'nova string'}

# Obtendo valores do dicionário
print(dicionario['a']) # -> False

print(dicionario['z']) # Retorna um erro pois a
                       # chave 'z' não existe

print(dicionario.get('z', False)) # Definimos um valor padrão
                                  # caso a chave não exista
                                  # -> saída:
                                  # False

# Eliminando pares (chave : valor):
del dicionario[5]
print(dicionario) # -> {'a': False, 'c': 'nova string'}

# Obter todas as chaves:
chaves = dicionario.keys()
print(chaves) # -> dict_keys(['a', 'c'])

# Obter chaves e valores como lista:
chaves = list(dicionario.keys())
valores = list(dicionario.values())
print(chaves) # -> ['a', 'c']
print(valores) # -> [False, 'nova string']

# Obter chaves e valores como tupla:
chaves = tuple(dicionario.keys())
valores = tuple(dicionario.values())
print(chaves) # -> ('a', 'c')
print(valores) # -> (False, 'nova string')

# Acrescentando um dicionario em outro:
dicionarioDois = {'z' : 23, 'w' : 88}

# Poderiamos fazer:
# dicionario['z'] = dicionarioDois['z']
# dicionario['w'] = dicionarioDois['w']
# Mas a forma usual é:
dicionario.update(dicionarioDois)
print(dicionario) # -> saída:
                  # {'a': False, 'c': 'nova string', 'z': 23,
                  #  'w': 88}
```

## Operadores lógicos (and, or, not), curto-circuito e condicionais

1. Operadores Lógicos e Curto-Circuito

Python usa três operadores lógicos principais: and, or, e not.

a) and (E lógico):

- Retorna True se ambos os operandos forem True.
- Usa curto-circuito: se o primeiro operando for False, não avalia o segundo.

Exemplo:

```python
x = 5
y = 10
resultado = x > 0 and y < 20
print(resultado)  # True

# Curto-circuito
resultado = x < 0 and print("Isso não será executado")
print(resultado)  # False
```

b) or (OU lógico):

- Retorna True se pelo menos um dos operandos for True.
- Usa curto-circuito: se o primeiro operando for True, não avalia o segundo.

Exemplo:

```python
x = 5
y = 10
resultado = x > 10 or y < 20
print(resultado)  # True

# Curto-circuito
resultado = x > 0 or print("Isso não será executado")
print(resultado)  # True
```

c) not (NÃO lógico):

- Inverte o valor booleano do operando.

Exemplo:

```python
x = True
resultado = not x
print(resultado)  # False
```

1. Condicionais

Python usa as estruturas if, elif, e else para controle de fluxo condicional.

Sintaxe básica:

```python
if condição:
    # código se a condição for verdadeira
elif outra_condição:
    # código se a outra condição for verdadeira
else:
    # código se nenhuma das condições anteriores for verdadeira
```

Exemplo:

```python
idade = 18

if idade < 13:
    print("Criança")
elif idade < 18:
    print("Adolescente")
else:
    print("Adulto")
```

1. Combinando Operadores Lógicos e Condicionais

Você pode combinar operadores lógicos em condicionais para criar lógicas mais complexas:

```python
idade = 25
tem_carteira = True

if idade >= 18 and tem_carteira:
    print("Pode dirigir")
elif idade >= 18 and not tem_carteira:
    print("Precisa tirar a carteira")
else:
    print("Não pode dirigir")
```

1. Expressões Condicionais (Operador Ternário)

Python também suporta expressões condicionais em uma única linha:

```python
idade = 20
status = "Maior de idade" if idade >= 18 else "Menor de idade"
print(status)  # Maior de idade
```

1. Truthy e Falsy

Em Python, valores podem ser avaliados como True ou False em um contexto booleano:

- Falsy: False, None, 0, 0.0, '', [], {}, set()
- Truthy: Todos os outros valores

Exemplo:

```python
lista = []
if not lista:
    print("Lista vazia")

numero = 42
if numero:
    print("Número diferente de zero")
```

## Mais sobre Condicionais

```python
fruta = 'kiwi'
if fruta == 'kiwi':
    print("É kiwi") # -> É kiwi
else:
    print("Não é kiwi")

# Outra forma:
mensagem = 'É kiwi' if fruta == 'kiwi' else 'Não é kiwi'
print(mensagem) # -> É kiwi
# ou
print('É kiwi' if fruta == 'kiwi' else 'Não é kiwi') # -> É kiwi

# elif
fruta = 'maça'
if fruta == 'kiwi':
    print("É kiwi")
elif fruta == 'maça':
    print('É maça') # -> É maça
elif fruta == 'abacaxi':
    pass # Instrução para quando não há ação 
         # evitando dessa forma mensagem de erro.
else:
    print("Não é kiwi e nem maça")

"""
Operadores de comparação:
> (maior), < (menor), >= (maior igual), <= (menor igual),
!= (diferente) e == (igual)
"""

"""
Constantes:
True = 1
False = 0
"""
if False: # Equivale a 'false':
          # [] (lista vazia);
          # () (tupla vazia);
          # {} (dicionário vazio);
          # 0 (zero);
          # '' (string nula);
          # None (palavra reservada da linguagem).
    print('É verdadeiro!')
else:
    print('É falso!') # É falso

# Outro exemplo
valor1 = None
valor2 = 20
if valor1 and valor2: # valor1 equivale a false,
                      # não entrará neste bloco
    print('valor1 and valor2')
    print('Um destes equivale a false')
if valor1 or valor2: # Entrará neste bloco pois
                     # valor2 equivale a true
    print('valor1 or valor2')
    print('Ao menos um é verdadeiro')
```

## Ciclo while

### Estrutura básica:

```python
while condição
    código
else:
    código
```

### Exemplo:

```python
contador = 0
flag = True

while flag: # São válidos para uso:
            # '==', '!=', '>', '<', '>=', '<='
            # Este trecho poderia ser:
            # while contador <= 10
    if contador == 5:
        contador += 1 # Aumenta em 1 o contador
                      # É o mesmo que:
                      # contador = contador + 1
        continue # Entrando neste bloco passa para
                 # a próxima interação do while sem
                 # continuar com as linhas abaixo no
                 # bloco while

    # Ponto de saída do `while` quando
    # `contador` passa de 10.
    if contador > 10:
        flag = False

    # if contador == 6:
        # break # Interrompe o bloco while abruptamente

    print(contador)

    contador += 1
else:
    print('\nO while terminou!')
```

## Ciclo for

O ciclo ***for*** pode ser usado com interáveis ***(listas, tuplas, dicionários e strings)***.

```python
lista = [1,2,3,4,5,6,7,8,9,10]

for valor in lista:
    print(valor)
```

> **Saída:**
> 
> ```
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> 10
> ```

```python
new_range = range(0,5) # O mesmo que: range(5)

for valor in new_range:
    print(valor)
```

> **Saída:**
> 
> ```
> 0
> 1
> 2
> 3
> 4
> ```

```python
new_range = range(0,10,2) # Salta de dois-em-dois

for valor in new_range:
    print(valor)
```

> Saída:
> 
> ```
> 0
> 2
> 4
> 6
> 8
> ```

```python
lista = [1,2,3,4,5,6,7,8,9,10]

for indice, valor in enumerate(lista):
    print(valor, "Tem como indice:", indice)
```

> **Saída:**
> 
> ```
> 1 Tem como indice: 0
> 2 Tem como indice: 1
> 3 Tem como indice: 2
> 4 Tem como indice: 3
> 5 Tem como indice: 4
> 6 Tem como indice: 5
> 7 Tem como indice: 6
> 8 Tem como indice: 7
> 9 Tem como indice: 8
> 10 Tem como indice: 9
> ```

```python
lista = [1,2,3,4]

for valor in range(0, len(lista)):
    print(valor)
```

> **Saída:**
> 
> ```
> 0
> 1
> 2
> 3
> ```

```python
for valor in 'Python':
    print(valor)
```

> **Saída:**
> 
> ```
> P
> y
> t
> h
> o
> n
> ```

```python
dicionario = {'a': 10, 'b': 20, 'c': 500}
for chave, valor in dicionario.items(): # Além de `.items()`
                                        # existem também:
                                        # `.keys()` e `.values()`
    print(f"A chave: '{chave}' tem o valor: {valor}")
    """
    ou
    print("A chave: '{}' tem o valor: {}".format(chave, valor))
    """
```

> **Saída:**
> 
> A chave: 'a' tem o valor: 10
> A chave: 'b' tem o valor: 20
> A chave: 'c' tem o valor: 500

## List Comprehension

```python
"""
lista = []
for valor in range(0, 101):
    lista.append(valor)
"""
lista = [ valor for valor in range(0, 101) ]
print(lista)
```

> **Saída:**
> 
> ```
> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
> ```

```python
# Obtendo lista de nº pares entre 0 a 100
lista = [ valor for valor in range(0, 101) if valor % 2 == 0 ]
print(lista)
```

> **Saída:**
> 
> ```
> [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52, 54, 56, 58, 60, 62, 64, 66, 68, 70, 72, 74, 76, 78, 80, 82, 84, 86, 88, 90, 92, 94, 96, 98, 100]
> ```

```python
# Obtendo tupla de nº impares entre 0 a 100
tupla = tuple( valor for valor in range(0, 101) if valor % 2 != 0 )
print(tupla)
```

> **Saída:**
> 
> ```
> (1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39, 41, 43, 45, 47, 49, 51, 53, 55, 57, 59, 61, 63, 65, 67, 69, 71, 73, 75, 77, 79, 81, 83, 85, 87, 89, 91, 93, 95, 97, 99)
> ```

```python
lista = [ valor for valor in range(0, 11) ]
# Obtendo par chave/valor (dicionário)
dicionario = { indice:valor for indice, valor in enumerate(lista) }
print(dicionario)
```

> **Saída:**
> 
> ```
> {0: 0, 1: 1, 2: 2, 3: 3, 4: 4, 5: 5, 6: 6, 7: 7, 8: 8, 9: 9, 10: 10}
> ```

## Funções

### Calculo do fatorial de um número:

```python
def fatorial(numero):
    fatorial = 1
    while numero > 0:
        fatorial *= numero
        numero -= 1
    return fatorial

print(fatorial(4))
print(fatorial(5))
print(fatorial(6))
```

> **Saída:**
> 
> ```
> 24
> 120
> 720
> ```

### Quatro operações:

```python
# soma()
# Parâmetros com valores default
# caso algum deles ou ambos não
# sejam repassados.
def soma(num1 = 0, num2 = 0): 
    return num1 + num2

# subtracao()
def subtracao(num1 = 0, num2 = 0):
    return num1 - num2

# multiplicacao()
def multiplicacao(num1 = 0, num2 = 0):
    return num1 * num2

# divisao()
# num2 é igual a 1 para
# que não ocorra divisão
# por zero.
def divisao(num1 = 0, num2 = 1): 
    return num1 / num2

# multiplos_valores()
def multiplos_valores():
    return "String", 1, True, 25.6 # Vai retornar uma tupla.

# mostrar_resultado(funcao)
def mostrar_resultado(funcao): # Parametro desta função
    print(funcao)              # também é uma função.

print('\n*** As quatro operações\n')
print(f'\tSoma de 2 + 2: {soma(2,2)}\n')
print(f'\tSubtração de 2 - 2: {subtracao(2,2)}\n')
print(f'\tMultiplicação de 2 * 2: {multiplicacao(2,2)}\n')
print(f'\tDivisão de 2 / 2: {divisao(2,2)}\n')

print('*** Retorno de múltiplos valores como tupla:', multiplos_valores())

# Obtendo o mesmo resultado
print('\n*** Teste da referência de função\n')
print(multiplicacao(2, 3))
my_var = multiplicacao # Variável referenciando uma função.
print(my_var(2, 3))
mostrar_resultado(my_var(2, 3))
```

> **Saída:**
>
> ```
> *** As quatro operações
> 
>  Soma de 2 + 2: 4
> 
>  Subtração de 2 - 2: 0
> 
>  Multiplicação de 2 * 2: 4
> 
>  Divisão de 2 / 2: 1.0
> 
> *** Retorno de múltiplos valores como tupla:
> 
> ('String', 1, True, 25.6)
> 
> *** Teste da referência de função:
> 
> 6
> 6
> 6
> ```

## Variáveis globais

### Palindromo

```python
frase = 'arroz é zorra'
def palindromo():
    global nova_frase # Tornando uma variável global
    nova_frase = frase[::-1]
    return frase == nova_frase

print(frase) # arroz é zorra
palindromo() # True
print(nova_frase) # arroz é zorra
```

## Argumentos

### Número de argumentos indefinido

```python
def soma(*args): # 'args' é uma nomenclatura
                 # convencional recorrente
    res = 0 # 'res' variável local
    for val in args: # 'args' é uma tupla
        res += val
    print('tupla:', args)
    return res # 'res' variável local
res = soma(1, 2, 3, 4, 5, 6, 7, 8, 9) # 'res' variável global
print(res)
```

> **Saída:**
> 
> ```
> tupla: (1, 2, 3, 4, 5, 6, 7, 8, 9)
> 45
> ```

### Número de argumentos indefinido nomeados

```python
def soma(**kwargs): # 'kwargs' é uma nomenclatura
                    # convencional recorrente
    val1 = kwargs.get('v1', 0) # Obtem 'v1' default é 0
    val2 = kwargs.get('v2', 0) # Obtem 'v2' default é 0
    print('dicionario:', kwargs)
    return val1 + val2

print(soma(v1 = 10, v2 = 20))
```

> **Obs.:** ***\* (um asterisco)*** é para ***tupla*** e ***\*\* (dois asteriscos)*** é para ***dicionário***.

> **Saída:**
> 
> ```
> dicionario: {'v1': 10, 'v2': 20}
> 30
> ```

## Lambdas

```python
somaDoisValores = lambda v1, v2 : v1 + v2
converteEmPergunta = lambda frase : f'{frase}?'
# ou:
# converteEmPergunta = lambda frase : '{}?'.format(frase)
retornaUmInteiro = lambda : 10 # Não recebe parâmetros
lambdasDevemExecutarAlgo = lambda : print('Executando um print')

print('2 + 3 =', somaDoisValores(2, 3))
print(converteEmPergunta('O que estuda'))
print('O inteiro é:', retornaUmInteiro())
lambdasDevemExecutarAlgo()
```

> **Saída:**
> 
> ```
> 2 + 3 = 5
> O que estuda?
> O inteiro é: 10
> Executando um print
> ```

## Funções aninhadas

```python
def dividir(dividendo, divisor):
    def validar(): # Não necessita de parâmetros porque usam os
                   # parâmetros da função 'dividir' acima.
        return dividendo > 0 and divisor > 0
    if validar():
        return dividendo / divisor

print(dividir(10, 0)) # Retorna 'none' pois divisor é 0
print(dividir(10, 5))
```

> **Saída:**
> 
> ```
> None
> 2.0
> ```

### Closure

```python
def tabuada(multiplicador):
    def produto(multiplicando):
        return multiplicador, multiplicando, multiplicador * multiplicando
    return produto

def montaTabuada(func):
    for n in range(1, 10):
        res = func(n)
        print(f'{res[0]} x {res[1]} = {res[2]}')
        # ou:
        # print('{} x {} = {}'.format(res[0], res[1], res[2]))
    print('\n')

# Criando uma função a partir de uma função
deCinco = tabuada(5)
# Enviando uma função para uma função
montaTabuada(deCinco) # ou: montaTabuada(tabuada(5))
```

> **Saída:**
> 
> ```
> 5 x 1 = 5
> 5 x 2 = 10
> 5 x 3 = 15
> 5 x 4 = 20
> 5 x 5 = 25
> 5 x 6 = 30
> 5 x 7 = 35
> 5 x 8 = 40
> 5 x 9 = 45
> ```

## *args e **kwargs

Em Python, a função com parâmetros `*args` e `**kwargs` é uma forma flexível de passar argumentos para uma função. Aqui está o detalhamento de como eles funcionam:

### 1. `*args`

- O parâmetro `*args` permite passar um número **variável de argumentos posicionais** para uma função.
- Dentro da função, `args` será uma **tupla** que conterá todos os argumentos posicionais extras fornecidos.

**Exemplo de uso**:

```python
def funcao_exemplo(*args):
    for arg in args:
        print(arg)

# Chamada da função
funcao_exemplo(1, 2, 3, 4)

# --> Saída:
# 1
# 2
# 3
# 4
```

Aqui, `*args` permite que você passe qualquer quantidade de argumentos posicionais, e a função irá iterar sobre eles.

### 2. `**kwargs`

- O parâmetro `**kwargs` permite passar um número **variável de argumentos nomeados** (ou argumentos de palavra-chave) para a função.
- Dentro da função, `kwargs` será um **dicionário** que conterá os argumentos nomeados (chave e valor).

**Exemplo de uso**:

```python
def funcao_exemplo(**kwargs):
    for chave, valor in kwargs.items():
        print(f"{chave} = {valor}")

# Chamada da função
funcao_exemplo(nome="Maria", idade=25, cidade="São Paulo")

# Saída:
# nome = Maria
# idade = 25
# cidade = São Paulo
```

Aqui, `**kwargs` permite que você passe qualquer quantidade de argumentos nomeados, e a função os processa como um dicionário.

### Combinação de `*args` e `**kwargs`

Você pode usar `*args` e `**kwargs` juntos para permitir que a função aceite ambos os tipos de argumentos (posicionais e nomeados).

**Exemplo**:

```python
def funcao_exemplo(*args, **kwargs):
    print("Argumentos posicionais:", args)
    print("Argumentos nomeados:", kwargs)

# Chamada da função
funcao_exemplo(1, 2, 3, nome="Maria", idade=25)

# Saída:
# Argumentos posicionais: (1, 2, 3)
# Argumentos nomeados: {'nome': 'Maria', 'idade': 25}
```

### Regras de uso:

- A ordem dos parâmetros na definição de uma função deve ser: argumentos normais, depois `*args`, depois argumentos nomeados comuns (se houver), e por fim `**kwargs`.

Exemplo correto:

```python
def funcao_exemplo(arg1, arg2, *args, **kwargs):
    pass
```

### Resumo:

- `*args`: captura argumentos **posicionais** em uma tupla.
- `**kwargs`: captura argumentos **nomeados** em um dicionário.

Isso torna a função muito flexível para aceitar diferentes tipos de entradas sem a necessidade de definir explicitamente cada parâmetro.

## **kwargs para inicializar atributos em um construtor

você pode usar `**kwargs` para inicializar atributos em um construtor (`__init__`) de uma classe. Isso é útil quando você deseja inicializar os atributos de uma classe de forma flexível, permitindo que o usuário da classe passe diferentes combinações de parâmetros nomeados.

Aqui está um exemplo simples de como usar `**kwargs` para inicializar atributos no construtor de uma classe:

### Exemplo:

```python
class Pessoa:
    def __init__(self, **kwargs):
        # Inicializando atributos com base em kwargs
        self.nome = kwargs.get('nome', 'Desconhecido')
        self.idade = kwargs.get('idade', 0)
        self.cidade = kwargs.get('cidade', 'Desconhecida')

    def exibir_informacoes(self):
        print(f"Nome: {self.nome}, Idade: {self.idade}, Cidade: {self.cidade}")

# Criando instâncias da classe passando parâmetros com **kwargs
p1 = Pessoa(nome="Maria", idade=25)
p2 = Pessoa(nome="João", cidade="Rio de Janeiro")
p3 = Pessoa()  # Sem passar parâmetros, assumirá os valores padrão

# Exibindo informações
p1.exibir_informacoes()  # Nome: Maria, Idade: 25, Cidade: Desconhecida
p2.exibir_informacoes()  # Nome: João, Idade: 0, Cidade: Rio de Janeiro
p3.exibir_informacoes()  # Nome: Desconhecido, Idade: 0, Cidade: Desconhecida
```

### Como funciona:

1. No método `__init__`, `**kwargs` é usado para receber um número variável de argumentos nomeados.
2. O método `get()` do dicionário é usado para buscar os valores dentro de `kwargs`. Caso a chave não exista, um valor padrão será retornado (`'Desconhecido'` para o nome, `0` para a idade, etc.).
3. Você pode passar qualquer combinação de argumentos nomeados ao criar uma instância da classe, e os atributos serão inicializados com base no que foi fornecido (ou com os valores padrão se não forem especificados).

### Vantagens:

- **Flexibilidade**: Você pode inicializar diferentes atributos sem a necessidade de especificar todos os parâmetros no construtor.
- **Valores padrão**: Você pode definir valores padrão para atributos não especificados, como mostrado no exemplo.

Esse padrão pode ser muito útil em cenários em que você não sabe antecipadamente quais atributos precisarão ser inicializados ou onde os atributos são opcionais.

## Decoradores

```python
"""
Decoradores é composta de três funções:
A (função que empacota tudo - wrapper),
B (função à decorar, ou seja, que receberá novas
funcionalidades) e
C (função que retorna com as novas funcionalidades)
"""
def decorador(func): # A recebendo B
    def nova_funcao(*args, **kwargs): # *args e **kwargs são
                                      # para contemplar
                                      # parâmetros caso haja.
        print(f'Executando função: {func.__name__}')
        func(*args, **kwargs)
        print('Fim...\n')
    return nova_funcao # retorna C

@decorador
def saudar():
    print('\tOlá, mundo!!!')

@decorador
def soma(num1, num2):
    print(f'\t2 + 2 = {num1 + num2}')

saudar()

soma(2, 2)
```

> **Saída:**
> 
> ```
> Executando função: saudar
>     Olá, mundo!!!
> Fim...
> 
> Executando função: soma
>     2 + 2 = 4
> Fim...
> ```

## Generators

```python
def gerador(*args):
    for valor in args:
        # yield funciona como return
        # entretanto permite a interação.
        yield valor, True if valor > 5 else False

for valor, boleano in gerador(1,2,3,4,5,6,7,8,9):
    print(f'{valor} - {boleano}')
    # ou:
    # print('{} - {}'.format(valor, boleano))
```

> **Saída:**
> 
> ```bash
> 1 - False
> 2 - False
> 3 - False
> 4 - False
> 5 - False
> 6 - True
> 7 - True
> 8 - True
> 9 - True
> ```

## Docstring

```python
"""
- A Docstring deve vir seguida ao nome da função
  para que o interpretador python a considere
  como tal.
"""
def gerador(*args):
    """
- Conteudo da Docstring:
- Esta função:
  - Recebe n qtde de números e retorna o número
    além disso retorna True ou False se o número
    é maior que 5.
    """
    for valor in args:
        # yield funciona como return
        # entretando permite a interação.
        yield valor, True if valor > 5 else False


for valor, boleano  in gerador(1,2,3,4,5,6,7,8,9):
    print(f'{valor} - {boleano}')
    # print('{} - {}'.format(valor, boleano))

# Mostra o nome desta função e o
# conteúdo da Docstring
print(f"\n- Nome da função: {gerador.__name__}")
# ou:
# print("\n- Nome da função: {}".format(gerador.__name__))
print(gerador.__doc__)
```

> **Saída:**
> 
> ```bash
> 1 - False
> 2 - False
> 3 - False
> 4 - False
> 5 - False
> 6 - True
> 7 - True
> 8 - True
> 9 - True
> 
> - Nome da função: gerador
> 
> - Conteudo da Docstring:
> - Esta função:
>   - Recebe n qtde de números e retorna o número
>     além disso retorna True ou False se o número
>     é maior que 5.
> ```

### Obtendo a Docstring pelo interpretador

```python
"""
- A Docstring deve vir seguida ao nome da função
  para que o interpretador python a considere
  como tal.
"""
def gerador(*args):
    """
- Conteudo da Docstring:
- Esta função:
  - Recebe n qtde de números e retorna o número
    além disso retorna True ou False se o número
    é maior que 5.
    """
    for valor in args:
        # yield funciona como return
        # entretando permite a interação.
        yield valor, True if valor > 5 else False
```

> **Usando o interpretador:**
> 
> ```bash
> >>> from func import gerador
> >>> help(gerador)
> 
> Help on function gerador in module test:
> 
> gerador(*args)
>     - Conteudo da Docstring:
>     - Esta função:
>       - Recebe n qtde de números e retorna o número
>         além disso retorna True ou False se o número
>         é maior que 5.
> (END)
> ```

## Módulo

Quando a aplicação tende a crescer muito em linhas de código desmembramos as funções em um módulo ou mais separando do script principal ***(main.py)***, vejamos:

***calculadora.py***

```python
def soma(n1, n2):
    # Retorna um número inteiro do resultado de uma soma
    return n1 + n2

def diferenca(n1, n2):
    # Retorna um número inteiro do resultado de uma diferença
    return n1 - n2

def produto(n1, n2):
    # Retorna um número inteiro do resultado de um produto
    return n1 * n2

def quociente(n1, n2):
    # Retorna um número real do resultado de um quociente
    return n1 / n2
```

***main.py***

```python
import calculadora # Considerando que main.py e
                   # calculadora.py estão na mesma
                   # pasta ou diretório

print (f'2 + 2 = {calculadora.soma(2, 2)}')
print (f'2 - 2 = {calculadora.diferenca(2, 2)}')
print (f'2 * 2 = {calculadora.produto(2, 2)}')
print (f'2 / 2 = {calculadora.quociente(2, 2)}')
```

> **Agora executando o script main.py a saída é:**
> 
> ```
> 2 + 2 = 4
> 2 - 2 = 0
> 2 * 2 = 4
> 2 / 2 = 1.0
> ```
> 
> Obs.: Na primeira execução de main.py é gerado a pasta pycache contendo a compilação do módulo calculadora.py para que seja executado mais rapidamente nas próximas vezes.

## Formas de importar módulos

***main.py***

```python
"""
-----------------------------------
Outras formas de importar módulos
-----------------------------------
O último método importado optou-se por mudar
o nome 'quociente' para 'div'.
"""
from calculadora import soma, diferenca, produto,
                        quociente as div
"""
-----------------------------------
ou
-----------------------------------
from calculadora import (soma, diferenca, produto,
                         quociente as div)
"""
print (f'2 + 2 = {soma(2, 2)}')
print (f'2 - 2 = {diferenca(2, 2)}')
print (f'2 * 2 = {produto(2, 2)}')
print (f'2 / 2 = {div(2, 2)}')
```

> **Agora executando o script *main.py* a saída é:**
> 
> ```
> 2 + 2 = 4
> 2 - 2 = 0
> 2 * 2 = 4
> 2 / 2 = 1.0
> ```

## Criando um módulo de maneira profissional

```python
"""
Aqui colocamos tudo o que faz este módulo
a que contexto ele corresponde
"""
__author__ = "Fulano de tal"
__copyright__ = "Copyright 2021, Empresa XYZ"
__credits__ = "Empresa XYZ"
__license__ = "GPL"
__version__ = "1.0.1"
__maintainer__ = "Fulano de tal"
__email__ = "fulanodetal@empreza_xyz.com"
__status__ = "Developer"
def soma(n1, n2):
    """Retorna um número inteiro do resultado de uma soma"""
    return n1 + n2
def diferenca(n1, n2):
    """Retorna um número inteiro do resultado de uma diferença"""
    return n1 - n2
def produto(n1, n2):
    """Retorna um número inteiro do resultado de um produto"""
    return n1 * n2
def quociente(n1, n2):
    """Retorna um número real do resultado de um quociente"""
    return n1 / n2
```

> **Chamando o interpretador python3 obtemos:**
> 
> ```bash
> Python 3.7.3 (default, Jan 22 2021, 20:04:44) 
> [GCC 8.3.0] on linux
> Type "help", "copyright", "credits" or "license" for more information.
> >>> import calculadora
> >>> help(calculadora)
> 
> Help on module calculadora:
> 
> NAME
>     calculadora
> 
> DESCRIPTION
>     Aqui colocamos tudo o que faz este módulo
>     a que contexto ele corresponde
> 
> FUNCTIONS
>     diferenca(n1, n2)
>         Retorna um número inteiro do resultado de uma diferença
> 
>     produto(n1, n2)
>         Retorna um número inteiro do resultado de um produto
> 
>     quociente(n1, n2)
>         Retorna um número real do resultado de um quociente
> 
>     soma(n1, n2)
>         Retorna um número inteiro do resultado de uma soma
> 
> DATA
>     __copyright__ = 'Copyright 2021, Empresa XYZ'
>     __email__ = 'fulanodetal@empreza_xyz.com'
>     __license__ = 'GPL'
>     __maintainer__ = 'Fulano de tal'
>     __status__ = 'Developer'
> 
> VERSION
>     1.0.1
> 
> AUTHOR
>     Fulano de tal
> Help on module calculadora:
> 
> NAME
>     calculadora
> 
> DESCRIPTION
>     Aqui colocamos tudo o que faz este módulo
>     a que contexto ele corresponde
> 
> FUNCTIONS
>     diferenca(n1, n2)
>         Retorna um número inteiro do resultado de uma diferença
> 
>     produto(n1, n2)
>         Retorna um número inteiro do resultado de um produto
> 
>     quociente(n1, n2)
>         Retorna um número real do resultado de um quociente
> 
>     soma(n1, n2)
>         Retorna um número inteiro do resultado de uma soma
> 
> DATA
>     __copyright__ = 'Copyright 2021, Empresa XYZ'
>     __email__ = 'fulanodetal@empreza_xyz.com'
>     __license__ = 'GPL'
>     __maintainer__ = 'Fulano de tal'
>     __status__ = 'Developer'
> 
> VERSION
>     1.0.1
> 
> AUTHOR
>     Fulano de tal
> ```
> 
> **Mais informações sobre o módulo:**
> 
> ```bash
> >>> import calculadora
> >>> dir(calculadora)
> ['__author__', '__builtins__', '__cached__', '__copyright__', '__credits__', '__doc__', '__email__', '__file__', '__license__', '__loader__', '__maintainer__', '__name__', '__package__', '__spec__', '__status__', '__version__', 'diferenca', 'produto', 'quociente', 'soma']
> ```

## Atribuito \_\_name\_\_

```python
from calculadora import __name__ as __name_calculadora__

print(__name__)
print(__name_calculadora__)
```

> **Chamando o interpretador python3:**
> 
> ```bash
> $ python3 main.py
> __main__
> calculadora
> ```

Quando se quer evitar que seja executado diretamente um módulo:

```python
def soma(n1, n2):
    """Retorna um número inteiro do resultado de uma soma"""
    return n1 + n2
def diferenca(n1, n2):
    """Retorna um número inteiro do resultado de uma diferença"""
    return n1 - n2
def produto(n1, n2):
    """Retorna um número inteiro do resultado de um produto"""
    return n1 * n2
def quociente(n1, n2):
    """Retorna um número real do resultado de um quociente"""
    return n1 / n2

if __name__ == '__main__': # Esta condição será true
                           # quando este script for
                           # executado diretamente.
    print("""Isto é um módulo, não deve ser
    executado como script principal!!!""")
```

> **Saída:**
> 
> ```bash
> $ python3 calculadora.py 
> Isto é um módulo, não deve ser
> executado como script principal!!!
> ```

## Anotações de tipo (type hints)

O uso de uma seta (`->`) para definir o tipo de retorno de uma função é um recurso de *type hinting* (sugestão de tipo) do Python introduzido na versão 3.5. Isso ajuda a melhorar a legibilidade do código e permite que ferramentas de análise estática, como o MyPy, verifiquem a compatibilidade dos tipos em tempo de desenvolvimento.

### Como Funciona o Type Hinting com Arrow (`->`)

Na declaração de uma função, você pode especificar o tipo esperado para cada argumento, seguido do tipo de retorno esperado após a seta (`->`). Isso é feito da seguinte maneira:

```python
def nome_funcao(arg1: tipo1, arg2: tipo2) -> tipo_retorno:
    # corpo da função
    return resultado
```

- `arg1: tipo1, arg2: tipo2` - Define os tipos esperados dos argumentos `arg1` e `arg2`.
- `-> tipo_retorno` - Indica o tipo que a função deve retornar.

É importante destacar que essa anotação é apenas uma sugestão para quem lê o código e para ferramentas de análise estática; o Python em si não impõe restrições de tipo em tempo de execução.

### Exemplo

Vamos ver um exemplo prático para entender melhor:

```python
def soma(a: int, b: int) -> int:
    """Soma dois números inteiros."""
    return a + b
```

Neste exemplo:

- A função `soma` espera receber dois argumentos do tipo `int` (inteiros).
- A seta `-> int` indica que o valor de retorno da função será do tipo `int`.

Outro exemplo, agora com um tipo de retorno diferente:

```python
def cumprimentar(nome: str) -> str:
    """Retorna uma saudação personalizada."""
    return f"Olá, {nome}!"
```

Neste caso:

- A função `cumprimentar` recebe um argumento `nome` do tipo `str` (string).
- A seta `-> str` indica que a função retornará um valor do tipo `str`.

### Exemplo com Tipos Mais Complexos

As sugestões de tipo também podem ser usadas com tipos mais complexos, como listas, dicionários e até funções. Veja um exemplo de uma função que recebe uma lista de números e retorna a média:

```python
from typing import List

def calcular_media(numeros: List[float]) -> float:
    """Calcula a média de uma lista de números."""
    return sum(numeros) / len(numeros)
```

Aqui:

- `numeros: List[float]` indica que o argumento `numeros` deve ser uma lista de números de ponto flutuante (`float`).
- `-> float` indica que o resultado retornado será um número de ponto flutuante.

### Vantagens do Uso de Type Hinting

1. **Melhoria na Legibilidade:** Facilita o entendimento do código, especialmente em projetos grandes ou quando você está trabalhando em um time.
2. **Detecção de Erros:** Ferramentas como o MyPy podem usar as anotações para detectar erros de tipo antes de o código ser executado.
3. **Documentação Automática:** Ajuda a documentar o propósito e o uso das funções de forma mais explícita.

Se tiver mais alguma dúvida ou quiser mais exemplos, fique à vontade para perguntar!

o *type hinting* (sugestão de tipo) pode ser aplicado em métodos de classes da mesma forma que em funções comuns. Isso ajuda a melhorar a clareza e a consistência do código, especialmente em projetos orientados a objetos.

### Usando *Type Hinting* em Métodos de Classe

Quando usamos *type hinting* em métodos de uma classe, podemos definir o tipo de `self`, os tipos dos parâmetros e o tipo de retorno da função. A sintaxe é a mesma que para funções normais, com a adição do parâmetro `self` (que representa a instância da classe).

#### Exemplo Básico

Vamos ver um exemplo simples de uma classe que define um método para calcular a área de um retângulo:

```python
class Retangulo:
    def __init__(self, largura: float, altura: float) -> None:
        self.largura = largura
        self.altura = altura
    
    def area(self) -> float:
        """Calcula a área do retângulo."""
        return self.largura * self.altura
```

#### Explicação:

1. No método `__init__`, utilizamos *type hinting* para os parâmetros `largura` e `altura`, ambos do tipo `float`. O tipo de retorno é `None` porque o método `__init__` não retorna um valor.
2. No método `area`, especificamos que ele não recebe nenhum parâmetro (além de `self`) e retorna um valor do tipo `float`.

### Exemplo com Tipos Mais Complexos

Agora, vejamos um exemplo mais complexo em que um método retorna uma instância da própria classe. Aqui usamos *type hinting* para indicar que o retorno será do tipo da classe atual:

```python
class Calculadora:
    def __init__(self, valor: float) -> None:
        self.valor = valor
    
    def adicionar(self, outro: float) -> 'Calculadora':
        """Adiciona um valor e retorna a própria instância."""
        self.valor += outro
        return self
    
    def subtrair(self, outro: float) -> 'Calculadora':
        """Subtrai um valor e retorna a própria instância."""
        self.valor -= outro
        return self
    
    def resultado(self) -> float:
        """Retorna o valor atual."""
        return self.valor
```

#### Explicação:

1. No método `adicionar`, usamos *type hinting* para indicar que o método retorna uma instância da classe `Calculadora` (usando `'Calculadora'` entre aspas porque a classe ainda não está completamente definida).
2. O mesmo acontece com o método `subtrair`, onde retornamos `self` para permitir o encadeamento de métodos (*method chaining*).
3. O método `resultado` retorna um valor do tipo `float`, que é o valor atual após as operações.

### *Type Hinting* com Variáveis de Instância

Também podemos ser mais explícitos com as variáveis de instância usando anotações de tipo no corpo da classe. Por exemplo:

```python
class Pessoa:
    nome: str
    idade: int

    def __init__(self, nome: str, idade: int) -> None:
        self.nome = nome
        self.idade = idade

    def cumprimentar(self) -> str:
        """Retorna uma saudação."""
        return f"Olá, {self.nome}, você tem {self.idade} anos."
```

Nesse exemplo:

- `nome: str` e `idade: int` são anotações de tipo para as variáveis de instância, indicando que `nome` deve ser do tipo `str` e `idade` do tipo `int`.

### Benefícios em Métodos de Classe

1. **Clareza:** Ajudam a entender quais tipos são esperados nos parâmetros dos métodos e o tipo de retorno.
2. **Manutenção:** Facilita a manutenção do código em equipes ou projetos maiores.
3. **Detecção de Erros:** Como no caso de funções comuns, ferramentas como MyPy ajudam a detectar inconsistências de tipos.

### Exemplo Final com Classe e Método Estático

Um último exemplo, usando um método estático:

```python
class Matematica:
    @staticmethod
    def somar(a: int, b: int) -> int:
        """Soma dois números inteiros."""
        return a + b
```

Neste exemplo:

- O método `somar` é um método estático (não precisa de uma instância da classe) e utiliza *type hinting* para indicar que os parâmetros são inteiros e o retorno também é um inteiro.

Assim, *type hinting* pode ser usado em classes da mesma forma que em funções normais, trazendo os mesmos benefícios de clareza, segurança e documentação.

## Bibliotecas - Uma amostra

```python
import random

print(random.randint(0,10)) # Imprime um número aleatório
                            # de 0 a 10 inclusive.
lista = [True, "String", 23, False]
print(random.choice(lista)) # Imprime aleatoriamente um
                            # item da lista.

random.shuffle(lista) # Muda a ordem original dos
                      # elementos.
print(lista)
```

> **Saída:**
> 
> ```
> $ python3 libraries.py 
> 5
> False
> [False, 'String', 23, True]
> $ python3 libraries.py 
> 0
> 23
> [False, 23, 'String', True]
> ```

```python
import datetime
print(datetime.datetime.now())
```

> **Saída:**
> 
> ```
> $ python3 time.py 
> 2021-09-19 16:52:12.863707
> ```

```python
import sys # Permite usar recursos de terminal
import time

for i in range(100):
    time.sleep(0.5)
    sys.stdout.write("\r%d %%" % i) # Para escrever no terminal
    sys.stdout.flush() # Para visualizar o que foi escrito
```

> **Saída:**
> 
> ```bash
> $ python3 libraries.py 
> 99 %
> ```

## Argv

```python
import sys

if __name__ == '__main__'
    if len(sys.argv) == 1:
        print('É necessario ao menos um argumento!!!')
    else:
        if sys.argv[1] == 'help':
            print("Contate o desenvolvedor!!!")
        print(sys.argv[1])
```

> **Saída:**
> 
> ```bash
> $ python3 argv.py
> É necessario ao menos um argumento!!!
> 
> $ python3 argv.py help
> Contate o desenvolvedor!!!
> help
> 
> $ python3 argv.py soma
> soma
> ```

## Exceções

Exemplo de um erro:

```python
print(2/0)
print("Script terminou!!!")
```

> **Saída:**
> 
> ```bash
> $ python3 exception.py 
> Traceback (most recent call last):
>   File "exception.py", line 1, in <module>
>     print(2/0)
> ZeroDivisionError: division by zero
> ```

Agora tratando o erro:

```python
try:
    print(2/0) # Instrução onde ocorre o erro
except ZeroDivisionError as error: 
    """
    Pegamos na saída anterior do 'print' o módulo que 
    trata o erro e colocamos o retorno em 'error'.
    """
    print(error) # Imprimos o conteúdo de 'error'
    """
    Colocamos abaixo nossa
    mensagem customizada.
    """
    print("Não é possível dividir por 0") 
print("Script terminou!!!")
```

> **Saída:**
> 
> ```
> $ python3 exception.py 
> division by zero
> Não é possível dividir por 0
> Script terminou!!!
> ```

Outro exemplo:

```python
try:
    lista = [1,2]
    print(lista[9])
    print(2/0)
"""
Nas exceções abaixo cobrimos
os erros que ocorrem.
"""
except IndexError as error:
    print(error)
    print("Não é possível obter o valor na posição 9")
except ZeroDivisionError as error:
    print(error)
    print("Não é possível dividir por 0")
"""
O bloco finally é sempre executado
ocorrendo exceção ou não.
"""
finally:
    print("Script terminou!!!")
```

> **Saída:**
> 
> ```bash
> $ python3 exception.py 
> list index out of range
> Não é possível obter o valor na posição 9
> Script terminou!!!
> ```
> 
> Comentando a linha onde encontramos a instrução abaixo (3ª linha):
> 
> ```python
> print(lista[9])
> ```
> 
> Ficando:
> 
> ```python
> # print(lista[9])
> ```
> 
> Obteremos a saída:
> 
> ```
> $ python3 exception.py 
> division by zero
> Não é possível dividir por 0
> Script terminou!!!
> ```
> 
> Exceção genérica
> 
> ```python
> try:
>        lista = [1,2]
>        print(lista[9])
>        print(2/0)
> except Exception as error: # Intercepta qualquer erro
>        print(error)
>        print("Não sei que erro ocorreu, mas ocorreu!!!")
> finally:
>        print("Script terminou!!!")
> ```
> 
> **Saída:**
> 
> ```
> $ python3 exception.py 
> list index out of range
> Não sei que erro ocorreu, mas ocorreu!!!
> Script terminou!!!
> ```
> 
> **Obs.:** O ideal não é usar a forma genérica de exceções (Exception) mas sim específicar os possíveis erros que podem ocorrer.

## Classes e Objetos

Classes são criadas em Python usando a palavra chave ***class***. Variáveis de classe são definidas diretamente no escopo da classe, enquanto variáveis de instância são definidas no construtor. O construtor em Python é a função ***\_\_init\_\_(self)***.

Exemplos:

***music.py***

```python
class Music:
    tipo = 'music' # variável de classe
    
    def __init__(self, genero='pop'): # construtor
    	self.genero = genero # variável de instância.
```

***lapis.py***

```python
"""
Nome de classe inicia com letra maiúscula
Nomes compostos usa-se padrão camel case.
"""
class Lapis:
    # Inicializando atributos de classe
    cor = 'preto'
    contem_borracha = False
    usa_grafite = True

# Instanciando um objeto
lapis = Lapis()
# Imprimindo conteúdo de seus atributos
print('Cor:', lapis.cor)
print('Contem borracha:', lapis.contem_borracha)
print('Usa grafite:', lapis.usa_grafite)
```

> **Saída:**
> 
> ```
> $ python3 lapis.py 
> Cor: preto
> Contem borracha: False
> Usa grafite: True
> ```

## Métodos

Métodos são funções que pertencem à classe ou ao objeto. O método pertencente ao objeto deve ter o parâmetro ***self*** enquanto o método de classe não. Algumas linguagens permitem chamar um método de classe em um objeto. Em Python isso não é possível.

```python
class MinhaClasse():
    def metodo_do_objeto(self):
    	pass
    def metodo_da_classe():
    	pass
    
    MinhaClasse.metodo_da_classe()
    obj = MinhaClasse()
    obj.metodo_do_objeto()
```

## Atributos e Métodos

***lapis.py***

```python
class Lapis:
    # Atributos de classe
    cor = 'preto'
    contem_borracha = False
    usa_grafite = True
    
    # Métodos
    def escrever(self):
        print("O lápis esta escrevendo.")
    def apagar(self):
        if self.possui_borracha():
            print("O lápis esta apagando.")
        else:
            print("Não é possível apagar.")
    def possui_borracha(self):
        return self.contem_borracha

lapis = Lapis() # Instanciando
lapis.escrever()
lapis.apagar()
# Modifica o valor do atributo
lapis.contem_borracha = True
lapis.apagar()
```

> **Saída:**
> 
> ```
> $ python3 lapis.py 
> O lápis esta escrevendo.
> Não é possível apagar.
> O lápis esta apagando.
> ```

## Método init

O construtor em Python.

***lapis.py***

```python
class Lapis:
    # __init__ (construtor)
    def __init__(self, cor = 'preto', contem_borracha = False, usa_grafite = True):
        self.cor = cor
        self.contem_borracha = contem_borracha
        self.usa_grafite = usa_grafite
        
    # Métodos de instância
    def escrever(self):
        print("O lápis esta escrevendo.")
    def apagar(self):
        if self.possui_borracha():
            print("O lápis esta apagando.")
        else:
            print("Não é possível apagar.")
    def possui_borracha(self):
        return self.contem_borracha

lapis = Lapis(contem_borracha = True) # Instanciando
lapis.escrever()
lapis.apagar()
```

> **Saída:**
>
> ```
> $ python3 lapis.py 
> O lápis esta escrevendo.
> O lápis esta apagando.
> ```
>
> Outra variação do script acima com a mesma saída:
>
> ```python
> class Lapis:
>  # Atributos de classe
>  cor = 'preto'
>  usa_grafite = True
> 
>  """
>  Método init com valor default de atributo
>  podendo ser modificado no instanciamento.
>  """
>  def __init__(self, contem_borracha = False):
>     # Atributo de instância
>      self.contem_borracha = contem_borracha
>         
>  # Métodos de instância
>  def escrever(self):
>      print("O lápis esta escrevendo.")
>     
>  def apagar(self):
>      if self.possui_borracha():
>          print("O lápis esta apagando.")
>      else:
>          print("Não é possível apagar.")
>             
>  def possui_borracha(self):
>      return self.contem_borracha
> 
> """
> Criando variável de instância 
> inserindo valor para o atributo
> modificando o valor default.
> """
> lapis = Lapis(contem_borracha = True)
> lapis.escrever()
> lapis.apagar()
> ```

## Métodos públicos, protegidos e privados

Python não tem palavras chaves para permissão de acesso, como public, protected e private. Na verdade, a linguagem nem reforça essas permissões. Em Python utiliza-se convenção para declarar a accessibilidade de um método, função ou atributo. Você pode acessar métodos protected de qualquer lugar e os private estão apenas escondidos, mas são acessíveis se você realmente quiser.

```python
class MinhaClasse():
    # Todo método é normalmente público
    def metodo_publico(self): 
    	pass
    
	# Métodos protegidos começam com _ (um underline)
    def _metodo_protected(): 
    	pass
    
	# Métodos privados começam com __ (dois underlines)
    def __metodo_private(): 
    	pass
```

***usuario.py***

```python
"""
Atributos e Métodos privados só podem ser
acessados pela classe e não pela instância.
"""
class Usuario:
    def __init__(self, username, password, email):
        self.username = username
        """
        Atributo e Método privado começam
        com '__' (dois underlines)
        """
        self.__password = self.__convertToUppercase(password)
        self.email = email
        
    # Método privado
    def __convertToUppercase(self, password):
        return password.upper()
    
    def getPassword(self):
        return self.__password

user = Usuario('Fulano', 'fulano123', 'fulano@email.com')
print(user.username)
print(user.email)
print(user.getPassword())
```

> **Saída:**
> 
> ```
> $ python3 usuario.py 
> Fulano
> fulano@email.com
> FULANO123
> ```

## Variáveis de classe

***circulo.py***

```python
class Circulo:
    # Atributo de classe que neste caso é privado.
    __pi = 3.1416 

    def __init__(self, raio):
        self.raio = raio

    def area(self):
        return self.raio * self.raio * self.__pi

c1 = Circulo(4)
c2 = Circulo(3)

print(f"Área de circulo de raio = {c1.raio}: {c1.area()}")
print(f"Área de circulo de raio = {c2.raio}: {c2.area()}")
```

> **Saída:**
> 
> ```
> $ python3 circulo.py 
> Área de circulo de raio = 4: 50.2656
> Área de circulo de raio = 3: 28.2744
> ```

## Propriedades

***usuario.py***

```python
class Usuario:
    def __init__(self, username, password, email):
        self.username = username
        self.__password = self.__convertToUppercase(password)
        self.email = email
        
    # Método privado
    def __convertToUppercase(self, password):
        return password.upper()
    
    @property
    def password(self):
        return self.__password
    
    @password.setter
    def password(self, newPassword):
        self.__password = self.__convertToUppercase(newPassword)

user = Usuario('Fulano', 'fulano123', 'fulano@email.com')
print(user.password)

user.password = 'Novo password'
print(user.password)

print('\nImprimindo atributos e respectivos valores:\n')
print(user.__dict__)
```

> **Saída:**
> 
> ```
> $ python3 usuario.py 
> FULANO123
> NOVO PASSWORD
> 
> Imprimindo atributos e respectivos valores:
> 
> {'username': 'Fulano', '_Usuario__password': 'NOVO PASSWORD', 'email': 'fulano@email.com'}
> ```

## Métodos estáticos

***circulo.py***

```python
class Circulo:
    @staticmethod
    def pi():
        return 3.1416

    def __init__(self, raio):
        self.raio = raio

    def area(self):
        return self.raio * self.raio * self.pi()

print(f'PI = {Circulo.pi()}')
c1 = Circulo(7)
print(f'Área de raio = {c1.raio}: {c1.area()}')
```

> **Saída:**
> 
> ```
> $ python3 circulo.py 
> PI = 3.1416
> Área de raio = 7: 153.9384
> ```

## Herança

***Exemplo:***

```python
class Pessoa:
    def __init__(self, nome: str, idade: int) -> None:
        self.nome = nome
        self.idade = idade

class Contato(Pessoa):
    def __init__(self, nome: str, idade: int, email: str) -> None:
        super().__init__(nome, idade)
        self.email = email

    def exibeDados(self) -> None:
        print(f"Nome: {self.nome} | Idade: {self.idade} | Email: {self.email}")

if __name__ == '__main__':
    contato = Contato(nome = 'Fulano', idade = 22, email = 'fulano@email.com')
    contato.exibeDados()
    # --> Saída:
    # Nome: Fulano | Idade: 22 | Email: fulano@email.com
```

***animal.py***

```python
class Animal:
    @property
    def terrestre(self):
        return True

class Felino(Animal):
    @property
    def garras_retrateis(self):
        return True
    def perseguir(self):
        print('\t\tO felino esta caçando!')

class Gato(Felino):
    def gato_perseguidor(self):
        self.perseguir()

class Jaguar(Felino):
    pass

gato = Gato()
jaguar = Jaguar()

# Informações sobre o Gato
print('\n- Gato:')
print(f'\t- É terrestre: {gato.terrestre}')
print(f'\t- Possui garras retráteis: {gato.garras_retrateis}')
print('\t- O que o felino esta fazendo:')
gato.gato_perseguidor()

# Informações sobre o Jaguar
print('\n- Jaguar:')
print(f'\t- É terrestre: {jaguar.terrestre}')
print(f'\t- Possui garras retráteis: {jaguar.garras_retrateis}')
print('\t- O que o felino esta fazendo:')
jaguar.perseguir()
```

> **Saída:**
> 
> ```
> $ python3 animal.py 
> 
> - Gato:
>     - É terrestre: True
>     - Possui garras retráteis: True
>     - O que o felino esta fazendo:
>         O felino esta caçando!
> 
> - Jaguar:
>     - É terrestre: True
>     - Possui garras retráteis: True
>     - O que o felino esta fazendo:
>         O felino esta caçando!
> ```

## Herança múltipla

***animal.py***

```python
class Animal:
    @property
    def terrestre(self):
        return True

class Felino(Animal):
    @property
    def garras_retrateis(self):
        return True
    def perseguir(self):
        print('\t\tO felino esta caçando!')

class Mascote:
    # Todos os mascotes necessitam de um nome
    nome = ''

# Classe com herança múltipla
class Gato(Felino, Mascote):
    def gato_perseguidor(self):
        self.perseguir()

class Jaguar(Felino):
    pass

gato = Gato()
jaguar = Jaguar()

# Informações sobre o Gato
gato.nome = 'Frajola'
print('\n- Gato:')
print(f'\t- Seu nome é: {gato.nome}')
print(f'\t- É terrestre: {gato.terrestre}')
print(f'\t- Possui garras retráteis: {gato.garras_retrateis}')
print('\t- O que o felino esta fazendo:')
gato.gato_perseguidor()

# Informações sobre o Jaguar
print('\n- Jaguar:')
print(f'\t- É terrestre: {jaguar.terrestre}')
print(f'\t- Possui garras retráteis: {jaguar.garras_retrateis}')
print('\t- O que o felino esta fazendo:')
jaguar.perseguir()
```

> **Saída:**
> 
> ```
> $ python3 animal.py 
> 
> - Gato:
>     - Seu nome é: Frajola
>     - É terrestre: True
>     - Possui garras retráteis: True
>     - O que o felino esta fazendo:
>         O felino esta caçando!
> 
> - Jaguar:
>     - É terrestre: True
>     - Possui garras retráteis: True
>     - O que o felino esta fazendo:
>         O felino esta caçando!
> ```

## Métodos de classe

**animal.py**

```python
class Animal:
    voador = True

    def __init__(self, nome):
        self.nome = nome

class Crocodilo(Animal):
    """
    A diferença dos métodos de classe para
    os métodos estáticos é que os métodos de
    classe podem acessar atributos e métodos
    da classe pai.
    """
    @classmethod
    def new(cls, nome): # cls = classe
        cls.voador = False
        return Crocodilo(nome)

crocodilo = Crocodilo.new('coco')
print(crocodilo.nome)
print(crocodilo.voador)
```

> **Saída:**
> 
> ```
> $ python3 animal.py 
> coco
> False
> ```

## Override (sobrescrita de métodos)

***animal.py***

```python
class Animal:
    @property
    def terrestre(self):
        return True

class Felino(Animal):
    @property
    def garras_retrateis(self):
        return True
    def perseguir(self):
        print('O felino esta caçando!')

class Mascote:
    def __init__(self, nome):
        self.nome = nome

    def mostrar_nome(self):
        print(self.nome)

class Gato(Felino, Mascote):
    def __init__(self, nome):
        Mascote.__init__(self, 'Garfield')
        self.nome_do_gato = nome

    def gato_perseguidor(self):
        self.perseguir()

    def mostrar_nome(self):
        """
        A instrução abaixo usa específicamente
        o método da classe 'Mascote'
        """
        Mascote.mostrar_nome(self)
        print(f"O nome do gato é: {self.nome_do_gato}")

gato = Gato('Frajola')
"""
Busca o método 'mostrar_nome()'
na instância da classe 'Gato'
caso não a encontre é procurado
nas classes herdadas da esquerda
para direita (Felino, Mascote).
"""
gato.mostrar_nome()
```

> **Saída:**
> 
> ```
> $ python3 animal.py 
> Garfield
> O nome do gato é: Frajola
> ```

## Classes - Curiosidades

```python
class Usuario:
    pass

usuario = Usuario()

# Retorna: {}
print(usuario.__dict__)
# Cria um atributo para a classe 'Usuario'
usuario.nome = 'Fulano' 
# Retorna: {'nome': 'Fulano'}
print(usuario.__dict__)
# Imprime: Fulano
print(usuario.nome)
```

*** usuario.py***

```python
class Usuario:
    def __init__(self):
        self.__password = 'senha secreta.'

    def mostrar_password(self):
        print(f"""
\t- Retorno da função 'mostrar_password()':\n
\t\t{self.__password}\n""")

usuario = Usuario()
usuario.__password = 'senha não tão secreta.'

print(usuario.__dict__)

usuario.mostrar_password()

print(f"""
\t- Atributo de instância 'usuario.__password':\n
\t\t{usuario.__password}\n""")
```

> Na saída observamos dois atributos (ambos diferentes): `_Usuario__password` e `__password` o primeiro privado (criado na própria classe) o segundo é público (criado pela instância).
> 
> **Obs.:** O prefixo `_Usuario` que inicia o atributo: `_Usuario__password` indica que se trata de uma atributo privado.
> 
> ```
> $ python3 usuario.py 
> {'_Usuario__password': 'senha secreta.', '__password': 'senha não tão secreta.'}
> 
>     - Retorno da função 'mostrar_password()':
> 
>         senha secreta.
> 
> 
>     - Atributo de instância 'usuario.__password':
> 
>         senha não tão secreta.
> ```

## Métodos mágicos também conhecidos como métodos Dunder

Método mágicos são métodos já estabelecidos em python que se iniciam com dois underlines e terminam com dois underlines tal como `__init__` que podemos usar para inicializar atributos ou executar métodos de suma importância, no entanto, o método `__init__` não é o construtor de uma classe, mas sim, o método `__new__`.

***usuario.py***

```python
class Usuario:
    def __new__(cls):
        print('Método \'__new__\' é o primeiro que se executa.')
        # '__new__' precisa retornar algo.
        return super().__new__(cls)

    def __init__(self):
        print('Método \'__init__\' é o segundo que se executa.')

usuario = Usuario()
```

> **Saída:**
> 
> ```
> $ python3 usuario.py 
> Método '__new__' é o primeiro que se executa.
> Método '__init__' é o segundo que se executa.
> ```

Quando inclu-o uma instrunção print para imprimir um objeto obtemos o espaço de memória ocupado pelo referido objeto.

***usuario.py***

```python
class Usuario:
    def __new__(cls):
        print('Método \'__new__\' é o primeiro que se executa.')
        # '__new__' precisa retornar algo.
        return super().__new__(cls)

    def __init__(self):
        print('Método \'__init__\' é o segundo que se executa.')

usuario = Usuario()
# Imprime o espaço de memória do objeto.
print(usuario)
```

> **Saída:**
> 
> ```
> $ python3 usuario.py 
> Método '__new__' é o primeiro que se executa.
> Método '__init__' é o segundo que se executa.
> <__main__.Usuario object at 0x7f2cb0ad6c50>
> ```

Alterando a saída padrão que imprime o espaço de memória do objeto:

***usuario.py***

```python
class Usuario:
    def __new__(cls):
        print('Método \'__new__\' é o primeiro que se executa.')
        # '__new__' precisa retornar algo.
        return super().__new__(cls)

    def __init__(self):
        print('Método \'__init__\' é o segundo que se executa.')

    def __str__(self):
        # '__str__' sempre precisa retornar uma string.
        return 'Esta é a saída quando imprimo um objeto'

usuario = Usuario()
print(usuario)
```

> **Saída:**
> 
> ```
> $ python3 usuario.py 
> Método '__new__' é o primeiro que se executa.
> Método '__init__' é o segundo que se executa.
> Esta é a saída quando imprimo um objeto
> ```

Quando acessamos um atributo que não se encontra na classe ocorre um erro, para evitar esse erro usamos o método `__getattr__` onde também podemos chamar outro método se for necessário.

***usuario.py***

```python
class Usuario:
    def __new__(cls):
        print('Método \'__new__\' é o primeiro que se executa.')
        # '__new__' precisa retornar algo.
        return super().__new__(cls)

    def __init__(self):
        print('Método \'__init__\' é o segundo que se executa.')

    def __str__(self):
        # '__str__' sempre precisa retornar uma string.
        return 'Esta é a saída quando imprimo um objeto'

    # __getattr__ guando acessamos atributo que não se encontra.
    def __getattr__(self, nome): 
        print('Atributo não se encontra!')
        self.outro_metodo()

    def outro_metodo(self):
        print('Podemos executar outro método!')

usuario = Usuario()

print(usuario)

print(usuario.apelido)
```

> **Saída:**
> 
> ```
> $ python3 usuario.py 
> Método '__new__' é o primeiro que se executa.
> Método '__init__' é o segundo que se executa.
> Esta é a saída quando imprimo um objeto
> Atributo não se encontra!
> Podemos executar outro método!
> None
> ```

## Pacotes

Pacotes nada mais são que pastas que contém módulos necessários ao nosso script (`main.py`) principal, por usa vez módulos são arquivos com extenção `.py`, arquivos estes que são nossas classes. Os módulos para que não fiquem dispersos é criado uma pasta com um nome que tenha haver com o contexto de nossa aplicação, esta pasta deverá conter um arquivo `__init__.py` para que configure se tratar de um pacote.

```
.
├── main.py
└── animais
    ├── __init__.py
    └── gato.py
```

### main.py

```python
from animais.gato import Gato

gato = Gato('Frajola')
print(gato.nome)
```

### gato.py

```python
class Gato:
  def __init__(self, nome):
    self.nome = nome
```

> **Saída:**
>
> ```
> $ python3 main.py 
> Frajola
> ```
>
> Ao executar o `main.py` pela primeira vez a árvore de diretório fica assim:
>
> ```
> .
> ├── main.py
> └── animais
>     ├── __init__.py
>     ├── gato.py
>     └── __pycache__
>         ├── __init__.cpython-39.pyc
>         └── gato.cpython-39.pyc
>  
> ```
>
> É criado a pasta `__pycache__` com a compilação em bytecode de `__init__.py` e de `gato.py` para que na próxima vez a execução seja mais rápida.

## Pacotes (arquivo `__init__`)

Com relação a importação:

```python
from animais.gato import Gato
```

Esta não é a melhor forma de importar pacotes, dai entra o arquivo `__init__` dentro deste arquivo colocaremos todos os módulos que necessitamos importar:

```python
"""
O ponto antes do módulo significa o diretório
corrente onde se encontra os módulos.
"""
from .gato import Gato
```

E no arquivo `main.py`:

```python
# from animais.gato import Gato
from animais import Gato

gato = Gato('Frajola')
print(gato.nome)
```

Arquivo `gato.py`:

```python
class Gato:
  def __init__(self, nome):
    self.nome = nome
```

> **Saída:**
> 
> ```
> $ python3 main.py 
> Frajola
> ```

O arquivo `__init__` não esta limitado ao que vimos acima, podemos também agregar outras funcionalidades a este arquivo:

```python
from .gato import Gato

"""
Agregando outras funcionalidades
ao arquivo __init__.py
"""

CONSTANTE = 'Esta é uma constante'

def criador_gatos(nome):
  return Gato(nome)

"""
Podemos também colocar
Laços for e etc...
"""
```

E no arquivo `main.py`:

```python
from animais import Gato
from animais import CONSTANTE
from animais import criador_gatos

# gato = Gato('Frajola')
gato = criador_gatos('Frajola')
print(gato.nome)
print(CONSTANTE)
```

> **Saída:**
> 
> ```
> $ python3 main.py 
> Frajola
> Esta é uma constante
> ```

## SubPacotes:

Continuando com o exemplo anterior se criarmos outras classes para outros animais tais como: aves, répteis e etc... Teríamos animais de diferentes contextos e para que fique melhor organizado criamos subpacotes para os diferentes contextos:

**Exemplo:**

```
.
├── main.py
└── animais
    ├── __init__.py
    ├── aves
    │   ├── __init__.py
    │   ├── galinha.py
    │   └── pato.py
    ├── felinos
    │   ├── __init__.py
    │   ├── gato.py
    │   └── leao.py
    └── repteis
        ├── __init__.py
        ├── jabuti.py
        └── lagarto.py
```

Conteúdo de `felinos/__init__.py`:

```python
from .gato import Gato
from .leao import Leao
```

Conteúdo de `animais/__init__.py`:

```python
from .felinos import Gato
from .felinos import Leao
```

Em `gato.py`:

```python
class Gato:
  def __init__(self, nome):
    self.nome = nome
```

Em `leao.py`:

```python
class Leao:
  def __init__(self, nome):
    self.nome = nome
```

E no `main.py`:

```python
from animais import Gato
from animais import Leao

gato = Gato('Frajola')
leao = Leao('Lion')

print(gato.nome)
print(leao.nome)
```

> **Saída:**
> 
> ```
> $ python3 main.py 
> Frajola
> Lion
> ```

## Raise - Criando nossas próprias exceções

Tradução de `raise` é levantar, logo, `raise` significa: **'levantando'**, **'subindo'** ou **'provocando'** uma exceção.

```python
class TinyIntError(Exception):
    pass

def tiny_int(val):
    return val >= 0 and val <= 255

try:
    numero = 400
    if tiny_int(numero):
        print('O número é correto')
    else:
        raise TinyIntError('Esta é uma mensagem para os números que não são TinyInt.')

except TinyIntError as error:
    print(error)
```

> **Saída:**
>
> ```
> $ python3 main.py
> Esta é uma mensagem para os números que não são TinyInt.
> ```

### Melhorando o script anterior:

### `main.py`

```python
# Classe TinyIntError
class TinyIntError(Exception):
	def __init__(self): # Define mensagem padrão.
		self.message = 'O número não conta com as características de um número tinyInt'
	def __str__(self): # Subscreve string de retorno de erro.
		return self.message

# Realizando as validações para 'val'
def validate_tiny_int(val):
	return val >= 0 and val <= 255

def validate_val(val):
	try:
		"""
		A função integrada: 'isinstance(object, classinfo)'
		checa se o 'object' é do tipo especificado.
		No 'return' abaixo 'val' é convertido para
		inteiro 'int(val)' e depois checa se é do tipo 'int'.
		"""
		return isinstance(int(val), int)
		"""
		Se a erro ocorrer na converção 'int(val)'
		entra na excessão abaixo e retorna 'False'.
		"""
	except ValueError as error:
		return False

# Função que testa 'val'
def tiny_int(val):
	try:
		if validate_val(val) and validate_tiny_int(val):
			return True
		else:
			raise TinyIntError()
	except TinyIntError as error:
		return error

print(f'400 = {tiny_int(400)}')
print(f'55 = {tiny_int(55)}')
```

> **Saída:**
>
> ```
> $ python3 main.py 
> 400 = O número não conta com as características de um número tinyInt
> 55 = True
> ```

### Empacotando o exemplo anterior

```
.
├── main.py
└── modulos
    ├── __init__.py
    ├── tinyIntError.py
    └── validates.py
```

### `main.py`

```python
from modulos import TinyIntError

tinyInt = TinyIntError()

print(f'400 = {tinyInt.tiny_int(400)}')
print(f'55 = {tinyInt.tiny_int(55)}')
```

### `modulos/__init__.py`

```python
from .tinyIntError import TinyIntError
```

### `modulos/tinyIntError.py`

```python
from .validates import validate_val, validate_tiny_int

class TinyIntError(Exception):
    message = 'O número não conta com as características de um número tinyInt'

    def __int__(self, val = 0):
        self.val = val

    def __str__(self): # Subscreve string de retorno de erro.
        return self.message

    def tiny_int(self, val):
        self.val = val
        try:
            if validate_val(self.val) and validate_tiny_int(self.val):
                return True
            else:
                raise TinyIntError()
        except TinyIntError as error:
            return error
```

### `modulos/validates.py`

```python
def validate_tiny_int(val):
    return val >= 0 and val <= 255

def validate_val(val):
    try:
        return isinstance(int(val), int)
    except ValueError as error:
        return False
```

> **Saída:**
>
> ```bash
> $ python3 main.py 
> 400 = O número não conta com as características de um número tinyInt
> 55 = True
> ```
