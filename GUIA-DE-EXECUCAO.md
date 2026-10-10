# Guia de Execução — Trabalho 1 (Sistema Adversarial)

Este documento existe para que **qualquer integrante do grupo** consiga continuar o trabalho sem depender de explicação verbal. Ele não faz parte do relatório entregue (o relatório é o `README.md`) — é um guia operacional interno.

**Prazo registrado no enunciado: 06/10/2026 às 23:59.** Como a revisão de fechamento foi realizada em 10/10/2026, confirmar no site da atividade qualquer nova orientação sobre prazo; este guia não presume prorrogação.

**Composição final informada pelo grupo:** Eduardo dos Santos Paim, Felipe H. Scherer, Rafael da Silva Moral e Lucas Correa Rodrigues. Atualizar também a capa dos slides e o cadastro da atividade, quando aplicável.

**Sistema escolhido:** compra de ingressos durante a abertura das vendas gerais de um evento com estoque limitado (fila virtual). Atores: comprador legítimo, revendedor/scalper, plataforma (defensor). Ver `README.md` seção 3.1 para o detalhamento já pronto.

---

## 1. Visão geral das etapas

| # | Etapa | Seção do relatório | Depende de | Status |
|---|---|---|---|---|
| 1 | Escolha e delimitação do sistema | Introdução do README | — | ✅ Concluída |
| 2 | Descrição do sistema adversarial | README § 3.1 | Etapa 1 | ✅ Concluída |
| 3 | Modelo estratégico estático | README § 3.2 | Etapa 2 | ✅ Concluída |
| 4 | Modelo estratégico dinâmico | README § 3.3 | Etapa 3 | ✅ Concluída |
| 5 | Ameaças e riscos | README § 3.4 | Etapas 2–4 | ✅ Concluída |
| 6 | Montagem final do repositório (declaração de IA, referências, contribuições) | README (final) | Etapas 2–5 | ✅ Consolidada; confirmar declaração de IA com os integrantes |
| 7 | PDF e vídeo final | externo (Canva/YouTube/site da atividade) | Etapas 2–6 | 🔲 Conferência e entrega externas pendentes |
| 8 | Revisão final + checklist | — | Etapas 1–7 | ✅ Relatório revisado; entrega externa ainda não validada |

Cada etapa abaixo diz **o que produzir**, **em qual arquivo** e **o que não pode faltar**, para que qualquer pessoa do grupo consiga pegar uma etapa e executar sozinha.

---

## Etapa 3 — Modelo estratégico estático (README § 3.2)

**O que fazer:**
1. Escolher **uma decisão central** do sistema e modelá-la como jogo 2x2 (duas ações para cada jogador). Sugestão: **Scalper** (ação A1 = "comprar manualmente/normal", A2 = "usar bots/múltiplas contas") vs. **Plataforma** (ação B1 = "não verificar / verificação fraca", B2 = "aplicar CAPTCHA + limite rígido por CPF").
2. Montar a matriz de payoffs usando valores de 0 a 3 (ordem de preferência), deixando explícito o par `(payoff do Jogador A, payoff do Jogador B)`.
3. Justificar, em texto, **por que** cada resultado recebeu aqueles valores (não pode ser arbitrário).
4. Identificar as **melhores respostas** de cada jogador a cada ação do outro.
5. Dizer se existe **estratégia dominante** para algum jogador.
6. Identificar se existe um **equilíbrio de Nash** (resultado em que nenhum jogador melhora mudando sozinho) — não precisa existir; se não existir, diga isso e explique por quê.
7. Avaliar se o resultado encontrado é bom ou ruim para o sistema e para os usuários legítimos.

**Não pode faltar:** a tabela de payoffs, a explicação dos payoffs, a análise de melhores respostas, e a conclusão sobre equilíbrio.

**Erro comum a evitar:** payoff sem justificativa, ou marcar "equilíbrio" sem mostrar a análise de melhor resposta que leva a ele.

---

## Etapa 4 — Modelo estratégico dinâmico (README § 3.3)

