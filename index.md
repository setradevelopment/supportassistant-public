---
layout: page
title: Política de Privacidade
description: SupportAssistant — extensão Chrome
---

# Política de Privacidade — SupportAssistant

**Última atualização:** 21 de maio de 2026

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

### Dados do Analista (Perfil)
Informações preenchidas manualmente pelo usuário em Configurações > Perfil (nome do analista, L2 responsável, Supervisor responsável, par de pausa de chat). São armazenadas via `chrome.storage.local` e usadas apenas para substituir variáveis em atalhos de texto (ex: `[L1]`, `[L2]`, `[Supervisor]`). Não são transmitidas a nenhum servidor.

### Rascunhos automáticos de respostas de tickets
Quando o usuário está digitando uma resposta em um ticket e a página é recarregada, a aba é fechada ou o computador é reiniciado antes do envio, o texto do campo de resposta é preservado localmente em `chrome.storage.local`. O conteúdo é **cifrado com AES-GCM** (chave de 256 bits gerada uma única vez por instalação e armazenada na mesma máquina) antes de ser gravado em disco.

A retenção é de **até 1 hora** sem edição: rascunhos com mais de uma hora sem alteração são apagados automaticamente por uma tarefa periódica (`chrome.alarms`), mesmo sem nenhuma aba aberta. O rascunho também é descartado ao enviar a mensagem pelo próprio sistema de tickets ou ao acionar o botão "Limpar" da ferramenta.

O recurso pode ser desativado pelo usuário em Configurações > Ticket > Formatação de Respostas. Ao desativar, todos os rascunhos preservados existentes são apagados imediatamente.

### Pasta de Tickets (organização manual)
O usuário pode criar uma árvore de pastas e subpastas para organizar tickets de seu interesse, salvando o número visível e a URL de cada ticket que escolher. Os dados (nomes de pasta e URLs escolhidas) são armazenados via `chrome.storage.local` sem cifra (informação de organização pessoal, sem PII de cliente).

Não há expiração automática: o conteúdo dessa árvore é gerenciado manualmente pelo usuário (adicionar, editar, remover). Pode ser **exportado** para arquivo JSON e **importado** em outra máquina ou após reinstalação, em Configurações > Pasta de Tickets > Backup.

