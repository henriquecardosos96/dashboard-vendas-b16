# 📊 Dashboard Semanal de Vendas — Agência B16

Dashboard de performance semanal desenvolvido pela **Agência B16** para acompanhamento consolidado das vendas de todos os clientes da carteira.

🔗 **Acesse o dashboard:** https://henriquecardosos96.github.io/dashboard-vendas-b16/

---

## 🎯 Sobre o projeto

Este dashboard centraliza e visualiza os dados de vendas semanais de todos os clientes da B16, permitindo uma visão rápida e comparativa do desempenho a cada semana. O report é publicado toda **sexta-feira às 10h** e compartilhado com a equipe via Telegram.

Os dados são lidos automaticamente do Google Sheets, consolidados por um script (Google Apps Script) e atualizados a cada 2 horas no dashboard.

---

## 👥 Clientes monitorados

| Cliente | Plataforma | Status |
|---|---|---|
| Maestro Thiago Santos | Kiwify | ✅ Ativo |
| Revista Catolicismo | Kiwify | ✅ Ativo |
| Mundial Cromo | Kiwify | ✅ Ativo (captação) |
| Carlos Nougué | Kiwify | ✅ Ativo |

---

## 📦 Fonte de dados

| Fonte | Descrição | Atualização |
|---|---|---|
| Google Sheets — `BASE_TOTAL_SEMANAL_at` | Base consolidada com dados de vendas de todos os clientes | Automática toda sexta às 10h via Apps Script |
| Kiwify (webhooks) | Cada venda aprovada é enviada em tempo real para a planilha de cada cliente | Tempo real |

**Regras de processamento:**
- Vendas = contagem de `order_ref` únicos com `order_status = paid`
- Semana = domingo a sexta (fuso horário: America/Sao_Paulo)
- Faturamento = campo `Faturamento` da Kiwify (líquido de taxas)

---

## 📈 O que o dashboard exibe

### 📊 Visão Geral
- Total de vendas e faturamento da semana
- Variação percentual (▲▼) vs semana anterior
- Barra com dados da semana anterior
- 🏆 Produto que mais vendeu
- Gráfico de faturamento por cliente com comparativo

### 👥 Por Cliente
- Tabela: Cliente | Vendas | Faturamento | Ticket Médio | Produto Destaque
- Variação individual por cliente vs semana anterior

### 📦 Por Produto
- Ranking de todos os produtos vendidos na semana
- Barra dupla: volume de vendas + faturamento

### 📈 Histórico
- Gráfico de faturamento por semana desde fevereiro/2026
- Semana atual destacada em amarelo

---

## ⚙️ Automação — Google Apps Script

O arquivo `consolidar_vendas_v2.gs` contém o script de consolidação automática.

**Como funciona:**
1. Acessa as 4 planilhas dos clientes via Google Sheets API
2. Filtra vendas pagas da semana atual (domingo a sexta)
3. Agrupa por cliente e produto
4. Limpa e regrava os dados na aba `BASE_TOTAL_SEMANAL_at`
5. Executa automaticamente toda sexta às 10h (horário de Brasília)

**Para instalar:**
1. Abra a planilha consolidada → Extensões → Apps Script
2. Cole o conteúdo do arquivo `.gs`
3. Execute `criarGatilho` uma vez para agendar
4. Execute `consolidarSemanaAtual` para testar

---

## 🛠️ Tecnologias utilizadas

- **HTML/CSS/JS** puro — sem frameworks
- **Google Sheets** como banco de dados via CSV público
- **Google Apps Script** para consolidação automática
- **Kiwify Webhooks** para captura de vendas em tempo real
- **GitHub Pages** para hospedagem gratuita via HTTPS

---

## 🔄 Fluxo completo
Kiwify (venda aprovada)
↓ webhook em tempo real
Planilha de cada cliente (Google Sheets)
↓ Apps Script toda sexta às 10h
BASE_TOTAL_SEMANAL_at (planilha consolidada)
↓ fetch a cada 2h
Dashboard (GitHub Pages)
↓ toda sexta
Grupo do Telegram da firma

---

## 📋 Changelog

### v2 · 10/04/2026
`fix: parseNum - corrigir leitura de faturamento no formato americano do Sheets`
- Corrigido bug de parsing de números (R$ 37.105,90 aparecia como R$ 37,11)
- Removidos elementos de status do header (botão atualizar, badge ao vivo)
- Data da semana fixada no header

### v1 · 10/04/2026
`feat: dashboard semanal de vendas B16`
- Big numbers: Total de Vendas + Faturamento com delta vs semana anterior
- 4 abas: Visão Geral, Por Cliente, Por Produto, Histórico
- Comparativo automático com semana anterior
- Gráfico histórico de faturamento por semana
- Script de consolidação automática (Google Apps Script)
- Lembrete semanal criado no Google Calendar (toda sexta às 10h)

---

## 🏢 Desenvolvido por

**Agência B16** — Hub Estratégico de Marketing Digital
