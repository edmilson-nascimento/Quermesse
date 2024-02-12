# Quermesse
 
 
![Static Badge](https://img.shields.io/badge/development-abap-blue)
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/edmilson-nascimento/quermesse)
![Static Badge](https://img.shields.io/badge/miriam_batista-abap-red)



Este tem como objeto explicar de maneira direta como são os fluxos e processo no atendimento de *incidentes* pelo time de `BC` da **EDP JUMP GA**.

## Glossário
É bem comum a utilização de sigla e aqui temos algumas para facilitar o entendimento dos processos/fluxos que são abordados para atendimentos de INC. A descrição abaixo é uma representação particular do cenário abordado e não contempla os termos de forma abrigida e/ou aplicada em outros cenarios/times/escopos.


| Sigla |Significado |Descrição |
|:--- |:---------- |:------------ |
|AST | - | Abreviação para centralizador de âmbito evoluitivo |
|BC|Business Consulting | ~~Find Clarity in Chaos~~ ABAP, Desenvolvedor SAP, Consultor ABAP, SAP DEV|
|GA|Gestão de Ativos|-|
|INC|Incidentes| Abreviação para centralizador de âmbito corretivo |
|TCODE |Transação SAP | _Transaction code_ de forma abrevia |
|Service-Now |Sistema de serviços EDP | Sistema interno da EDP usado para gestão de ticket/chamados |
|.|.|.|


## O que é Quermesse?
Quermesse é um sistema criado e mantido pelo time de `BC` da **EDP JUMP GA** que tem como finalidade gerir os *Incidentes* que foram criados no sistema Service-Now e que exigem a atuação do time de `BC` para análises, melhorias e outros.

## Transação e filtro
Para acessar a solução deves user a tcode `ZCA_QUERMESSE_BC`. É possivel fazer filtro por Status, `BC`que esta atender, Tickets abertos e outros. Por padrão, o filtro inicial esta para que sejam listados os itens que não tem `BC` atribuido e que estão em aberto. Dessa forma tem de forma direto uma lista do que esta disponivel para atendimento no momento.

## Visão geral

```mermaid

%%{ init: { 'flowchart': { 'curve': 'basis' } } }%%
flowchart TB

Begin((" ")):::startClass --> service-now([Service-Now])
B --> C([Create jobs by variant]) 

C --> J1(FLB1N Partidas em Aberto - F)
C --> J2(FLB1N Atividade FI MM - F)
C --> J3(FLB3N Partidas em Aberto - CR)
C --> J4(FLB1N Partidas Lancadas - F)

J1 --> submitFBL1N("Call FBL1N - Report RFITEMAP")
J2 --> submitFBL1N
J3 --> submitFBL3N("Call FBL3N - Report RFITEMGL")
J4 --> submitFBL3N

submitFBL1N --> alvGetData(["Busca dados gerados pelo ALV"])
submitFBL3N --> alvGetData

alvGetData --> excelRoutine(["Processa arquivo excel com dados recuperados"])

excelRoutine --> saveFile(["Salva arquivo no servidor"])

saveFile --> End(((" "))):::endClass
```

### Visão de atendimento BC
A descrição contempla o fluxo dos passos que um `BC` deve atender para seguir a resolução de um INC na Quermesse. 

#### Boas praticas para seguir
Dentre as descrições do processo em si, algumas regras devem ser seguidas para que o fluxo ocorra como esperado durantes os atendimentos, segue abaixo:
- INC terá que estar inserido corretamente na Quermesse para se iniciar desenvolvimento/analise
- O Status deve ser alterado de acordo com a evolução do INC