---
layout: page
title: Política de Privacidade
description: SupportAssistant — extensão Chrome
---

# Política de Privacidade — SupportAssistant

**Última atualização:** abril de 2026

---

## Visão geral

SupportAssistant é uma extensão para Google Chrome distribuída pela Chrome Web Store, voltada para agentes que prestam atendimento técnico em plataformas SaaS de relacionamento com clientes.

A extensão **opera inteiramente no navegador do usuário**. Todo o processamento ocorre localmente, na máquina onde está instalada. **Nenhuma informação pessoal ou de uso é coletada, armazenada em servidores externos ou transmitida a terceiros pelo desenvolvedor da extensão.**

---

## Dados processados pela extensão

A extensão processa, exclusivamente no navegador do usuário, os seguintes tipos de dados:

### Atalhos de texto e configurações do usuário
Atalhos de texto criados pelo usuário, preferências de formatação por plataforma, configurações do sinalizador de inatividade e do botão flutuante são armazenados via API `chrome.storage.local`. Esses dados ficam na máquina do usuário e podem ser exportados em arquivo CSV a qualquer momento pela própria extensão.

### Histórico de uso recente
Lista dos últimos atalhos utilizados, armazenada localmente apenas para exibição na interface da extensão.

### Conteúdo das páginas autorizadas
A extensão lê o DOM das páginas onde está autorizada a operar (nome do cliente em atendimento, documento exibido em cards laterais, timestamps de mensagens para detecção de inatividade). Esses dados são usados **exclusivamente em tempo real** para as automações operacionais ativadas pelo próprio usuário. Não são persistidos pela extensão. Não são transmitidos a nenhum servidor.

### Documento do cliente em fluxo automatizado
Durante a execução do fluxo de busca automática de clientes, o documento (CNPJ) é mantido exclusivamente em **memória de sessão** (API `chrome.storage.session`), cifrado em **AES-GCM** com chave gerada aleatoriamente a cada sessão. É descartado automaticamente ao fechar o navegador. Nunca é persistido em disco em texto claro.

---

## Origens autorizadas

A extensão atua apenas nas seguintes origens, declaradas em seu manifesto e exibidas pela Chrome Web Store no momento da instalação:

- **Central de atendimento ao cliente** — `*.octadesk.com`, `*.octadesk.app`
- **Sistema de tickets** — `www.bling.com.br`
- **Site dos Correios** — `buscacepinter.correios.com.br` *(para preenchimento automático de CEP)*

Em qualquer outra página da web, a extensão permanece inativa e não tem acesso ao conteúdo.

---

## Comunicação externa

A extensão **não realiza chamadas a servidores próprios do desenvolvedor**. Não há analytics, telemetria, tracking, envio de relatórios de uso ou qualquer comunicação com infraestrutura controlada pelo desenvolvedor.

A interação da extensão se restringe às mesmas plataformas que o usuário já acessa em seu fluxo de trabalho normal — nas quais ela apenas lê elementos da interface e automatiza ações que o próprio usuário realizaria manualmente.

---

## Recursos empacotados

Todos os recursos utilizados pela extensão (ícones, sons de alerta, scripts) estão empacotados dentro do arquivo `.crx` distribuído pela Chrome Web Store. A extensão **não carrega recursos de servidores externos em tempo de execução** e funciona offline para seus recursos próprios.

---

## Controle do usuário sobre seus dados

- Todos os dados manipulados pela extensão permanecem na máquina do usuário.
- O usuário pode **exportar** seus atalhos a qualquer momento, através da função de backup em arquivo CSV disponível na tela de configurações.
- O usuário pode **remover** todos os dados da extensão desinstalando-a pelo menu `chrome://extensions`. A desinstalação apaga integralmente o storage da extensão.
- O usuário pode **desativar** módulos individualmente (atalhos, formatador, sinalizador, botão flutuante) através das configurações.

---

## Compartilhamento de dados

O desenvolvedor da extensão certifica que:

- **Não vende e não transfere** dados do usuário a terceiros, fora dos casos de uso aprovados.
- **Não usa nem transfere** dados do usuário para fins não relacionados ao único propósito declarado da extensão.
- **Não usa nem transfere** dados do usuário para determinar credibilidade ou para fins de empréstimo.

---

## Atualizações da extensão

Atualizações da extensão são distribuídas exclusivamente pela Chrome Web Store. O navegador do usuário verifica e instala atualizações automaticamente, em background, conforme a política padrão do Chrome. **As preferências e os atalhos do usuário são preservados** durante atualizações — apenas a desinstalação manual remove os dados.

---

## Alterações nesta Política

Esta Política de Privacidade pode ser atualizada para refletir mudanças em funcionalidades futuras da extensão. Versões anteriores podem ser consultadas no histórico de commits deste repositório. A data da última atualização sempre estará indicada no topo do documento.

---

## Contato

Para dúvidas sobre esta política, utilize o canal de suporte registrado na página da extensão na Chrome Web Store.
