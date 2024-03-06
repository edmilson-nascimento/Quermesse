# Quermesse
 
![Static Badge](https://img.shields.io/badge/development-abap-blue)
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/edmilson-nascimento/quermesse)
![Static Badge](https://img.shields.io/badge/miriam_batista-abap-red)
![Static Badge](https://img.shields.io/badge/alexandra_espada-abap-pink)

> 🗘 Este documento, assim como o negócio, está em constante fase de melhorias


# Table of Contents
- [Introdução](#introdução) 
- [Glossário](#glossário)
- [O que é Quermesse?](#o-que-é-quermesse)
- [Transacção e filtro](#transacção-e-filtro)
- [Visão geral](#visão-geral)
  - [Visão de atendimento BC](#visão-de-atendimento-bc)
    - [Status de Incidentes](#status-de-incidentes)
    - [Boas praticas para seguir](#boas-praticas-para-seguir)
    - [Atividades iniciais](#atividades-iniciais)
  - [Fluxo de atendimento geral](#fluxo-de-atendimento-geral)

## Introdução
Este tem como objecto explicar de maneira directa como são os fluxos e processo no atendimento de *Incidentes* pelo time de `BC` da **EDP JUMP GA**.

## Glossário
É bem comum a utilização de siglas e aqui temos algumas para facilitar o entendimento dos processos/fluxos que são abordados para atendimentos de INC. A descrição abaixo é uma representação particular do cenário abordado e não contempla os termos de forma abrangida e/ou aplicada em outros cenários / times / escopos.

| Sigla |Significado |Descrição |
| :--- |:---------- |:------------ |
| AST | Asset | Abreviação para centralizador de âmbito evolutívo |
| BC|Business Consulting | ~~Find Clarity in Chaos~~ ABAP, Desenvolvedor SAP, Consultor ABAP, SAP DEV|
| DFCT |Corrective Change | - |
| FF | Firefighter | Perfil para acesso em Ambiente Produtivo com finalidades de análise e processamento |
| GA|Gestão de Ativos|-|
| INC|Incidentes| Abreviação para centralizador de âmbito corretivo |
| TCODE |Transação SAP | _Transaction code_ de forma abrevia |
| Service-Now |Sistema de serviços EDP | Sistema interno da EDP usado para gestão de ticket/chamados |


## O que é Quermesse?
Quermesse é um sistema criado e mantido pelo time de `BC` da **EDP JUMP GA** que tem como finalidade gerir os *Incidentes* que foram criados no sistema Service-Now e que exigem a actuação do time de `BC` para análises, melhorias e outros.

## Transacção e filtro
Para acessar a solução deves user a tcode `ZCA_QUERMESSE_BC`. É possível fazer filtro por Status, `BC`que esta atender, Tickets abertos e outros. Por padrão, o filtro inicial esta para que sejam listados os itens que não tem `BC` atribuido e que estão em aberto. Dessa forma tem de forma directo uma lista do que esta disponível para atendimento no momento.

## Visão geral
Itens que foram criados no Service-Now para atendimento do time de Jump GA, podem ou não ser adicionados no sistema Quermesse. Isso depende se esse tema necessita de apoio técnico, seja para analise ou pontos de correção. Após analise do recurso funcional (que é responsável por inserir o item na Quermesse), isso é definido.

```mermaid
%%{ init: { 'flowchart': { 'curve': 'basis' } } }%%
flowchart TB

    Begin((" ")):::startClass --> service-now([Service-Now])
    service-now --> Atendimento-BC(["Necessario atendimento BC?"])
    Atendimento-BC --> Q1{" "}

    Q1 -- Sim --> Quermesse("Adic. na Quermesse") 
            --> End
    Q1 -- Não -->

End(((" "))):::endClass
```


## Fluxo de atendimento por Status
Isso corresponde a uma representação direta de Status de Incidentes mantidos na Quermesse.
```mermaid
flowchart TD
    start((" ")) --> Q1
    Q1(1. Criado) --> Q2(2. Atribuido)
    Q2 --> Desenvolvimento-BC
    Desenvolvimento-BC(6. Em desenvolvimento - BC) --> Q4(7. Em Teste - Funcional)

%%  saida de cancelamento
    Q4 --> Q3(3. Cancelado)
    Q3 --> End(((" ")))


    Q4 --> QQ{{Testes ok?}}
    QQ -- Sim --> Q5(8. Aguardando Aprovação)
    QQ -- Não --> Desenvolvimento-BC
%%  Desenvolvimento-BC --> Q6(Case SAP criado)
%%  Q6 --> Q4
    Q5 --> Q9(4. Fechado)
    Q9 --> End(((" ")))
```
&#129518;
.
### Visão de atendimento BC
A descrição contempla o fluxo dos passos que um `BC` deve atender para seguir a resolução de um INC na Quermesse. 

#### Status de Incidentes
Para facilitar o entendimento de cada Status na Quermesse, segue abaixo a lista com descrivos correspondentes.

| Status | Descrição | Observações | 
| :---------- | :---------- | :---------- | 
| Criado | Item foi criado na Quermesse | Esse passo será mantido ate dados de testes serem anexos/compartilhados | 
| Atribuido | Quando o item esta direcionado para atendimento | ∆ Atendimento ainda não iniciado |
| * Em desenvolvimento (BC) | O item esta em atendimento pelo lado do `BC` |  - | 
| * Em Teste (Funcional) | A solução proposta em testes funcionais |  - | 
| * Aguardando Aprovação | Aguardando aprovação do DFCT | Acontece após o sucesso dos testes funcionais | 
| ~~Case SAP criado~~ | ~~Solução sendo atendimento por _Case SAP_~~ |  
| Reaberto | Aberto novamente por necessidade de melhoria/ajuste | - | 
| Cancelado | Não há mais necessidade de ajuste ABAP | - | 
| Fechado | Concluído analise/ajuste | Ultima fase do INC | 

*_Itens que devem ser criados. Ainda não existentes no cenario atual_;  

Níveis de status (configuração tcode `OIBS` *ZCA_STAT*).
| Nº do status | Status | Texto Breve | Nº mais baixo | Nº mais elevado |
|:--:|:---:|:---|:--- |:---|
| 1 | CRD | Criado | 1 - Criado | 4 - Fechado
| 2 | ATR | Atribuido | 2 - Atribuido | 4 - Fechado
| 3 | CLD | Cancelado | 3 - Cancelado | 4 - Fechado
| 4 | FCD | Fechado | 4 - Fechado | 5 - Reaberto
| 5 | RBT | Reaberto | 2 - Atribuido | 4 - Fechado
| 6 | DEV | Em desenvolvimento (BC) | 2 - Atribuido | 7 - Em Teste (Funcional)
| 7 | TST | Em Teste (Funcional) | 6 - Em desenvolvimento (BC) | 8 - Aguardando Aprovação
| 8 | APR | Aguardando Aprovação | 7 - Em Teste (Funcional) | 4 - Fechado

### Boas praticas para seguir
Dentre as descrições do processo em si, algumas regras devem ser seguidas para que o fluxo ocorra como esperado durante os atendimentos, segue abaixo:
- INC terá que estar inserido correctamente na Quermesse para se iniciar desenvolvimento / análise
- INC deve ser inserido na Quermesse pelo recurso funcional e actualizado pelo recurso `BC`
- O Status deve ser alterado de acordo com a evolução do INC
- O campo Resolução da Corretiva deve ser actualizado a medida que a solução se desenvolve (analise/testes/etc)
- Após ter o ajuste transportado para _Ambiente de Produção_, o item deve ser fechado na Quermesse.


### Atividades iniciais
Afim de evitar retrabalho e tambem visando que o INC seja escalável, é necessário termos os dados de forma que o `BC` **consiga iniciar o atendimento de acordo com os dados que foram inseridos**. Ou no caso, pelo menos estar mais inteirado do que trata o fluxo para poder atender o INC.

```mermaid
flowchart TB
start((" "))    --> verifFuncional([Verif. funcional responsável])
verifFuncional  --> verifCenarios([Verificar cenários de testes])

    verifCenarios   --> existTestK15(Existem testes em k15?)
    existTestK15    --  Não --> solicitarK15(Solicicitar cenários)

    solicitarK15    --> End
    existTestK15--  Sim --> avaliarK15(Análise em K15)

avaliarK15      --> End(((" ")))
```
> O atendimento do INC é inciado **somente após os dados de testes anexados** para chegarmos a soluções mais assertivas.

Pode-se gerar um arquivo de testes respondendo por exemplo as perguntas abaixo:

0. Qual Ambiente?
1. Quais os passos de execução?
2. Qual o resultado encontrado hoje?
3. Qual o resultado esperado e como verificar?

Respondendo as perguntas acima, usando prints caso seja possivel, consegue gerar um arquivo de testes para que o `BC` avalie o cenario.

