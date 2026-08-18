# Console Financeiro

Um sistema de processamento de pagamentos desenvolvido em C# que demonstra conceitos fundamentais de Programação Orientada a Objetos. Primeiro projeto em grupo realizado durante o curso técnico em Desenvolvimento de Software no SENAI.

## Sobre o Projeto

Console Financeiro foi desenvolvido como exercício prático de POO em C#, implementando um sistema que processa três tipos de pagamento distintos com lógica de negócio realista. Cada tipo de pagamento possui regras, validações e cálculos específicos, demonstrando como sistemas financeiros reais estruturam o processamento de transações de forma elegante e extensível.

O projeto reflete a importância de design orientado a objetos desde o início: o código foi estruturado para permitir que novos tipos de pagamento sejam adicionados facilmente sem modificação da lógica existente, seguindo o princípio Open/Closed do SOLID.

## Funcionalidades

### ✓ Pagamento por Boleto
- Geração de código de barras com 3 sequências aleatórias
- Desconto automático de 12% aplicado ao valor
- Exibição da data da transação
- Confirmação de valor final a pagar

### ✓ Pagamento por Crédito
- Suporte a parcelamento de 1 até 12 vezes
- Juros progressivos: 5% para 1-6 parcelas, 8% para 7-12 parcelas
- Limite de crédito: R$ 2.000
- Cálculo automático do valor total com juros
- Validação antes de processar

### ✓ Pagamento por Débito
- Processamento imediato da transação
- Validação de saldo antes de autorizar
- Saldo inicial simulado de R$ 500.000.000
- Exibição do saldo atualizado após transação
- Mensagem de erro para saldo insuficiente

### ✓ Suporte a Bandeiras de Cartão
- Visa
- MasterCard
- Elo
- American Express

### ✓ Interface Interativa
- Menu principal com loop até encerramento
- Menu para seleção de bandeira
- Colorização contextual do console (vermelho para avisos, verde para sucesso)
- Coleta estruturada de dados do cartão (CVV, titular, número, bandeira)
- Feedback visual em cada etapa

## Tecnologias Utilizadas

| Tecnologia | Versão | Propósito |
|-----------|--------|----------|
| **C#** | 11 | Linguagem de programação |
| **.NET** | 7.0 | Framework e runtime |
| **Console API** | .NET padrão | Interface com usuário |

## Arquitetura

O projeto demonstra uma arquitetura clara baseada em **herança polimórfica**, fundamental para sistemas extensíveis:

```
Pagamento (classe base abstrata)
├── Boleto (herança direta)
└── Cartao (classe abstrata intermediária)
    ├── Credito (herança de Cartao)
    └── Debito (herança de Cartao)
```

### Responsabilidades de Cada Classe

**Pagamento** (Classe Base)
- Define contrato comum: propriedade `valor` e `data`
- Implementa método `Cancelar()` genérico para qualquer tipo
- Serve como base para todas as formas de pagamento

**Cartao** (Classe Abstrata)
- Estende `Pagamento` para tipos de cartão
- Define propriedades comuns: `Bandeira`, `NumeroCartao`, `Titular`, `CVV`
- Implementa método `SalvarCartao()` — coleta dados do usuário com validação de bandeira
- Define método abstrato `Pagar()` que cada tipo implementa diferentemente
- Evita duplicação de código entre Crédito e Débito

**Boleto**
- Herda diretamente de `Pagamento`
- Implementa `CodigoDeBarras()` para gerar número aleatório de barra
- Implementa `Registrar()` com cálculo de desconto

**Credito**
- Herda de `Cartao`
- Implementa `Pagar()` com validação de limite
- Coleta número de parcelas com regras de juros
- Calcula e exibe valor final com juros aplicados

**Debito**
- Herda de `Cartao`
- Implementa `Pagar()` com validação de saldo
- Deduz valor do saldo e exibe saldo atualizado
- Oferece feedback claro de sucesso ou erro

### Por Que Essa Arquitetura?

1. **Reutilização**: `Cartao` evita duplicar código entre Crédito e Débito
2. **Extensibilidade**: Adicionar novo tipo é simples (ex: PIX, Criptomoeda)
3. **Polimorfismo**: `Pagar()` se comporta diferente em cada classe
4. **Manutenibilidade**: Mudanças em `Cartao` beneficiam Crédito e Débito simultaneamente

## Banco de Dados

**Não há banco de dados implementado.** Este é um projeto educacional onde:
- Dados são mantidos exclusivamente em memória
- Transações não são persistidas
- Sem histórico de pagamentos
- Sem tabelas ou esquema SQL

Isso foi apropriado para o contexto de aprendizado, focando em lógica de negócio e POO.

## Como Executar

### Pré-requisitos

- **.NET SDK 7.0 ou superior** instalado
  - Download: https://dotnet.microsoft.com/download
- Terminal ou IDE (Visual Studio, VS Code, Rider)
- Windows, macOS ou Linux

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
   - Selecione o tipo de pagamento: 1 (Boleto), 2 (Crédito) ou 3 (Débito)
   - Preencha os dados solicitados
   - Acompanhe o processamento no console
   - Digite `0` para encerrar

### Exemplos de Uso

**Exemplo 1: Pagamento por Boleto**
```
Selecione: 1
Qual o valor do seu pagamento?: 100.00
[Código de barras gerado]
No dia de [data]
O total a ser pago é de: R$ 88.00
```

