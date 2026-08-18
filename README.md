# Console Financeiro

Um sistema de processamento de pagamentos desenvolvido em C# que demonstra conceitos fundamentais de Programação Orientada a Objetos, incluindo herança, polimorfismo e classes abstratas.

## Sobre o Projeto

Console Financeiro é uma aplicação console que simula um sistema de pagamentos com suporte a múltiplas formas de pagamento. O projeto foi desenvolvido como exercício prático de POO em C#, implementando um fluxo realista de processamento de transações financeiras com validações e cálculos específicos para cada tipo de pagamento.

O objetivo é demonstrar como sistemas financeiros reais utilizam estruturas orientadas a objetos para gerenciar diferentes tipos de pagamentos de forma elegante e extensível.

## Funcionalidades

### ✓ Implementadas

- **Pagamento por Boleto**: Geração de código de barras com desconto de 12% aplicado automaticamente
- **Pagamento por Crédito**: Suporte a parcelamento de 1 até 12 vezes com juros progressivos (5% até 6 parcelas, 8% acima)
- **Pagamento por Débito**: Processamento imediato com validação de saldo
- **Múltiplas Bandeiras**: MasterCard, Visa, Elo e American Express
- **Interface Interativa**: Menu console com feedback visual e colorização contextual
- **Validações**: Limite de crédito (R$ 2.000) e verificação de saldo para débito
- **Cálculos Financeiros**: Aplicação correta de descontos, juros e precisão monetária

## Tecnologias Utilizadas

| Tecnologia | Versão | Propósito |
|-----------|--------|----------|
| **C#** | 11 | Linguagem principal |
| **.NET** | 7.0 | Framework/Runtime |
| **Console API** | - | Interface com usuário |

## Arquitetura

O projeto utiliza uma arquitetura baseada em herança e polimorfismo:

```
Pagamento (classe base)
├── Boleto
└── Cartao (classe abstrata)
    ├── Credito
    └── Debito
```

### Estrutura de Classes

- **Pagamento**: Classe base que define o contrato básico com propriedade `valor` e data da transação
- **Cartao**: Classe abstrata que estende `Pagamento` e implementa a lógica comum de cartões (dados do titular, número, CVV, bandeira)
- **Boleto**: Implementação específica de pagamento por boleto, herda diretamente de `Pagamento`
- **Credito**: Pagamento com parcelamento e juros, herda de `Cartao`
- **Debito**: Pagamento imediato com validação de saldo, herda de `Cartao`

Esta estrutura permite que novos tipos de pagamento sejam adicionados facilmente através da herança, respeitando o princípio Open/Closed do SOLID.

## Banco de Dados

**Não há banco de dados implementado.** Os dados são mantidos exclusivamente em memória durante a execução do programa. Isso significa que:

- As transações não são persistidas
- Não existe histórico de pagamentos
- Os dados são perdidos ao encerrar a aplicação

Este é um sistema educacional focado em demonstrar conceitos de POO, não em produção.

## Como Executar

### Pré-requisitos

- **.NET SDK 7.0** ou superior instalado
  - Download: https://dotnet.microsoft.com/download
- Um terminal ou IDE compatível com C# (Visual Studio, VS Code, etc.)

### Passo a Passo

1. **Clone o repositório**
   ```bash
   git clone https://github.com/mlm5608/Console_Financeiro.git
   cd Console_Financeiro
   ```

2. **Restaure as dependências**
   ```bash
   dotnet restore
   ```

3. **Execute a aplicação**
   ```bash
   dotnet run
   ```

4. **Interaja com o menu**
   - Selecione o tipo de pagamento (1, 2 ou 3)
   - Insira as informações solicitadas
   - Acompanhe o processamento no console

5. **Saia da aplicação**
   - Digite `0` no menu principal para encerrar

### Execução em IDE

- **Visual Studio**: Abra `projeto-pagamento.csproj` e pressione `F5`
- **VS Code**: Instale a extensão C# e execute através do painel Debug

## Configuração

Não há arquivo de configuração necessário (`.env`, `appsettings.json`, etc.). A aplicação funciona com configurações padrão definidas no código:

- Limite de crédito: R$ 2.000
- Saldo inicial de débito: R$ 500.000.000 (simulado)
- Desconto em boleto: 12%
- Juros em crédito: 5% (1-6 parcelas) ou 8% (7-12 parcelas)

## Demonstração

### Exemplo de Uso - Pagamento por Crédito

```
PROJETO PAGAMENTO - Escolha sua forma de pagamento:     
                                            
  (1)- Boleto                               
  (2)- Crédito                              
  (3)- Débito                               
                                            
  (0)- Sair/Fechar                          

Seleciona a opção desejada: 2

Digite o CVV do cartão: 123
Digite o nome do titular do cartão: João Silva
Digite o número do cartão: 1234567890123456

Selecione a bandeira do cartão:
(1)- MasterCard
(2)- Elo
(3)- American Express
(4)- Visa
(0)- Sair/Fechar

Selecione a bandeira: 4
Bandeira selecionada: Visa

Qual o valor do seu pagamento?: 500.00

Quer dividir o valor em quantas parcelas?
Máximo de 12
até 6 - acrécimo de 5% de juros
de 7 até 12 - acrécimo de 8% de juros
0 - Sem parcelamento
6
O valor total ficará R$525
```

## Melhorias Futuras

As seguintes funcionalidades **não estão implementadas** e representam possibilidades de extensão:

- [ ] Persistência em banco de dados (SQL Server, SQLite ou PostgreSQL)
- [ ] Histórico de transações e extratos
- [ ] Validação de cartão com Luhn Algorithm
- [ ] Tratamento robusto de exceções (try-catch)
- [ ] Testes unitários (xUnit ou NUnit)
- [ ] Logging estruturado de operações
- [ ] Autenticação de usuário
- [ ] Relatórios de transações
- [ ] Integração com APIs reais de pagamento
- [ ] Interface gráfica (WPF/Windows Forms)

## Autor

**mlm5608** - Desenvolvedor  
Projeto criado como exercício de Programação Orientada a Objetos em C#.

---

**Nota**: Este é um projeto educacional. Não é destinado a processar transações reais ou em ambiente de produção.
