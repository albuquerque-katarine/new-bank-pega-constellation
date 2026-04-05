# New Bank
## Pega Constellation

## Vídeo de demonstração

Acesse o Vídeo: ![New Bank App - Pega Constellation](https://lnkd.in/dMpNjka2)

## Objetivo

A aplicação New Bank tem como objetivo simular um fluxo bancário básico, organizado de forma simples e modular dentro de um Case Type. Ela permite gerenciar o ciclo completo de um cliente desde a entrada até a movimentação da conta.

## Finalidade

- Abertura de conta ou acesso existente
- Movimentação financeira
- Finalização e continuidade

## Case Type - Conta Bancária

![Case Type](image.png)

## Status

- Novo (Abertura)
- Em-Processamento (Movimentação)
- Concluído | Resolved-Completed (Finalização)

## Flow - Abertura

![alt text](image-10.png)

## Flow - Movimentação

![alt text](image-12.png)

## Flow - Finalização

![alt text](image-11.png)

## Data Type

- Cliente
    - ClienteID (Text-line)
    - NomeCompleto (Text-line)
    - Telefone (Phone)
    - Email (Email)
    - Senha (Text-line)

- Transacao
    - TransacaoID (Text-line)
    - Data (Date-only)
    - Tipo (picklist: Depósito | Saque)
    - Valor (Decimal)

- Conta
    - NumeroConta (Text-line)
    - Data (Date-Time)
    - EmailCliente (Text-line)
    - Saldo (Decimal)
    - Cliente (Data Referenca Single Records)
    - Transacoes (Embedded Data List Records)

## Data Pages Savable

- D_ClienteSavable
- D_TransacaoSavable
- D_ContaSavable

As Data Pages Salváveis possuem duas fontes de dados, Loockup e Data Transform; se o Param.pyGUID for diferente de Vazio, acessa o Loockup; senão o Data Transform. O parâmetro pyGUID foi configurado para não ser obrigatório.

## Data Pages Criadas

### Data Objects: Cliente

- D_ClientePorEmailSenha
    - Tipo: List
    - Parâmetro(s): Email e Senha
    - Fonte de dados: Report Definition

Data Page usada para validar o acesso à conta, solicitando email e senha.

### Data Objects: Conta

- D_ContaPorEmailCliente
    - Tipo: List
    - Parâmetro(s): Email
    - Fonte de dados: Report Definition

Data Page usada para verificar se a conta existe, fazendo a busca com o email do cliente.

## Stage: Abertura

1. Escolhe a Operação:
    - Criar Conta - Vai para opção 2. Criar Conta
    - Acessar Conta - Vai para opção 3. Acessar Conta

    ![alt text](image-1.png)

2. Criar Conta:
    - Nome Completo (Text)
    - Telefone (Phone)
    - Email (Email)
    - Senha (Text)

    ![alt text](image-2.png)

3. Save Data Page (Cliente)     

4. Acessar Conta
    - Email (Email)
    - Senha (Text)
    - Criar Conta (Boolean) Volta para opção 2. Criar Conta

    ![alt text](image-3.png)

## Stage: Movimentação

1. Realizar Transação:
    - Exibe o email do cliente
    - Exibe o Saldo Atual
    - Tipo (Picklist: Depósito | Saque)
    - Valor (Decimal)

    ![alt text](image-4.png)

2. Save Data Page (Transação)
3. Save Data Page (Conta)


## Stage: Finalização

1. Exibir Conta
    - Exibe o Email do cliente
    - Exibe o Número da Conta do cliente
    - Exibe o Saldo Atual
    - Exibe o Tipo da operação
    - Exibe o Valor da transação
    - Deseja Realizar Nova Operação?

    ![alt text](image-5.png)

## Pré-Processamento

- Realizar Transações (Data Transform: DT_PreRealizarTransacao)
    - Parâmetro: Email

    ![alt text](image-8.png)

## Pós-Processamento

- Acessar Conta (Data Transform: DT_ValidarCliente)

    ![alt text](image-9.png)

- Realizar Transações (Data Transform: DT_CalcularSaldo)
    - Parâmetro: Email

    ![alt text](image-6.png)

- Exibir Conta (Data Transform: DT_PreExibirConta)

    ![alt text](image-7.png)

## Contatos

- E-mail: [kba.2879@gmail.com](mailTo:kba.2879@gmail.com)

- Linkedin: [/katarine-albuquerque](https://www.linkedin.com/in/katarine-albuquerque/)