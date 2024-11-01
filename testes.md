# Testando Função de Soma com `pytest`

Esta página apresenta uma introdução sobre como realizar testes de software usando casos de teste para a função `soma`. Abordamos classes de equivalência e análise de valor limite, e a prática de criação de testes usando `pytest`.

## Explicação de Casos de Teste para a Função `soma`

Vamos definir e explicar os casos de teste essenciais para uma função `soma` que recebe dois valores inteiros e retorna a soma deles. Essa função será testada para diferentes tipos de entradas para garantir que funcione corretamente em diversos cenários.

### 1. Casos Básicos

- **Valores positivos**  
   - Exemplo: `soma(2, 3)` → Saída esperada: `5`
   - Objetivo: Verificar que a função soma corretamente dois números inteiros positivos.

- **Valores negativos**  
   - Exemplo: `soma(-2, -3)` → Saída esperada: `-5`
   - Objetivo: Validar que a função trata adequadamente a soma de dois números negativos.

- **Zero e valor positivo**  
   - Exemplo: `soma(0, 5)` → Saída esperada: `5`
   - Objetivo: Testar que zero não afeta o valor positivo na soma.

- **Zero e valor negativo**  
   - Exemplo: `soma(0, -5)` → Saída esperada: `-5`
   - Objetivo: Garantir que zero não altera o valor negativo na soma.

- **Valores mistos (positivo e negativo)**  
   - Exemplo: `soma(5, -3)` → Saída esperada: `2`
   - Objetivo: Confirmar que a função soma corretamente valores de sinais opostos.

### 2. Casos Limite

Para testar a robustez da função `soma`, é importante verificar como ela se comporta com valores no limite dos inteiros.

- **Limite superior**  
   - Exemplo: `soma(2147483647, 1)` → Saída esperada: `2147483648` (se o sistema suporta valores maiores)
   - Objetivo: Testar como a função reage ao maior valor de um inteiro comum (32 bits).

- **Limite inferior**  
   - Exemplo: `soma(-2147483648, -1)` → Saída esperada: `-2147483649` (ou erro de overflow)
   - Objetivo: Checar como a função lida com o menor valor possível para um inteiro.

### 3. Casos Especiais

Casos adicionais ajudam a cobrir situações específicas que podem ser encontradas na prática.

- **Dois valores zero**  
   - Exemplo: `soma(0, 0)` → Saída esperada: `0`
   - Objetivo: Confirmar que somar dois zeros resulta em zero.

- **Valores máximos opostos**  
   - Exemplo: `soma(2147483647, -2147483648)` → Saída esperada: `-1`
   - Objetivo: Garantir que a função trata valores extremos de sinais opostos.

- **Grande disparidade**  
   - Exemplo: `soma(1, -1000000)` → Saída esperada: `-999999`
   - Objetivo: Testar a função com números de magnitudes muito diferentes.

| Caso de Teste                            | Entrada               | Saída Esperada |
|------------------------------------------|-----------------------|----------------|
| Soma de dois valores positivos           | `soma(2, 3)`         | `5`            |
| Soma de dois valores negativos           | `soma(-2, -3)`       | `-5`           |
| Soma de zero e um valor positivo         | `soma(0, 5)`         | `5`            |
| Soma de zero e um valor negativo         | `soma(0, -5)`        | `-5`           |
| Soma de valores mistos (positivo e negativo) | `soma(5, -3)` | `2`            |
| Soma no limite superior do tipo inteiro  | `soma(2147483647, 1)`| Overflow ou `2147483648`|
| Soma no limite inferior do tipo inteiro  | `soma(-2147483648, -1)`| Overflow ou `-2147483649`|
| Soma de dois zeros                       | `soma(0, 0)`         | `0`            |
| Valores máximos opostos                  | `soma(2147483647, -2147483648)`| `-1`|
| Grande disparidade                       | `soma(1, -1000000)`  | `-999999`      |

## Implementando os Casos de Teste com `pytest`

Vamos criar uma função `soma` e os testes em `pytest`.

### 1. Função `soma`

No arquivo `soma.py`, definimos a função `soma`:

```python
def soma(a, b):
    return a + b
```


No arquivo test_soma.py, escrevemos os casos de teste explicados anteriormente. Estes testes cobrem as entradas básicas, os limites e casos especiais.


```python
from soma import soma
import pytest

def test_soma_valores_positivos():
    assert soma(2, 3) == 5

def test_soma_valores_negativos():
    assert soma(-2, -3) == -5

def test_soma_zero_e_positivo():
    assert soma(0, 5) == 5

def test_soma_zero_e_negativo():
    assert soma(0, -5) == -5

def test_soma_valores_mistos():
    assert soma(5, -3) == 2

def test_soma_limite_superior():
    assert soma(2147483647, 1) == 2147483648

def test_soma_limite_inferior():
    assert soma(-2147483648, -1) == -2147483649

def test_soma_dois_zeros():
    assert soma(0, 0) == 0

def test_soma_valores_maximos_opostos():
    assert soma(2147483647, -2147483648) == -1

def test_soma_grande_disparidade():
    assert soma(1, -1000000) == -999999
```