**O que fazer:**
1. Pegar o jogo da Etapa 3 e **transformá-lo em uma sequência de pelo menos 3 rodadas**, seguindo o ciclo `ação → resposta → observação → adaptação`.
2. Preencher a tabela de rodadas (ação do participante, resposta do sistema, o que se torna observável, adaptação para a rodada seguinte). Use a história do scalper tentando burlar a plataforma e a plataforma reagindo, igual ao descrito na § 3.1 ("por que é adversarial").
3. Garantir que a sequência mostre: a resposta do sistema também gera informação; o scalper muda de ação mas mantém o objetivo; a plataforma também se adapta; decisões passadas afetam rodadas seguintes; a defesa tem custo para usuários legítimos (ex.: CAPTCHA mais difícil atrasa compradores reais também).
4. Criar o diagrama do ciclo adaptativo em Mermaid e salvar a fonte em `diagramas/ciclo-adaptativo.mmd` (+ exportar PNG para `diagramas/ciclo-adaptativo.png`), embedando também no README.
5. Responder as 5 perguntas finais da seção 3.3 do enunciado (quem observa quem; o que cada lado consegue mudar; o que dispara adaptação; custo da adaptação para cada lado; onde pode surgir uma corrida armamentista).

**Não pode faltar:** as 3 rodadas completas, o diagrama, e as 5 respostas finais.

---

## Etapa 5 — Ameaças e riscos (README § 3.4)

**O que fazer:**
1. Listar **pelo menos 3 pontos de exploração** no sistema/rodadas modeladas (ex.: endpoint de compra sem rate limit, validação de CPF sem checagem de duplicidade real, CAPTCHA contornável por farm de cliques).
2. Criar o diagrama de superfície de ataque (Mermaid) mostrando essas interfaces/fluxos, salvar fonte em `diagramas/superficie-de-ataque.mmd` (+ PNG), embedar no README.
3. Descrever **pelo menos 3 cenários de ameaça** no formato exato pedido: *"Um [ator] pode realizar [ação] por meio de [ponto de exploração], aproveitando [fraqueza/pressuposto], causando [impacto] sobre [ativo]."*
4. Montar a tabela de risco (ID, cenário, ponto de exploração, pressuposto, ativo afetado, probabilidade 1-3, impacto 1-3, risco = probabilidade × impacto).
5. Escolher a ameaça de **maior risco** e responder: como o sistema responderia; que informação essa resposta revela ao adversário; como ele se adaptaria na rodada seguinte; efeitos colaterais sobre usuários legítimos; risco residual; o que precisa continuar sendo preservado.

**Não pode faltar:** o diagrama de superfície de ataque, as 3 ameaças no formato pedido, a tabela de risco, e a análise da ameaça prioritária com adaptação seguinte e risco residual (não apresentar a defesa como solução definitiva).

**Consistência obrigatória:** as ameaças aqui devem conectar com os atores/ativos da Etapa 2 e com as rodadas da Etapa 4 — não usar ameaças genéricas que não aparecem no sistema analisado.

---

## Etapa 6 — Montagem final do repositório

**O que fazer:**
1. **Declaração de uso de IA** (seção final do README): para quais tarefas de IA generativa foi usada (ex.: estruturação do texto, geração de diagramas Mermaid), e como o grupo verificou/validou o conteúdo (releitura crítica, comparação com a teoria vista em aula, ajustes manuais).
2. **Referências** (`fontes/referencias.md`): qualquer fonte externa usada (artigos, documentação de plataformas de ingresso, notícias sobre scalping, etc.), em formato simples (autor/título, link, data de acesso).
3. **Contribuições individuais** (seção final do README): nome de cada integrante e resumo do que fez — deve bater com o histórico de commits do GitHub.
4. Conferir se os 3 diagramas exigidos existem em `diagramas/` tanto embutidos no README quanto como arquivo-fonte editável (e PNG, se a ferramenta permitir exportar).
5. Revisar se o `README.md` é **autossuficiente** (dá pra entender tudo sem abrir outro arquivo que não esteja referenciado nele).

---

## Etapa 7 — Slides e vídeo de apresentação

