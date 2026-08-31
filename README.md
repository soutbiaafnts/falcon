<img alt="millennium falcon" src="./assets/banner.png" >

<h1 align="center">FALCON</h1>

<div align="center">

![Versão](https://custom-icon-badges.demolab.com/badge/versão-1.0.0-success)
![Status](https://custom-icon-badges.demolab.com/badge/status-ativo-success)
![Environment](https://custom-icon-badges.demolab.com/badge/ambiente-desenvolvimento-blue)

</div>

## Índice

- [Introdução](#1-introdução)
- [Problema de Pesquisa](#2-problema-de-pesquisa)
- [Hipóteses](#3-hipóteses)
- [Objetivo Geral](#4-objetivo-geral)
- [Objetivos Específicos](#5-objetivos-específicos)
- [Requisitos do Projeto](#6-requisitos-do-projeto)
- [Visão Geral do Funcionamento](#7-visão-geral-do-funcionamento)
- [Arquitetura Mecânica](#8-arquitetura-mecânica)
- [Quantidade de Compartimentos](#9-quantidade-de-compartimentos)
- [Arquitetura Eletrônica](#10-arquitetura-eletrônica)
- [Tecnologias](#11-tecnologias)
- [Arquitetura do Software](#12-arquitetura-de-software)
- [Arquitetura Baseada em Eventos](#13-arquitetura-baseada-em-eventos)
- [Máquina de Estados](#14-máquina-de-estados)
- [Engenharia de Software](#15-engenharia-de-software)
- [Organização da Equipe](#16-organização-da-equipe)
- [Indicadores de Validação](#17-indicadores-de-validação)
- [Cronograma](#18-cronograma)
- [Critérios de Aceite](#19-critérios-de-aceite)
- [Preparação para o TCC](#20-preparação-para-o-tcc)
- [Conclusão](#21-conclusão)

---

# 1. Introdução

O Falcon é um sistema embarcado para dispensação automática de medicamentos desenvolvido com foco na autonomia de idosos e na redução da necessidade de acompanhamento constante por cuidadores.

O projeto integra conceitos de Sistemas Embarcados, Internet das Coisas (IoT), Automação, Engenharia de Software, Robótica e Modelagem 3D para desenvolver um dispositivo de baixo custo, modular e preparado para futuras expansões.

A Iniciação Científica terá como foco o desenvolvimento de um protótipo funcional capaz de armazenar medicamentos, realizar a dispensação automática em horários programados, registrar eventos e fornecer uma interface simples para pacientes e cuidadores.

O Trabalho de Conclusão de Curso será uma evolução natural deste projeto, incorporando comunicação via Internet, banco de dados, dashboard web, acompanhamento remoto e geração de relatórios.

---

# 2. Problema de Pesquisa

**Como a utilização de um dispensador automático de medicamentos influencia a autonomia de idosos e a necessidade de intervenção dos cuidadores na administração medicamentosa?**

---

# 3. Hipóteses

## Hipótese Técnica (validada na IC)

O Falcon será capaz de:

- armazenar medicamentos;
- dispensá-los automaticamente nos horários programados;
- registrar a retirada ou ausência de retirada dos medicamentos;
- fornecer informações suficientes para apoiar o acompanhamento da administração medicamentosa.

## Hipótese de Impacto (a ser explorada futuramente)

A utilização do Falcon tende a aumentar a autonomia dos idosos e reduzir a necessidade de acompanhamento constante por parte dos cuidadores.

---

# 4. Objetivo Geral

Projetar, desenvolver e validar um protótipo funcional de um sistema embarcado para dispensação automática de medicamentos, visando avaliar seu potencial para aumentar a autonomia dos idosos e reduzir a necessidade de intervenção constante dos cuidadores.

---

# 5. Objetivos Específicos

- Projetar a estrutura mecânica utilizando modelagem e impressão 3D.
- Desenvolver a arquitetura eletrônica baseada em ESP32.
- Implementar o mecanismo automático de dispensação.
- Desenvolver um sistema de configuração de horários.
- Implementar sensores para monitoramento do funcionamento.
- Detectar automaticamente a retirada do copo contendo o medicamento.
- Registrar localmente todos os eventos de dispensação.
- Desenvolver uma interface simples para pacientes e cuidadores.
- Construir uma arquitetura de software modular preparada para futura integração com sistemas IoT.

---

# 6. Requisitos do Projeto

## Requisitos Funcionais

O Falcon deverá:

- armazenar medicamentos em compartimentos independentes;
- permitir configuração de horários;
- emitir alerta sonoro no horário programado;
- liberar apenas o medicamento correspondente ao horário atual;
- impedir acesso ao estoque pelo paciente;
- detectar retirada do copo;
- registrar retirada ou ausência de retirada;
- exibir informações em display;
- manter configurações mesmo após desligamento.

## Requisitos Não Funcionais

O sistema deverá:

- possuir baixo custo;
- ser compacto;
- utilizar componentes facilmente encontrados;
- permitir manutenção simples;
- possuir arquitetura modular;
- facilitar futuras expansões;
- utilizar componentes preparados para IoT;
- possuir alimentação por bateria e fonte externa.

---

# 7. Visão Geral do Funcionamento

## Abastecimento

O cuidador:

1. desbloqueia o compartimento utilizando uma chave física;
2. abastece os compartimentos;
3. configura os horários;
4. fecha novamente o sistema.

---

## Operação

Durante o funcionamento:

1. O Falcon monitora continuamente o horário através do RTC.
2. Quando chega o horário programado:

   - o buzzer é acionado;
   - o display informa que há um medicamento disponível.
3. O paciente pressiona o botão de confirmação.
4. O mecanismo gira até o compartimento correspondente.
5. O medicamento é conduzido por um funil até um copo apoiado sobre uma célula de carga.
6. Quando o paciente retira o copo:

   - o Falcon registra o evento;
   - encerra o alarme.
7. Caso o copo não seja retirado:

   - o alarme é repetido periodicamente.
8. Após 30 minutos sem retirada:

   - registra "medicamento não retirado";
   - considera o horário encerrado e segue para o próximo evento programado.

---

# 8. Arquitetura Mecânica

O Falcon será composto por:

- estrutura cilíndrica fixa;
- haste central;
- conjunto de palhetas acopladas à haste;
- compartimentos independentes;
- porta inferior de dispensação;
- funil direcionador;
- suporte para copo;
- compartimento eletrônico.

A haste central será movimentada por um motor de passo.

Cada posição angular corresponderá a um compartimento.

---

# 9. Quantidade de Compartimentos

Inicialmente será adotado:

**12 compartimentos.**

Justificativas:

- reduz complexidade mecânica;
- reduz tempo de impressão;
- reduz torque necessário;
- facilita validação;
- mantém o protótipo compacto.

No TCC poderá ser ampliado para 28 compartimentos (estoque semanal), sem necessidade de grandes alterações no software.

---

# 10. Arquitetura Eletrônica

## Unidade de Processamento

ESP32 DevKit V1

---

## Controle de Tempo

RTC DS3231

---

## Interface

Display OLED 128x64 I²C

Botões:

- cima
- baixo
- confirmar
- voltar

---

## Atuadores

- buzzer ativo;
- motor de passo (NEMA 17 ou equivalente).

---

## Sensores

- célula de carga + HX711;
- sensor Hall ou chave fim de curso para posição HOME.

---

## Alimentação

- fonte externa;
- bateria recarregável;
- conversor DC-DC.

---

# 11. Tecnologias

## Linguagem

C++

Framework Arduino para ESP32.

Motivos:

- ampla documentação;
- grande quantidade de bibliotecas;
- maior desempenho;
- facilidade de manutenção;
- alta escalabilidade.

---

# 12. Arquitetura de Software

O software será dividido em módulos independentes.

- Display
- RTC
- Motor
- Buzzer
- Botões
- Célula de carga
- Configurações
- Persistência
- Registro de eventos
- Agendador
- Máquina de Estados

Cada módulo possuirá apenas uma responsabilidade.

---

# 13. Arquitetura Baseada em Eventos

O software será orientado por eventos.

Exemplos:

## Evento: Horário Alcançado

- ligar buzzer;
- atualizar display;
- aguardar confirmação.

## Evento: Confirmação

- posicionar compartimento;
- liberar medicamento.

## Evento: Copo Retirado

- registrar evento;
- desligar buzzer;
- atualizar display.

Essa abordagem facilita manutenção e futuras expansões.

---

# 14. Máquina de Estados

Fluxo simplificado:

Inicialização

↓

Busca posição HOME

↓

Modo de espera

↓

Horário alcançado

↓

Alarme

↓

Confirmação

↓

Dispensação

↓

Aguardando retirada

↓

Registro

↓

Retorno ao modo de espera

---

# 15. Engenharia de Software

O projeto adotará princípios modernos de desenvolvimento.

## SOLID

Principalmente:

- Single Responsibility Principle;
- Open/Closed Principle.

---

## Clean Code

- nomes claros;
- funções pequenas;
- baixo acoplamento;
- alta coesão.

---

## Git

Controle de versão desde o primeiro dia.

Branches sugeridas:

- main
- software
- hardware
- mecanica
- testes

---

## Kanban

Organização das atividades:

- Backlog
- A Fazer
- Em Desenvolvimento
- Em Teste
- Concluído

---

## Sprints

Reuniões semanais para integração dos módulos.

---

# 16. Organização da Equipe

## Desenvolvimento de Software - Bianca

Responsável por:

- arquitetura;
- programação;
- integração;
- testes.

---

## Eletrônica - Wanessa

Responsável por:

- circuito;
- sensores;
- motores;
- alimentação;
- montagem.

---

## Mecânica - Alany

Responsável por:

- modelagem CAD;
- impressão 3D;
- testes mecânicos;
- ajustes estruturais.

---

# 17. Indicadores de Validação

O Falcon será avaliado através de indicadores objetivos.

- funcionamento correto da dispensação;
- precisão do posicionamento;
- funcionamento contínuo sem travamentos;
- registro correto dos eventos;
- tempo de resposta do sistema;
- custo final do protótipo;
- consumo energético;
- facilidade de configuração.

---

# 18. Cronograma

## Fase 1 – Planejamento (Julho)

- levantamento de requisitos;
- arquitetura;
- definição dos componentes;
- compra de materiais.

---

## Fase 2 – Desenvolvimento Inicial

- software básico;
- display;
- RTC;
- menus;
- armazenamento.

---

## Fase 3 – Desenvolvimento Mecânico

- impressão;
- montagem;
- mecanismo de rotação;
- sensores.

---

## Fase 4 – Integração

- software;
- eletrônica;
- mecânica.

---

## Marco – 17 de Agosto

Protótipo funcional contendo:

- configuração de horários;
- alarme;
- posicionamento;
- dispensação;
- detecção da retirada;
- registro local.

---

## Fase 5 – Refinamento

Até metade de setembro.

- calibração;
- testes;
- documentação;
- correções.

---

# 19. Critérios de Aceite

O Falcon será considerado funcional quando:

- localizar corretamente a posição HOME;
- posicionar qualquer compartimento corretamente;
- dispensar o medicamento correspondente;
- detectar retirada do copo;
- registrar corretamente os eventos;
- manter horários após desligamento;
- operar continuamente durante testes prolongados.

---

# 20. Preparação para o TCC

A arquitetura será preparada para reutilização.

Na IC:

Sistema Embarcado

↓

Persistência Local

↓

Interface Local

No TCC serão adicionados:

- Wi-Fi;
- API REST;
- Banco de Dados;
- Dashboard Web;
- Relatórios;
- Estatísticas;
- Notificações;
- Atualizações OTA.

Nenhum desses recursos exigirá reescrever o núcleo do software.

---

# 21. Conclusão

O Falcon será desenvolvido como um **produto de engenharia**, e não apenas como um protótipo acadêmico. O projeto seguirá uma abordagem baseada em levantamento de requisitos, desenvolvimento incremental, modularização de hardware e software, integração contínua e validação por indicadores objetivos.

Essa estratégia permitirá que a Iniciação Científica entregue um sistema funcional, confiável e tecnicamente consistente, ao mesmo tempo em que estabelece uma base sólida para o Trabalho de Conclusão de Curso. A evolução futura poderá concentrar esforços na conectividade, monitoramento remoto e análise de dados, preservando toda a arquitetura desenvolvida na IC e reduzindo significativamente o retrabalho.