### Chave da API Gemini (BYOK) e prompts personalizados
Para usar a funcionalidade de Resumo do Atendimento (que aciona o modelo Gemini do Google), cada usuário gera sua **própria chave de API** gratuita em [aistudio.google.com/apikey](https://aistudio.google.com/apikey) e cola na tela de configurações da extensão. A chave é **cifrada com AES-GCM** (chave de 256 bits gerada uma única vez por instalação e armazenada na mesma máquina) antes de ser gravada em `chrome.storage.local`. O desenvolvedor da extensão não tem acesso a essa chave em nenhum momento.

Os prompts (textos enviados ao modelo) que controlam o formato do resumo são armazenados em `chrome.storage.local` (chave `iaPromptsCustom`). O usuário pode editá-los livremente em Configurações > Resumo Atendimento e restaurar os defaults embarcados a qualquer momento. Nenhum dado dos prompts é transmitido a servidores do desenvolvedor.

### Cache de resumos gerados
Cada resumo gerado pelo Gemini é armazenado em `chrome.storage.local` por **até 7 dias**, indexado por atendimento. Após esse prazo, é apagado automaticamente. O usuário pode forçar a geração de um novo resumo a qualquer momento clicando em "Resumir conversa atual" no modal.

---

## Origens autorizadas

A extensão atua apenas nas seguintes origens, declaradas em seu manifesto e exibidas pela Chrome Web Store no momento da instalação:

- **Central de atendimento ao cliente** — `*.octadesk.com`, `*.octadesk.app`
- **Sistema de tickets** — `www.bling.com.br`
- **Site dos Correios** — `buscacepinter.correios.com.br` *(para preenchimento automático de CEP no fluxo legado de consulta)*
- **ViaCEP** — `viacep.com.br` *(para consulta direta de CEP via API pública, sem necessidade de abrir nova aba)*

Em qualquer outra página da web, a extensão permanece inativa e não tem acesso ao conteúdo.

---

## Comunicação externa

A extensão **não realiza chamadas a servidores próprios do desenvolvedor**. Não há analytics, telemetria, tracking, envio de relatórios de uso ou qualquer comunicação com infraestrutura controlada pelo desenvolvedor.

A interação da extensão se restringe às mesmas plataformas que o usuário já acessa em seu fluxo de trabalho normal (nas quais ela apenas lê elementos da interface e automatiza ações que o próprio usuário realizaria manualmente), com uma única exceção declarada:

### Consulta de CEP via ViaCEP

Quando o usuário aciona a função "Buscar" no módulo de Consulta de CEP, o número do CEP digitado é enviado para a API pública [ViaCEP](https://viacep.com.br) (endpoint `https://viacep.com.br/ws/<CEP>/json/`) para obter o endereço correspondente. Os campos retornados incluem CEP, logradouro, bairro, cidade, UF e código IBGE do município (usado em notas fiscais).

Detalhes:
- A requisição é feita exclusivamente a partir da ação manual do usuário (clique em "Buscar" ou tecla Enter).
- Apenas o número do CEP é enviado. Nenhum outro dado pessoal, identificador da extensão, identificador do usuário ou cookie acompanha a chamada (`credentials: 'omit'`).
- A ViaCEP é um serviço público brasileiro de consulta de CEP em operação desde 2014, amplamente utilizado pela comunidade de desenvolvimento.
- O fluxo legado de consulta nos Correios continua disponível como opção alternativa pelo link "clique aqui" exibido junto ao formulário.

### Geração de resumo via Google Gemini (BYOK)

Quando o usuário aciona o botão "✨ Resumo do Atendimento", o histórico textual da conversa ou do ticket aberto é enviado **diretamente do navegador do usuário** para a API do Google Gemini (endpoint `https://generativelanguage.googleapis.com/v1beta/models/<modelo>:generateContent`), autenticando com a chave própria do usuário (BYOK). O retorno (texto do resumo) é exibido no navegador e armazenado em cache local conforme descrito acima.

Detalhes:
- A requisição é feita exclusivamente a partir da ação manual do usuário (clique no botão "✨ Resumo" ou "Resumir conversa atual").
- O conteúdo enviado é o histórico textual visível na tela do atendimento (as mesmas mensagens que o usuário já visualiza).
- Nenhum dado é enviado a servidores do desenvolvedor da extensão. A comunicação ocorre exclusivamente entre o navegador do usuário e a API do Google, com `credentials: 'omit'` (sem cookies ou identificadores adicionais).
- O usuário pode revogar a chave a qualquer momento em [aistudio.google.com/apikey](https://aistudio.google.com/apikey), ou removê-la diretamente das configurações da extensão (botão "Remover chave").
- A política de uso de dados da API do Google Gemini é independente desta política e está disponível em [ai.google.dev/gemini-api/terms](https://ai.google.dev/gemini-api/terms).

---

## Recursos empacotados

Todos os recursos utilizados pela extensão (ícones, sons de alerta, scripts) estão empacotados dentro do arquivo `.crx` distribuído pela Chrome Web Store. A extensão **não carrega recursos de servidores externos em tempo de execução** e funciona offline para seus recursos próprios.

---

## Controle do usuário sobre seus dados

- Todos os dados manipulados pela extensão permanecem na máquina do usuário.
- O usuário pode **exportar** seus atalhos de texto a qualquer momento, através da função de backup em arquivo CSV disponível na tela de configurações.
- O usuário pode **exportar e importar** a árvore da Pasta de Tickets em arquivo JSON, em Configurações > Pasta de Tickets > Backup. A importação oferece modos "Mesclar" (deduplica por nome de pasta e URL no mesmo nível) e "Substituir tudo".
- O usuário pode **visualizar e gerenciar** o espaço ocupado pela extensão em Configurações > Perfil > Armazenamento Local, com detalhamento por categoria (Atalhos do Short Text, Rascunhos de Tickets, Pastas de Tickets, Outros).
- O usuário pode **remover** todos os dados da extensão desinstalando-a pelo menu `chrome://extensions`. A desinstalação apaga integralmente o storage da extensão.
- O usuário pode **desativar** módulos individualmente (atalhos, formatador, sinalizador, botão flutuante, rascunho automático) através das configurações.

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