**O que fazer:**
1. Transformar cada seção do README em 1-2 slides (não copiar texto corrido — usar a tabela de atores, a matriz de payoffs, a tabela de rodadas, o diagrama de superfície de ataque e a tabela de risco como slides visuais).
2. Estrutura sugerida: (1) o sistema e a interação escolhida, (2) atores e conflito, (3) modelo estático, (4) modelo dinâmico, (5) ameaças e risco priorizado, (6) o que o sistema precisa preservar / próximos passos para o Trabalho 2.
3. Gravar o vídeo no Canva com os quatro integrantes participando (balancear a fala — é critério de nota individual), subir no YouTube e entregar o link no site da atividade. O vídeo exportado deve ter no máximo **10 minutos**, conforme a orientação posterior do professor. Não basta conferir as durações de cada slide isoladamente.
4. Exportar a apresentação em PDF, disponibilizá-la com acesso para avaliação e entregar o link no site da atividade. Registrar os links no README é opcional, não uma exigência do enunciado.
5. Conferir que os slides cobrem as seções 3.1–3.4, que não restam textos do template e que o áudio de cada integrante termina junto de seu slide sem cortes ou elementos desaparecendo. Remover Saimon e Jian da capa conforme a composição final informada.

Uma divisão possível para o vídeo é: 2 minutos para sistema/atores, 2 minutos para modelo estático, 2 minutos para modelo dinâmico e 2 minutos para ameaças/resposta. Reservar até 1 minuto para abertura, conclusão e transições, mirando 9 minutos no total. É uma sugestão; a fala real deve ser equilibrada entre os quatro integrantes.

O endereço de edição do Canva não substitui o PDF nem a publicação do vídeo no YouTube. A conferência dos arquivos finais e a submissão são etapas externas ao relatório.

---

## Etapa 8 — Revisão final (antes de entregar)

Confira usando o checklist oficial do enunciado (seção 6):

- [x] interação específica e bem delimitada
- [x] atores, objetivos, ativos, capacidades, informações e pressupostos
- [x] matriz de payoffs explicada
- [x] pelo menos 3 rodadas de ação/resposta/observação/adaptação
- [x] os 3 diagramas solicitados (contexto, superfície de ataque, ciclo adaptativo), PNGs e fontes editáveis
- [x] pelo menos 3 ameaças ligadas ao sistema analisado
- [x] avaliação de probabilidade, impacto e risco
- [x] resposta à ameaça prioritária, próxima adaptação e risco residual
- [x] referências, declaração de uso de IA e contribuições individuais registradas
- [ ] declaração de IA confirmada pelos quatro integrantes, incluindo outros usos que tenham feito
- [ ] capa e cadastro da atividade correspondem à composição final do grupo
- [ ] PDF final sem placeholders e com todas as partes do trabalho
- [ ] vídeo no YouTube com até 10 minutos, fala equilibrada e sem cortes de áudio
- [ ] links de PDF e vídeo acessíveis aos avaliadores e submetidos no site da atividade

---

## 2. Como dividir entre o grupo (sugestão para 4-6 pessoas)

Como as etapas têm dependência sequencial (3.2 → 3.3 → 3.4), a forma mais rápida de paralelizar **sem perder coerência** é:

1. Uma dupla fecha a Etapa 3 (modelo estático) primeiro, pois as demais dependem dela.
2. Assim que o jogo estático estiver definido, uma pessoa/dupla parte para a Etapa 4 (dinâmico) e outra para rascunhar a Etapa 5 (ameaças), já que ambas podem usar os mesmos atores/pressupostos da Etapa 2.
3. Uma pessoa cuida dos diagramas (Mermaid) conforme cada etapa fecha o conteúdo.
4. Uma pessoa cuida da Etapa 6 (montagem final) e dos slides (Etapa 7), consolidando o que as outras produziram.
5. Todo mundo revisa a Etapa 8 junto, pois **cada integrante precisa entender e saber explicar todas as decisões**, não só a parte que escreveu.

## 3. Fluxo de trabalho no Git

- Cada pessoa commita **diretamente as seções que escreveu**, com mensagens claras, ex.: `git commit -m "3.2: matriz de payoffs scalper x plataforma"`.
- Não concentrar tudo em um único commit/pessoa — a nota individual depende do histórico de commits aparecer balanceado.
- Antes de editar o `README.md`, puxe a versão mais recente (`git pull`) para evitar conflito, já que é um arquivo único compartilhado.
- Se possível, cada etapa pode ser um commit (ou um pequeno conjunto de commits) separado, para ficar fácil rastrear quem fez o quê.
