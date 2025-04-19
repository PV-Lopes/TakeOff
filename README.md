# 🧠 Desafio de Prompt Engineering com ChatGPT

Este documento apresenta a resolução do **Desafio de Prompt Engineering**.
---

## Questão 1: Como o algoritmo de Ray Tracing calcula a cor de um pixel

**Técnica Utilizada:** Chain of Thought  
**Prompt Utilizado:**

> Explique passo a passo como o algoritmo de Ray Tracing calcula a cor de um pixel em uma imagem renderizada. Comece com o conceito de emissão de raios da câmera, passando por interseção com objetos, cálculo de iluminação, reflexões, refrações e composição final da cor. Use uma abordagem didática.

**Resposta da IA:**

1. **Emissão do Raio (Ray Generation)**: Um raio é lançado da câmera para cada pixel da imagem.
2. **Interseção com Objetos**: O algoritmo detecta colisões entre o raio e os objetos na cena.
3. **Cálculo de Iluminação**: Se houver colisão, calcula-se luz ambiente, luz direta e sombras.
4. **Reflexão e Refração**: Raios secundários são lançados para simular superfícies reflexivas ou transparentes.
5. **Recursão**: O processo se repete para os raios secundários.
6. **Composição Final**: A cor do pixel é uma combinação das contribuições dos diversos raios.
7. **Anti-Aliasing (opcional)**: Técnicas adicionais suavizam a imagem final.

---

## Questão 2: Decomposição numérica de 142.981

**Técnica Utilizada:** Zero-Shot + CIDI  
**Prompt Utilizado:**

> Explique como fazer a decomposição numérica do número 142.981 em suas ordens (centena de milhar, dezena de milhar, milhar, centena, dezena e unidade). Forneça o contexto da decomposição, a ideia por trás dela, detalhamento de cada etapa e exemplos semelhantes no final.

**Resposta da IA:**

### C - Contexto:
A decomposição numérica ajuda a entender o valor de cada dígito em sua posição decimal.

### I - Ideia:
Separar o número nas suas ordens: centena de milhar, dezena de milhar, milhar, centena, dezena e unidade.

### D - Detalhamento:
plaintext
142.981 = 100.000 + 40.000 + 2.000 + 900 + 80 + 1
I - Iteração (Exemplo adicional):
plaintext
Copiar
Editar
85.673 = 80.000 + 5.000 + 600 + 70 + 3

---

## Questão 3: Personagens maquiavélicos em As Crônicas de Gelo e Fogo

**Técnica Utilizada:** Few-Shot + Contextualização Filosófica
**Prompt Utilizado:**

> Quais personagens de "As Crônicas de Gelo e Fogo" possuem traços inspirados nos ensinamentos de Nicolau Maquiavel? Considere princípios da obra "O Príncipe", como o uso da astúcia, da manipulação política, do pragmatismo e da busca pelo poder a qualquer custo. Exemplifique com 2 a 3 personagens, como Petyr Baelish, Cersei Lannister ou Tyrion, e explique como cada um aplica conceitos maquiavélicos.

**Resposta da IA:**

Petyr Baelish (Mindinho)
Mestre da manipulação e das intrigas.

Usa o caos como escada para o poder.

Representa o maquiavelismo clássico: o fim justifica os meios.

Cersei Lannister
Usa o medo e o controle para manter o poder.

Exemplo: Explosão do Septo de Baelor para eliminar adversários.

Tyrion Lannister
Inteligente e estrategista.

Pragmático ao lidar com alianças e traições.

Age de forma maquiavélica para sobreviver e influenciar.

---

## Questão 4: Endpoint FastAPI com validação e UUID

**Técnica Utilizada:** Zero-Shot + Prompt técnico estruturado
**Prompt Utilizado:**

> Crie um endpoint usando FastAPI em Python que aceite um objeto do tipo Item com os seguintes campos:

> nome: string, máximo de 25 caracteres.

> valor: float

> data: do tipo date, não pode ser superior à data atual.

> O endpoint deve:

> Validar os campos recebidos conforme os requisitos acima.

> Retornar o corpo da requisição junto com um campo adicional chamado uuid, contendo um identificador único gerado dinamicamente.

> Forneça o código completo, incluindo os imports necessários.

**Resposta da IA (código):**

python
Copiar
Editar
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel, Field, validator
from uuid import uuid4
from datetime import date

app = FastAPI()

class Item(BaseModel):
    nome: str = Field(..., max_length=25)
    valor: float
    data: date

    @validator("data")
    def validar_data(cls, v):
        if v > date.today():
            raise ValueError("A data não pode ser superior à data atual.")
        return v

@app.post("/item")
def processar_item(item: Item):
    return {
        "nome": item.nome,
        "valor": item.valor,
        "data": item.data,
        "uuid": str(uuid4())
    }
