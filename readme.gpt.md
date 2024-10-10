## Introdução
Este documento tem como objetivo explicar de maneira direta como são os fluxos e processos no atendimento de *Incidentes* pelo time de `BC` da **EDP JUMP GA**.

<TODO> Incluir uma breve explicação sobre a **EDP JUMP GA**, para contextualizar o leitor sobre o que é e qual sua função.

## Glossário
É bem comum a utilização de siglas e aqui temos algumas para facilitar o entendimento dos processos/fluxos que são abordados para atendimentos de INC. A descrição abaixo é uma representação particular do cenário abordado e não contempla os termos de forma abrangente e/ou aplicada em outros cenários / times / escopos.

| Sigla | Significado | Descrição |
| :--- | :---------- | :------------ |
| AST | Asset | Abreviação para centralizador de âmbito evolutivo |
| BC|Business Consulting | ~~Find Clarity in Chaos~~ ABAP, Desenvolvedor SAP, Consultor ABAP, SAP DEV|
| DFCT | Corrective Change | Refere-se a mudanças corretivas aplicadas a um incidente já em andamento |
| FF | Firefighter | Perfil para acesso em Ambiente Produtivo com finalidades de análise e processamento |
| GA|Gestão de Ativos| Área responsável pela gestão de ativos na EDP |
| INC|Incidentes| Abreviação para centralizador de âmbito corretivo |
| TCODE |Transação SAP | _Transaction code_ de forma abreviada |
| Service-Now |Sistema de serviços EDP | Sistema interno da EDP usado para gestão de ticket/chamados |

## O que é Quermesse?
Quermesse é um sistema criado e mantido pelo time de `BC` da **EDP JUMP GA** que tem como finalidade gerir os *Incidentes* que foram criados no sistema Service-Now e que exigem a atuação do time de `BC` para análises, melhorias e outros.

<TODO> Incluir exemplo visual do sistema Quermesse ou expandir detalhes sobre como ele se integra ao Service-Now.

## Transação e filtro
Para acessar a solução, deve-se usar a tcode `ZCA_QUERMESSE_BC`. Uma transação (ou TCODE) é um código utilizado no sistema SAP para executar uma função ou acessar uma aplicação específica. No Quermesse, essa transação permite filtrar por Status, `BC` responsável, tickets abertos e outros. Por padrão, o filtro inicial lista itens sem `BC` atribuído e que estão em aberto, facilitando a identificação de demandas disponíveis.

## Visão geral
Itens criados no Service-Now para atendimento do time de Jump GA podem ou não ser adicionados no sistema Quermesse, dependendo da necessidade de apoio técnico. Após análise do recurso funcional (responsável por inserir o item na Quermesse), é definida a inclusão ou não.

```mermaid
%%{ init: { 'flowchart': { 'curve': 'basis' } } }%%
flowchart TB
    Begin((" ")):::startClass --> service-now([Service-Now])
    service-now --> Atendimento-BC(["Necessário atendimento BC?"])
    Atendimento-BC --> Q1{" "}
    Q1 -- Sim --> Quermesse("Adic. na Quermesse") --> End
    Q1 -- Não -->
End(((" "))):::endClass
