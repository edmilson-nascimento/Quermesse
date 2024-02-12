# Quermesse
 
 
![Static Badge](https://img.shields.io/badge/development-abap-blue)
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/edmilson-nascimento/quermesse)
![Static Badge](https://img.shields.io/badge/miriam_batista-abap-red)



Este tem como objeto explicar de maneira direta como são os fluxos e processo no atendimento de *incidentes* pelo time de `BC` da **EDP JUMP GA**.

## Glossário
É bem comum a utilização de sigla e aqui temos algumas para facilitar o entendimento dos processos/fluxos que são abordados para atendimentos de INC. A descrição abaixo é uma representação particular do cenário abordado e não contempla os termos de forma abrigida e/ou aplicada em outros cenarios/times/escopos.


| Sigla |Significado |Descrição |
|:--- |:---------- |:------------ |
|BC|Business Consulting | ~~Find Clarity in Chaos~~ ABAP, Desenvolvedor SAP, Consultor ABAP, SAP DEV|
|GA|Gestão de Ativos|-|
|tcode |Transação SAP | _Transaction code_ de forma abrevia |
|.|.|.|


## O que é Quermesse?
Quermesse é um sistema criado e mantido pelo time de `BC` da **EDP JUMP GA** que tem como finalidade gerir os *Incidentes* que foram criados no sistema Service-Now e que exigem a atuação do time de `BC` para análises, melhorias e outros.

## Transação e filtro
Para acessar a solução deves user a tcode `ZCA_QUERMESSE_BC`. É possivel fazer filtro por Status, `BC`que esta atender, Tickets abertos e outros. Por padrão, o filtro inicial esta para que sejam listados os itens que não tem `BC` atribuido e que estão em aberto. Dessa forma tem de forma direto uma lista do que esta disponivel para atendimento no momento.

## Visão geral

```mermaid

```

### Visão de atendimento BC