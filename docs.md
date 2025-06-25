# Documentação API Grow Integração

Esta documentação descreve os endpoints disponíveis na API de integração da Grow, seus parâmetros e exemplos de uso.

## Sumário

- [Documentação API Grow Integração](#documentação-api-grow-integração)
  - [Sumário](#sumário)
  - [Autenticação](#autenticação)
  - [URL Base](#url-base)
  - [Endpoints](#endpoints)
    - [Pedidos](#pedidos)
      - [Listar Pedidos](#listar-pedidos)
      - [Listar Pedidos Por Id](#listar-pedidos-por-id)
      - [Pedidos Integração Retorno](#pedidos-integração-retorno)
    - [Clientes](#clientes)
      - [Listar Clientes](#listar-clientes)
      - [Listar Clientes Por Id](#listar-clientes-por-id)
      - [Clientes Integração Retorno](#clientes-integração-retorno)
  - [Dicas de Uso](#dicas-de-uso)
  - [Ferramentas Recomendadas](#ferramentas-recomendadas)

## Autenticação

A API utiliza autenticação Basic Auth. É necessário incluir as credenciais em todas as requisições.

**Credenciais:**
- **Username:** seu_usuario
- **Password:** sua_senha

## URL Base

```
http://54.207.130.71:4020/api/
```

## Endpoints

### Pedidos

#### Listar Pedidos

Retorna uma lista de pedidos.

**Método:** GET  
**Endpoint:** `/pedidos/{pagina}`

**Parâmetros de URL:**
- `pagina` (obrigatório): Número da página para paginação dos resultados

**Exemplo de requisição:**
```http
GET http://54.207.130.71:4020/api/pedidos/1
```

#### Listar Pedidos Por Id

Retorna informações detalhadas de um pedido específico.

**Método:** GET  
**Endpoint:** `/pedidos/id/{id}`

**Parâmetros de URL:**
- `id` (obrigatório): ID do pedido a ser consultado

**Exemplo de requisição:**
```http
GET http://54.207.130.71:4020/api/pedidos/id/1
```

**Exemplo de retorno:**

```json
{
    "page": 1,
    "total_pages": 57,
    "data": [
        {
            "id": 1, // ID interno do pedido, use esse id para consultar o pedido de forma mais específica
            "total": "282.00",
            "frete": "0.00",
            "status": "ET", // CA - Cancelado, ET - Entregue, EV - Enviado, PG - Pago, EP - Em produção
            "total_venda": "399.90",
            "subtotal_venda": "699.99",
            "observacoes": "Cliente pediu para entrar em contato quando estiver em rota.",
            "id_integrador": "",
            "status_integracao": "N", // N = Não Integrado, I = Integrado
            "observacoes_integracao": "",
            "dthr_registro": "2025-03-01 14:02:09",
            "cliente": {
                "nome": "CLAÙDIA JAKELINE RIBEIRO DE CASTRO",
                "documento": "59957433253",
                "email": "claudia_jakeline@hotmail.com",
                "telefone": "(92)99477-8181",
                "id_integrador": "",
                "status_integracao": "",
                "observacoes_integracao": "",
                "endereco": {
                    "cep": "69076660",
                    "endereco": "RUA FRANKLIN TÁVORA",
                    "numero": "N 1874",
                    "bairro": "JAPIIM",
                    "cidade": "MANAUS",
                    "estado": "AM",
                    "complemento": "",
                    "local": "Casa"
                }
            },
            "fornecedor": {
                "nome": "Delicatto Moveis",
                "documento": "24600810000228",
                "razao_social": "GSP DO BRASIL LTDA",
                "logomarca": "delicatto.jpg"
            },
            "itens": [
                {
                    "descricao": "ROUPEIRO MONACO 1,80 X 0,73 X 0,37M BRANCO",
                    "codigo_sku": "113186",
                    "codigo_gtin": "040114116748",
                    "codigo_mpn": "113186",
                    "codigo_ncm": "44111490",
                    "quantidade": "1.000",
                    "valor_unitario": "282.00",
                    "valor_total": "282.00"
                }
            ],
            "venda": {
                "total_produtos": "699.99", // Total dos produtos na venda
                "total_frete": "0.00", // Total do frete
                "total_desconto": "300.09", // Total de desconto aplicado
                "total_venda": "399.90", // Total da venda após descontos
                "itens": [] // Lista de itens da venda, cada item deve conter: descricao, codigo_sku, codigo_gtin, codigo_mpn, codigo_ncm, quantidade, valor_unitario, valor_total
            },
            "loja": {
                "id": 1,
                "nome": "Loja Exemplo",
                "cnpj": "12.345.678/0001-90",
                "endereco": "Rua Exemplo, 123",
                "cidade": "Cidade Exemplo",
                "estado": "SP"
            },
            "pagamentos": [
                {
                    "forma": "Cartão de Crédito", // Formas de pagamento: "Cartão de Crédito", "Cartão Débito", "Pix loja", "Pix fornecedor", "Dinheiro"
                    "valor_pago": "399.90", // Valor pago pelo cliente,
                    "qtd_parcela": 5, // Quantidade de parcelas
                    "valor_parcela": 79.98, // Valor de cada parcela
                    "codigo_sankhya": 7 // Código do tipo de pagamento no Sankhya
                }
            ]
        }
    ]
}
```

#### Pedidos Integração Retorno

Atualiza o status de integração de um pedido.

**Método:** POST  
**Endpoint:** `/pedidos/retorno/{id}`

**Parâmetros de URL:**
- `id` (obrigatório): ID do pedido a ser atualizado

**Corpo da Requisição:**
```json
{
    "id_integrador": 1525,
    "status": "integrado", // valores possíveis: "integrado" ou "pendente"
    "observacoes": "Teste de Integração" // Opcional
}
```

**Exemplo de requisição:**
```http
POST http://54.207.130.71:4020/api/pedidos/retorno/25
{
    "id_integrador": 1525,
    "status": "integrado",
    "observacoes": "Teste de Integração"
}
```

### Clientes

#### Listar Clientes

Retorna uma lista de clientes.

**Método:** GET  
**Endpoint:** `/clientes/{pagina}`

**Parâmetros de URL:**
- `pagina` (obrigatório): Número da página para paginação dos resultados

**Exemplo de requisição:**
```http
GET http://54.207.130.71:4020/api/clientes/25
```

#### Listar Clientes Por Id

Retorna informações detalhadas de um cliente específico.

**Método:** GET  
**Endpoint:** `/clientes/id/{id}`

**Parâmetros de URL:**
- `id` (obrigatório): ID do cliente a ser consultado

**Exemplo de requisição:**
```http
GET http://54.207.130.71:4020/api/clientes/id/25
```

#### Clientes Integração Retorno

Atualiza o status de integração de um cliente.

**Método:** POST  
**Endpoint:** `/clientes/retorno/{id}`

**Parâmetros de URL:**
- `id` (obrigatório): ID do cliente a ser atualizado

**Corpo da Requisição:**
```json
{
    "id_integrador": 1525,
    "status": "integrado", // valores possíveis: "integrado" ou "pendente"
    "observacoes": "Teste de Integração" // Opcional
}
```

**Exemplo de requisição:**
```http
POST http://54.207.130.71:4020/api/clientes/retorno/25

{
    "id_integrador": 1525,
    "status": "integrado",
    "observacoes": "Teste de Integração"
}
```

## Dicas de Uso

1. Certifique-se de enviar as credenciais corretas em todas as requisições usando Basic Auth.
2. Para consultar uma lista paginada de pedidos ou clientes, use os endpoints `/pedidos/{pagina}` ou `/clientes/{pagina}`.
3. Para obter detalhes específicos de um pedido ou cliente, use os endpoints `/pedidos/id/{id}` ou `/clientes/id/{id}`.
4. Para atualizar o status de integração, use os endpoints de retorno com o método POST e inclua os dados necessários no corpo da requisição.

## Ferramentas Recomendadas

Para testar esta API, você pode utilizar:

- Postman: Interface gráfica para testes de API
- cURL: Ferramenta de linha de comando para transferência de dados
- Qualquer biblioteca HTTP na linguagem de sua preferência