**Exemplo 2: Pagamento por Crédito**
```
Selecione: 2
Digite o CVV do cartão: 123
Digite o nome do titular: João Silva
Digite o número do cartão: 1234567890123456
Selecione a bandeira: 4 (Visa)
Qual o valor do seu pagamento?: 500.00
Quer parcelar em quantas vezes?: 6
O valor total ficará R$525 (500 + 5% de juros)
```

**Exemplo 3: Pagamento por Débito**
```
Selecione: 3
Digite o CVV do cartão: 456
Digite o nome do titular: Maria Santos
Digite o número do cartão: 9876543210987654
Selecione a bandeira: 1 (MasterCard)
Qual o valor do seu pagamento?: 200.00
Pagamento de R$200 realizado com sucesso. Novo saldo: R$499999800
```

## Configuração

Nenhuma configuração externa é necessária. Todos os valores padrão estão definidos no código:

- **Limite de Crédito**: R$ 2.000 (em `Credito.cs`)
- **Saldo Inicial**: R$ 500.000.000 (em `Debito.cs`)
- **Desconto Boleto**: 12% (em `Boleto.cs`)
- **Juros Crédito**: 5% (até 6 parcelas) ou 8% (7-12 parcelas) (em `Credito.cs`)

Para modificar qualquer valor, edite o arquivo `.cs` correspondente e execute `dotnet run` novamente.

## Conceitos de Programação Demonstrados

- **Herança**: Todas as classes herdam comportamento de `Pagamento` ou `Cartao`
- **Polimorfismo**: Método `Pagar()` sobrescrito em cada tipo de pagamento
- **Classes Abstratas**: `Cartao` define contrato sem implementação completa
- **Encapsulamento**: Propriedades com getters/setters, dados privados
- **Namespaces**: Organização em `projeto_pagamento`
- **Tipos Primitivos**: float, int, string para armazenar dados
- **Estruturas de Controle**: loops `do-while`, `switch-case`, `if-else`
- **String Interpolation**: Uso de `@$""` para formatação
- **Métodos**: Públicos e privados com responsabilidades claras
- **Validação de Negócio**: Regras específicas por tipo de pagamento

## Fluxos Principais da Aplicação

### Fluxo Geral
1. Menu principal exibido em loop
2. Usuário seleciona tipo de pagamento (1-3) ou sai (0)
3. Dependendo da escolha, fluxo específico é executado
4. Resultado exibido com colorização contextual
5. Retorna ao menu principal

### Fluxo de Boleto
1. Pergunta valor do pagamento
2. Gera 3 números aleatórios para código de barras
3. Exibe código de barras formatado
4. Calcula e exibe valor com desconto de 12%

### Fluxo de Crédito
1. Coleta dados do cartão (CVV, titular, número, bandeira)
2. Menu para seleção de bandeira com validação
3. Pergunta valor do pagamento
4. Valida se não ultrapassa limite (R$ 2.000)
5. Se OK, pergunta número de parcelas
6. Aplica juros conforme número de parcelas (5% ou 8%)
7. Exibe valor final com juros

### Fluxo de Débito
1. Coleta dados do cartão (CVV, titular, número, bandeira)
2. Menu para seleção de bandeira com validação
3. Pergunta valor do pagamento
4. Valida se saldo é suficiente
5. Se OK, deduz valor do saldo
6. Exibe novo saldo atualizado

## Principais Desafios Técnicos

1. **Estruturação de Hierarquia**: Decidir o que vai em `Pagamento`, `Cartao` e subclasses
2. **Validações Específicas**: Cada tipo tem regras diferentes (limite, saldo, juros)
3. **Menu Aninhado**: Bandeira é um submenu dentro do fluxo de cartão
4. **Precisão Monetária**: Usar `float` e `Math.Round()` para valores financeiros
5. **Fluxo de Entrada**: Garantir que dados são coletados na ordem correta

## Melhorias Futuras

As seguintes funcionalidades **não estão implementadas** e representam oportunidades de extensão:

- [ ] **Banco de Dados**: SQLite ou SQL Server para persistência
- [ ] **Histórico de Transações**: Armazenar e consultar pagamentos realizados
- [ ] **Validação de Cartão**: Luhn Algorithm para validar número de cartão
- [ ] **Tratamento de Exceções**: try-catch para inputs inválidos
- [ ] **Testes Unitários**: xUnit ou NUnit para validar lógica
- [ ] **Logging Estruturado**: Registrar operações críticas
- [ ] **Autenticação**: Validar usuário antes de processar
- [ ] **Relatórios**: Gerar extratos e análises
- [ ] **Integração com APIs**: Comunicar com sistemas de pagamento reais
- [ ] **Interface Gráfica**: WPF ou Windows Forms para melhor UX
- [ ] **Validação de Entrada Robusta**: Garantir dados válidos em todos os campos
- [ ] **Transações Atômicas**: Garantir consistência em operações múltiplas

## Autor

**mlm5608** - Desenvolvedor  
Projeto desenvolvido como primeiro projeto em grupo durante o curso técnico em Desenvolvimento de Software no SENAI.

---

**Nota**: Este é um projeto educacional criado como exercício de Programação Orientada a Objetos em C#. Não é destinado a processar transações reais ou em ambiente de produção.

**Links Úteis:**
- [Repositório GitHub](https://github.com/mlm5608/Console_Financeiro)
- [Documentação .NET](https://learn.microsoft.com/pt-br/dotnet/)
- [C# Documentation](https://learn.microsoft.com/pt-br/dotnet/csharp/)
