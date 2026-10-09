# SEED Labs — Segurança Web

Relatórios técnicos de dois laboratórios de segurança web da plataforma educacional [SEED Labs](https://seedsecuritylabs.org/) (Syracuse University, Prof. Wenliang Du), executados em ambiente controlado para fins acadêmicos.

> **Autor:** Guilherme Carvalho Santos — Faculdade de Computação, Universidade Federal de Uberlândia (UFU)
> **Disciplina:** Segurança Web — Prof. Kil Jin Brandini Park

Os relatórios seguem o padrão ABNT (capa, sumário, figuras e referências) e documentam, de cada laboratório: a familiarização com o alvo, a exploração passo a passo, a **contramedida** que elimina a falha e as considerações finais.

## Relatórios

| Laboratório | Relatório | Tema |
|---|---|---|
| **SQL Injection Attack Lab** | [`Relatorio_SQL_Injection.pdf`](Relatorio_SQL_Injection.pdf) | Injeção de SQL em `SELECT`/`UPDATE`, bypass de autenticação e adulteração de registros |
| **Cross-Site Scripting (XSS) Attack Lab** (Elgg) | [`Relatorio_XSS_Elgg.pdf`](Relatorio_XSS_Elgg.pdf) | XSS persistente, requisições forjadas no contexto da vítima e worm auto-propagável |

## Resumo dos laboratórios

### 🛢️ SQL Injection (aplicação de gestão de funcionários)
Exploração de uma aplicação que monta comandos SQL por **concatenação de strings**, sem separar código de dados:
- bypass de autenticação para acesso como administrador sem conhecer a senha;
- vazamento de dados sensíveis de todos os funcionários;
- alteração de registros próprios e de terceiros via injeção em `UPDATE`;
- análise de por que o encadeamento de comandos (`;`) falha com `mysqli::query()`.
- **Contramedida:** reescrita das consultas com **prepared statements** (`bind_param`), separando estrutura e dados — o ataque deixa de funcionar.

### 🕸️ Cross-Site Scripting / XSS (rede social Elgg)
Exploração de campos de perfil que aceitam HTML sem tratamento, caracterizando **XSS persistente (stored)**:
- execução de código arbitrário no navegador da vítima;
- leitura e exfiltração do cookie de sessão;
- requisições autenticadas forjadas (adicionar amizade, editar perfil) usando os próprios tokens anti-CSRF da página;
- construção de um **worm** que se copia para o perfil da vítima e se auto-propaga.
- **Contramedida:** **Content Security Policy (CSP)** restritiva (sem `unsafe-inline`), combinada com escape/filtragem de saída.

## Ambiente

Como os equipamentos usados são MacBook com **Apple Silicon (ARM64)** — incompatíveis com a VM oficial x86/VirtualBox da SEED —, o ambiente foi reconstruído de forma equivalente:

- **Virtualização:** UTM + Ubuntu Server 22.04 LTS (ARM64)
- **Conteinerização:** Docker / Docker Compose com o pacote `Labsetup-arm.zip`
- **Acesso:** SSH a partir do Terminal do macOS

## Aviso

Todo o conteúdo é **estritamente educacional** e foi executado em ambiente isolado e controlado (contêineres locais da SEED Labs), sobre aplicações **propositalmente vulneráveis**. Não utilize estas técnicas contra sistemas sem autorização explícita.

## Referências

- SEED Labs — [SQL Injection Attack Lab](https://seedsecuritylabs.org/Labs_20.04/Web/Web_SQL_Injection/)
- SEED Labs — [Cross-Site Scripting (XSS) Attack Lab (Elgg)](https://seedsecuritylabs.org/Labs_20.04/Web/Web_XSS_Elgg/)
