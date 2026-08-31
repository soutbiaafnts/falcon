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
- [Critérios de Aceite](#18-critérios-de-aceite)
- [Preparação para o TCC](#19-preparação-para-o-tcc)
- [Conclusão](#20-conclusão)

---

# 1. Introdução

O Falcon é um sistema embarcado para dispensação automática de medicamentos desenvolvido com foco na autonomia de idosos e na redução da necessidade de acompanhamento constante por cuidadores.

O projeto integra conceitos de Sistemas Embarcados, Internet das Coisas (IoT), Automação, Engenharia de Software, Robótica e Modelagem 3D para desenvolver um dispositivo de baixo custo, modular e preparado para futuras expansões.

A Iniciação Científica terá como foco o desenvolvimento de um protótipo funcional capaz de armazenar medicamentos, realizar a dispensação automática em horários programados, registrar eventos e fornecer uma interface simples para pacientes e cuidadores.

O Trabalho de Conclusão de Curso será uma evolução natural deste projeto, incorporando comunicação via Internet e geração de relatórios.

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
- impedir a dispensação de outros medicamentos em ausência de retirada;
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
   - considera o horário encerrado e trava o próximo evento programado até que a retirada seja detectada.

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

A haste central será movimentada por um servo motor 360˚.

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
- servo motor 360˚.

---

## Sensores

- célula de carga + HX711;
- sensor Hall e ímã de neodímio para posição HOME.

---

## Alimentação

- fonte externa;
- bateria recarregável;
- conversor DC-DC.

## Valores

- [ESP32 DevKit V1](https://www.mercadolivre.com.br/esp32-30-pino-doit-devkit-com-esp32-wroom-32-wifi-bluetooth/p/MLB2038780923?pdp_filters=item_id:MLB3914402941#is_advertising=true&searchVariation=MLB2038780923&backend_model=search-backend;EQ:ESP32%20NODEMCU;EQ:ESP32%20WROOM&be_origin=backend&position=1&search_layout=grid&type=pad&tracking_id=4d1debf9-8a6a-42a1-9800-cc507a36f91b&ad_domain=VQCATCORE_LST&ad_position=1&ad_click_id=ZTYwMzdhODEtMTA4Yi00Y2VhLWEyMmYtZTY1MDQ5N2Q4Y2Q1): R$ 32,70
- [RTC DS3231](https://www.mercadolivre.com.br/modulo-real-time-rtc-ds3231/p/MLB41384231?pdp_filters=item_id:MLB4970079878#is_advertising=true&searchVariation=MLB41384231&backend_model=search-backend;EQ:MODULO%20RTC;EQ:RTC%20DS3231%20MODULO;EQ:MODULO%20RTC%203231;EQ:RTC%20DS3231%20ARDUINO&be_origin=backend&position=1&search_layout=grid&type=pad&tracking_id=c17a0cc6-e659-4e7b-901a-14bb75c5008c&ad_domain=VQCATCORE_LST&ad_position=1&ad_click_id=N2ExN2VmZjctZGYzOC00YzhkLTgxMzYtOGUyZDRiMzZlN2Rj): R$ 19,19
- [Display OLED 128x64 I²C](https://www.mercadolivre.com.br/modulo-display-oled-tela-096-i2c-ssd1306-lcd-arduino-pic/up/MLBU773901547?pdp_filters=item_id:MLB3892633142#is_advertising=true&searchVariation=MLBU773901547&backend_model=search-backend;EQ:SSD1306;EQ:OLED%20096%20I2C;EQ:DISPLAY%20OLED%20128X64%20I2C%20AZUL;EQ:DISPLAY%20OLED%20128X64%20I2C&be_origin=backend&position=1&search_layout=grid&type=pad&tracking_id=63dfb182-08c7-4a85-abdb-91708b91d7fa&ad_domain=VQCATCORE_LST&ad_position=1&ad_click_id=ZTk4MDMwMDMtZDIwNC00YTVmLThhZmUtYmNkZDAzMGViN2Ji): R$ 17,98
- [4 botões](https://www.mercadolivre.com.br/kit-com-500--chave-tactil-6x6x5mm-4t-180-graus/up/MLBU3226780648?pdp_filters=item_id:MLB4087872511#polycard_client=recommendations_vip-pads-up&wid=MLB4087872511&sid=recos&reco_backend=recomm_platform_base_pads_rfa_MERGE_marketplace&reco_model=recos_backend_only&reco_client=vip-pads-up&reco_item_pos=2&reco_backend_type=low_level&reco_id=7c3d9f05-d357-4f24-a1d6-46cf5ef65fd5&is_advertising=true&ad_domain=VIPDESKTOP_UP&ad_position=3&ad_click_id=NTk4YmRhMzMtNDkyMS00NGJiLWE2MWMtZWU3ODlmNWRiNzQ3): ≃ R$ 0,38
- [Buzzer ativo](https://www.mercadolivre.com.br/buzzer-ativo-5v-sinal-beep-arduino-raspberry-som/up/MLBU3872444152?pdp_filters=item_id:MLB6524026378#is_advertising=true&searchVariation=MLBU3872444152&backend_model=search-backend;EQ:BUZZER%205V;EQ:BUZZER%20ATIVO%205V&be_origin=backend&position=3&search_layout=grid&type=pad&tracking_id=111eae54-e435-4e59-ac77-3eb81cb5ed3e&ad_domain=VQCATCORE_LST&ad_position=3&ad_click_id=YzRmZGM3MmEtZGNlNi00NmRjLWIzN2MtYzQzYjFlZDcwNGEz): R$ 7,92
- [Servo motor 360˚](https://www.mercadolivre.com.br/servo-motor-tower-pro-mg90d-360-graus/p/MLB68229896#polycard_client=search-desktop&be_origin=backend&overlay_label=not_apply&search_layout=grid&position=7&type=product&tracking_id=ab3f713d-84e9-4777-bbec-be6a654796b7&wid=MLB6655136984&sid=search): R$ 33,44
- [Célula de carga + HX711](https://www.mercadolivre.com.br/1-celula-de-carga-1kg-sensor-peso--1-modulo-hx711-arduino/up/MLBU750020937?pdp_filters=item_id:MLB2693893440#is_advertising=true&searchVariation=MLBU750020937&backend_model=search-backend;EQ:CELULA%20CARGA%2010KG&be_origin=backend&position=1&search_layout=grid&type=pad&tracking_id=721b0252-50d7-46a9-80fa-e40b20ddbfcb&ad_domain=VQCATCORE_LST&ad_position=1&ad_click_id=YmZmOTcxMTEtNDdkOS00NjNmLThlYzItYTA3MjZmMjcyMThm): R$ 27,92
- [Sensor Hall](https://www.mercadolivre.com.br/kit-10-sensores-magnetico-de-efeito-hall-ss41f-41f-c-nfe/up/MLBU755274844?pdp_filters=item_id:MLB2855778087#is_advertising=true&searchVariation=MLBU755274844&backend_model=search-backend;EQ:SENSOR%20EFEITO%20HALL&be_origin=backend&position=3&search_layout=grid&type=pad&tracking_id=04c8adaf-76b5-4a32-be34-4bbb23488635&ad_domain=VQCATCORE_LST&ad_position=3&ad_click_id=Yjc0OWZiODItYjc0Yi00NTRjLWE1MzUtYzlmMTI1ZWI4MmQ0): R$ 2,19
- [Imã de Neodímio](https://www.mercadolivre.com.br/ima-de-neodimio-10x2-redondo-pequeno-10mm-x-2mm-n35-10pcs/p/MLB32490961#polycard_client=search-desktop&be_origin=backend&overlay_label=not_apply&search_layout=grid&position=5&type=product&tracking_id=5e0b6c7d-64b2-4396-afaf-7d3ca2b69a1a&wid=MLB5320606870&sid=search): R$ 2,22
- [Fonte externa](): R$
- [Bateria recarregável](): R$
- [Conversor DC-DC](): R$

**Total:** ≃ R$ 143,94

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

# 18. Critérios de Aceite

O Falcon será considerado funcional quando:

- localizar corretamente a posição HOME;
- posicionar qualquer compartimento corretamente;
- dispensar o medicamento correspondente;
- detectar retirada do copo;
- registrar corretamente os eventos;
- manter horários após desligamento;
- operar continuamente durante testes prolongados.

---

# 21. Preparação para o TCC

A arquitetura será preparada para reutilização.

Na IC:

Sistema Embarcado

↓

Persistência Local

↓

Interface Local

No TCC serão adicionados:

- Wi-Fi;
- Relatórios;
- Estatísticas;
- Notificações;

Nenhum desses recursos exigirá reescrever o núcleo do software.

---

# 21. Conclusão

O Falcon será desenvolvido como um **produto de engenharia**, e não apenas como um protótipo acadêmico. O projeto seguirá uma abordagem baseada em levantamento de requisitos, desenvolvimento incremental, modularização de hardware e software, integração contínua e validação por indicadores objetivos.

Essa estratégia permitirá que a Iniciação Científica entregue um sistema funcional, confiável e tecnicamente consistente, ao mesmo tempo em que estabelece uma base sólida para o Trabalho de Conclusão de Curso. A evolução futura poderá concentrar esforços na conectividade e análise de dados, preservando toda a arquitetura desenvolvida na IC e reduzindo significativamente o retrabalho.
