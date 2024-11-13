# Global Solution FIAP S2/2024 - SunnyMeter 
Projeto Global Solution para a disciplina de "Domain Driven Design com Java", para os cursos de Engenharia de Software - FIAP/SP, 2024. 

Por: Professor Fellipe Souto.

- [Global Solution FIAP S2/2024 - SunnyMeter](#global-solution-fiap-s22024---sunnymeter)
- [Introdução](#introdução)
- [O Projeto](#o-projeto)
  - [Entidade: Cliente](#entidade-cliente)
  - [Entidade: Instalação](#entidade-instalação)
  - [Entidade: Contrato](#entidade-contrato)
  - [Entidade: Registro de Consumo](#entidade-registro-de-consumo)
  - [Entidade: Registro de Produção](#entidade-registro-de-produção)
- [Regras de negócio](#regras-de-negócio)
  - [Regras de negócio: Cliente](#regras-de-negócio-cliente)
  - [Regras de negócio: Instalação](#regras-de-negócio-instalação)
  - [Regras de negócio: Contrato](#regras-de-negócio-contrato)
  - [Regras de negócio: Registro de Consumo](#regras-de-negócio-registro-de-consumo)
  - [Regras de negócio: Registro de Geração](#regras-de-negócio-registro-de-geração)
- [Especificação da API](#especificação-da-api)
  - [API de Clientes](#api-de-clientes)
  - [API de Instalações](#api-de-instalações)
  - [API de Contratos (WIP)](#api-de-contratos-wip)
  - [API de Registro de Consumo \& Registro de Produção (WIP)](#api-de-registro-de-consumo--registro-de-produção-wip)
- [Diretrizes para entrega do trabalho:](#diretrizes-para-entrega-do-trabalho)
- [Dicas e Considerações](#dicas-e-considerações)
- [Atualizações](#atualizações)
- [Referências úteis](#referências-úteis)


# Introdução

Na cidade de São Pedro do Sol Nascente a concessionária pública de energia elética (CPEEL) está lançando um novo dispositivo para seus clientes, um medidor de energia elétrica inteligente chamado SunnyMeter. Esse dispositivo será capaz de ler em tempo real o consumo de energia da residência e enviar diretamente para o servidor da concessionária essa informação. Com isso, será possível acompanhar o consumo de cada instalação de forma sofisticada, podendo até mesmo estimar o gasto de um cliente através do seu padrão de consumo.

Além de monitorar a energia consumida pela instalação, o cliente poderá instalar pequenos geradores de energia elétrica, como painéis solares, rodas d'agua e/ou moinhos de vento, e vender de volta a energia produzida, tudo controlado pelo SunnyMeter. Esse processo de geração de energia pelos clientes recebe o nome de "Geração distribuída", e é uma das grandes promessas da CPEEL para uma produção e consumo de energia elétrica mais limpa e sustentável para o futuro.

> Geração distribuída (GD), também chamada de geração descentralizada, é a geração e armazenamento elétrico realizado por uma variedade de dispositivos pequenos, conectados à rede ou conectados ao sistema de distribuição.
> 
> Usinas de geração de energia convencionais, como usinas movidas a carvão, gás e energia nuclear, bem como represas hidrelétricas e usinas de energia solar de grande escala, são centralizadas e geralmente exigem que a energia elétrica seja transmitida por longas distâncias. Por outro lado, os sistemas distribuídos são tecnologias descentralizadas, modulares e mais flexíveis, localizadas próximas ao consumo, porém com capacidades menores. Esses sistemas podem incluir vários componentes de geração e armazenamento. Neste caso, eles são referidos como sistemas híbridos de energia.
> 
> Os sistemas GD normalmente usam fontes de energia renováveis, incluindo pequenas hidrelétricas, biomassa, biogás, energia solar, energia eólica e energia geotérmica, e cada vez mais desempenham um papel importante para o sistema de distribuição de energia elétrica . Por meio de uma interface, os sistemas de Energia distribuída podem ser gerenciados e coordenados dentro de uma rede inteligente . A geração e o armazenamento distribuídos permitem a coleta de energia de várias fontes e podem reduzir os impactos ambientais e melhorar a segurança do abastecimento.
>
> Fonte: [Geração distribuída](https://pt.wikipedia.org/wiki/Gera%C3%A7%C3%A3o_distribu%C3%ADda) (Wikipedia)

# O Projeto

Sua tarefa nesse projeto será desenvolver uma aplicação Java utilizando Spring Boot. Essa aplicação deverá expor um conjunto de endpoints, através dos quais será possível gerenciar diferentes entidades. O objetivo final do sistema será:

1. Cadastrar, listar, buscar e deletar clientes
2. Cadastrar, listar, buscar e deletar instalações
3. Cadastrar, listar, buscar e deletar contratos
4. Calcular o consumo de energia mensal em kW/h de um cliente
5. Calcular a produção de energia mensal em kW/h de um cliente

Cada entidade será apresentada e detalhada a seguir.

## Entidade: Cliente

Um cliente representa uma pessoa física ou jurídica que tenha um contrato de instalação ativa com a CPEEL. A seguir está detalhado os atributos que cada cliente deverá ter obrigatoriamente:

- Nome: O nome do cliente, podendo ser uma pessoa ou empresa.
  - ex: 
    - João da Silva; 
    - Gráficas Tamarindo S.A
- Identificador cliente UUID: Identificador único do tipo UUID que identifica unicamente um cliente de forma global e não previsível
  - ex:
    - 7da41106-5109-45f4-8d09-9ca405c33e5c
    - 84b4b063-58a4-4dab-bf4f-fd13954c328c
- Endereço: O endereço completo do cliente
  - ex:
    - Rua das Flores, 41
    - Avenida Lins da Cunha, 51 4 Andar, Sala 10
- Documento: CPF/CNPJ do cliente
  - ex:
    - 966.351.800-60
    - 35.142.208/0001-20
- Tipo Cliente: Diz se o cliente é PF ou PJ
- CEP: O CEP do endereço do cliente
  - ex:
    - 055345-120
    - 010034-000
- Ativo: Flag booleana que diz se o cliente está com o cadastro ativo ou não

## Entidade: Instalação

Uma instalação representa um único medidor SunnyMeter instalado. Nas propriedades do cliente.

- Número instalação UUID: Identificador único do tipo UUID que identifica unicamente uma instalação de forma global e não previsível
  - ex:
    - 7da41106-5109-45f4-8d09-9ca405c33e5c
    - 84b4b063-58a4-4dab-bf4f-fd13954c328c
- Endereço: O endereço completo da instalação
  - ex:
    - Rua das Flores, 41
    - Avenida Lins da Cunha, 51 4 Andar, Sala 10
- CEP: O CEP do endereço da instalação
  - ex:
    - 055345-120
    - 010034-000
- Ativo: Flag booleana que diz se a instalação está com o cadastro ativo ou não

## Entidade: Contrato

Um contrato é a combinação entre um cliente ativo e uma instalação ativa.

- Identificador cliente UUID: Identificador único de um cliente (Chave estrangeira)
- Número da instalação UUID: Identificador único do tipo UUID que representa a instalação (Chave estrangeira)
- Data de início: Data inicial do contrato
- Duração contrato: A duração do contrato em dias.
- Ativo: Flag booleana que diz se o contrato está ativo ou não
- Identificador contrato UUID: Identificador único do tipo UUID que representa o contrato.

## Entidade: Registro de Consumo

Um registro de consumo representa quanto que um cliente gastou de energia elétrica até dado momento.

- Identificador contrato UUID: Identificador único do tipo UUID que identifica unicamente um contrato de forma global e não previsível (Chave estrangeira)
- Consumo kWh: Número de ponto-flutuante positivo que representa quanto que o cliente gastou de energia elétrica até aquele dado momento em kiloWatt/hora.
- Medição Timestamp: Marcação de tempo de quando a medição foi feita, deve seguir o padrão Unix Timestamp

## Entidade: Registro de Produção

Um registro de produção representa quanto que um cliente produziu de energia elétrica até dado momento.

- Identificador contrato UUID: Identificador único do tipo UUID que identifica unicamente um contrato de forma global e não previsível (Chave estrangeira)
- Produção KWh: Número de ponto-flutuante positivo que representa quanto que o cliente gerou de energia elétrica até aquele dado momento em Kilowatss/hora.
- Medição Timestamp: Marcação de tempo de quando a medição foi feita, deve seguir o padrão Unix Timestamp

# Regras de negócio

Cada entidade terá um conjunto de regras de negócio para funcionar, espera-se que seja implementado todas as regras especificadas a seguir. Caso aja dúvida por parte do grupo ou alguma descrição fique superficial, ou em aberto, o grupo pode tirar dúvidas comigo, ou dar sua propria interpretação para o enunciado, desde que isso esteja descrito no relatório.

## Regras de negócio: Cliente

- Um cliente não deve ser apagado do banco de dados, apenas a flag "Ativo" deverá ser modificada. Chamamos isso de deleção lógica de registro.

## Regras de negócio: Instalação

- Um instalação não deve ser apagada do banco de dados, apenas a flag "Ativo" deverá ser modificada. Chamamos isso de deleção lógica de registro.

## Regras de negócio: Contrato

- Um contrato não deve ser apagado do banco de dados, apenas a flag "Ativo" deverá ser modificada. Chamamos isso de deleção lógica de registro.
- A vigência de um contrato deverá ser um múltiplo de 90, podendo ir de 90 dias a 810 dias.
- Um cliente e uma instalação poderão ter apenas um contrato ativo por vez.
- Passada toda a duração de um contrato este deverá ser considerado como não estando ativo

## Regras de negócio: Registro de Consumo

- O registro de consumo funciona através de um contador de consumo que está funcionando no SunnyMeter. A cada nova requisição para a API o registro de consumo deverá enviar um novo "Consumo KWh", que deverá ser maior do que o último enviado, bem como um timestamp posterior ao último enviado. Considere o exemplo prático a seguir:

```
{
    "instalacao_uuid": "7da41106-5109-45f4-8d09-9ca405c33e5c",
    "consumo_kwh: 410.90,
    "medicao_timestamp": 1731284100 // November 11, 2024 00:15:00 AM
}

{
    "instalacao_uuid": "7da41106-5109-45f4-8d09-9ca405c33e5c",
    "consumo_kwh: 418.90,
    "medicao_timestamp": 1731370500 // November 12, 2024 00:15:00 AM
}
```

O sistema deverá lidar com erros de leitura, como leituras que vieram fora de ordem. Para calcular o consumo mensal basta subtrair a primeira leitura do mês da última.

## Regras de negócio: Registro de Geração

- O registro de geração de energia funciona de forma análoga ao [Registro de Consumo](README.md#regras-de-negócio-registro-de-consumo), se baseie nele para extrair as funcionalidades do sistema.

# Especificação da API

## API de Clientes

```plain
URL: /clientes
MÉTODO: POST
DESCRIÇÃO: Cria um novo cliente a partir de um JSON

EXEMPLO 1:
INPUT SCHEMA:
{
    "nome": "joão da silva",
    "endereco": "Rua das Flores, 41",
    "documento": "966.351.800-60",
    "tipo": "PF",
    "cep": "055345-120"
}

OUTPUT SCHEMA:
{
    "cliente_uuid": "7da41106-5109-45f4-8d09-9ca405c33e5c",
    "nome": "joão da silva",
    "endereco": "Rua das Flores, 41",
    "documento": "966.351.800-60",
    "cep": "055345-120"
    "ativo": "true",
    "tipo": "PF"
}

EXEMPLO 2:
INPUT SCHEMA:
{
    "nome": "Gráficas Tamarindo S.A",
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "documento": "35.142.208/0001-20",
    "tipo": "PJ",
    "cep": "010034-000"
}

OUTPUT SCHEMA:
{
    "cliente_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
    "nome": "Gráficas Tamarindo S.A",
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "documento": "35.142.208/0001-20",
    "cep": "010034-000"
    "ativo": "true",
    "tipo": "PJ"
}

URL: /clientes
MÉTODO: GET
DESCRIÇÃO: Lista todos os clientes cadastrados

EXEMPLO 1:
OUTPUT SCHEMA:
[
    {
        "cliente_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
        "nome": "Gráficas Tamarindo S.A",
        "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
        "documento": "35.142.208/0001-20",
        "cep": "010034-000"
        "ativo": "true",
        "tipo": "PJ"
    },
    {
        "cliente_uuid": "7da41106-5109-45f4-8d09-9ca405c33e5c",
        "nome": "joão da silva",
        "endereco": "Rua das Flores, 41",
        "documento": "966.351.800-60",
        "cep": "055345-120"
        "ativo": "true",
        "tipo": "PF"
    },
    ...
]

URL: /clientes/<cliente-uuid>
MÉTODO: GET
DESCRIÇÃO: Busca um cliente específico pelo seu cliente_uuid

EXEMPLO 1:

URL: /clientes/84b4b063-58a4-4dab-bf4f-fd13954c328c
OUTPUT SCHEMA:
[
    {
        "cliente_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
        "nome": "Gráficas Tamarindo S.A",
        "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
        "documento": "35.142.208/0001-20",
        "cep": "010034-000"
        "ativo": "true",
        "tipo": "PJ"
    }
]

EXEMPLO 2:
URL: /clientes/123
OUTPUT SCHEMA:
[]

URL: /clientes/<cliente-uuid>
MÉTODO: DELETE
DESCRIÇÃO: Deleta logicamente um cliente específico através de seu cliente_uuid

EXEMPLO 1:

URL: /clientes/84b4b063-58a4-4dab-bf4f-fd13954c328c
OUTPUT SCHEMA:
{
    "cliente_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
    "nome": "Gráficas Tamarindo S.A",
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "documento": "35.142.208/0001-20",
    "cep": "010034-000"
    "ativo": "false",
    "tipo": "PJ"
}

```

## API de Instalações

```plain
URL: /instalacoes
MÉTODO: POST
DESCRIÇÃO: Cria uma nova instalacao a partir de um JSON

EXEMPLO 1:
INPUT SCHEMA:
{
    "endereco": "Rua das Flores, 41",
    "cep": "055345-120"
}

OUTPUT SCHEMA:
{
    "instalacao_uuid": "7da41106-5109-45f4-8d09-9ca405c33e5c",
    "endereco": "Rua das Flores, 41",
    "cep": "055345-120"
    "ativo": "true",
}

EXEMPLO 2:
INPUT SCHEMA:
{
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "cep": "010034-000"
}

OUTPUT SCHEMA:
{
    "instalacao_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "cep": "010034-000"
    "ativo": "true",
}

URL: /instalacoes
MÉTODO: GET
DESCRIÇÃO: Lista todos as instalacoes cadastrados

EXEMPLO 1:
OUTPUT SCHEMA:
[
  {
    "instalacao_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "cep": "010034-000"
    "ativo": "true",
    }
    ...
]

URL: /instalacoes/<instalacao-uuid>
MÉTODO: GET
DESCRIÇÃO: Busca uma instalacao específica pelo seu instalacao_uuid

EXEMPLO 1:

URL: /instalacoes/84b4b063-58a4-4dab-bf4f-fd13954c328c
OUTPUT SCHEMA:
[
    {
        "instalacao_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
        "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
        "cep": "010034-000"
        "ativo": "true",
    }
]

EXEMPLO 2:
URL: /instalacoes/123
OUTPUT SCHEMA:
[]

URL: /instalacaos/<instalacao-uuid>
MÉTODO: DELETE
DESCRIÇÃO: Deleta logicamente uma instalação específica através de seu instalacao_uuid

EXEMPLO 1:

URL: /instalacaos/84b4b063-58a4-4dab-bf4f-fd13954c328c
OUTPUT SCHEMA:
{
    "instalacao_uuid": "84b4b063-58a4-4dab-bf4f-fd13954c328c",
    "endereco": "Avenida Lins da Cunha, 51 4 Andar, Sala 10",
    "cep": "010034-000"
    "ativo": "false",
}
```

## API de Contratos (WIP)

## API de Registro de Consumo & Registro de Produção (WIP)

# Diretrizes para entrega do trabalho:

O presente trabalho terá sua nota dividida da seguinte forma:

- CÓDIGO: 80% de Peso
- DOCUMENTAÇÃO: 20% de Peso

Serão aceitos grupos de 1 a 4 pessoas. A correção do código será feita levando em consideração os seguintes pontos:

- Organização do código
- Legibilidade do código
- Corretudo do código
- Completude do código
- Tratamento de erros
- Testes manuais e automatizados
- Documentação do código e projeto

# Dicas e Considerações

- Estude os commits e códigos produzidos nas aulas.
- Discutam em grupo, apenas em consenso chegamos às melhores ideias.
- Não use chatGPT ou qualquer tipo de IA/ML, chatbot, LLM ou coisa afim. Seu uso acarretará em zero para todo o grupo.
- Não será tolerado plágios, um cientista de verdade compartilha e referencia suas fontes de forma correta. Não se constrói a Ciência de forma sozinha, apenas em comunidade. Faremos isso com cortêsia e consideração por aqueles que vieram antes de nós. Esse é o pensamento científico que adotaremos nessa e nas atividades futuras.
- Tirem dúvidas por e-mail comigo, costumo responder rápido
- Conversem entre vocês, mas não copiem um dos outros, isso também é plágio ;) .
- Se divirtam, esse é o objetivo final da ciência e desse trabalho:).

# Atualizações

- 12/11: Publicação versão 1
- 13/11: Atualizado especificação das Entidades Cliente, Instalação e Contrato


# Referências úteis

- [Unix timestamp](https://www.baeldung.com/java-retrieve-unix-time)
- [Physical vs. Logical Deletion of Database Records](https://www.baeldung.com/sql/physical-vs-logical-deletion)