# Surf Coach

Um sistema de coaching pessoal para surfistas, construído sobre o Claude Code. Funciona como ter uma equipa de coaching disponível a qualquer hora — que te conhece, se lembra de tudo, e fica mais precisa quanto mais a usas.

---

## O que é isto

Imagina ter acesso a um coach de surf pessoal, mais uma equipa de 14 especialistas em background: psicólogo, fisioterapeuta, nutricionista, especialista em sono, coach de mobilidade, coach de ginásio, coach de técnica de surf, health coach, coach de respiração, médico de medicina chinesa, coach de periodização, life coach, médico psicossomático e guia espiritual.

Não falas com todos eles directamente. O teu coach de surf lê as avaliações deles antes de cada sessão e usa esse contexto para te dar coaching integrado — como um médico de família que fala com os especialistas antes da consulta.

O sistema aprende contigo. Quanto mais sessions registares, mais preciso fica. Um coach com 3 sessões de dados é útil. Um coach com 30 sessões, métricas, objectivos e um programa de ginásio é outra coisa.

---

## O que isto não é

**Não substitui profissionais reais.** Quando algo precisa de uma análise de sangue, de mãos de um fisioterapeuta, ou de avaliação clínica, o sistema diz-te isso directamente e indica-te o caminho. Esse handoff é parte do como funciona, não uma limitação.

**Não é um atalho.** Funciona na proporção do que lhe deres. Logs honestos e regulares fazem um sistema de coaching real. Uso superficial dá resultados superficiais.

**Não é infalível.** Trabalha com o que reportas. Tu és a fonte de verdade — o sistema é o teu parceiro de pensamento, não a tua autoridade.

---

## O que o torna diferente

**Memória que não apaga.** Cada sessão, cada métrica, cada observação fica disponível para sempre. Nunca tens de re-explicar a tua história. O coach retoma exactamente onde parou.

**Uma equipa que comunica.** Os especialistas lêem os relatórios uns dos outros antes de escreverem os seus. O fisioterapeuta sabe o que o coach de ginásio prescreveu. O health coach sabe o que o especialista em sono identificou. Este nível de integração não existe numa equipa humana real.

**Disponível sempre.** Às 23h antes de uma viagem de surf. Num dia de descanso quando queres pensar nos teus objectivos. Logo após sair da água enquanto a sessão ainda está fresca.

**Honesto, não motivacional.** O coach diz-te quando estás a evitar o teu objectivo principal, quando a tua frequência de sessões não bate certo com as tuas ambições, e quando o que planeaste e o que fizeste não são a mesma coisa.

---

## Trade-offs honestos

| O que o coaching AI faz bem | O que um coach humano faz melhor |
|---|---|
| Memória perfeita de todas as sessões | Ler a tua linguagem corporal e energia |
| Equipa integrada que comunica | Observação física directa e avaliação hands-on |
| Disponível sempre, sem marcações | Responsabilização real através de relação |
| Sem ego nem agenda | Reconhecimento intuitivo de padrões ao longo de anos |
| Custo dramaticamente menor | O efeito terapêutico da ligação humana |

---

## Pré-requisitos

- [Claude Code](https://claude.ai/code) instalado
- Subscrição Claude Pro ou acima (necessário para o uso de agentes)
- Git (para clonar e manter o repositório actualizado)

---

## Como começar

### 1. Clonar o repositório

```bash
git clone https://github.com/matildevonreis/surf-coach.git
cd surf-coach
```

### 2. Abrir no Claude Code

```bash
claude
```

### 3. Iniciar o coaching

```
/coach
```

O coach detecta onde estás. Se é a primeira vez, explica o sistema e guia-te pelo setup passo a passo. Não precisas de saber mais nada para começar.

---

## Fluxo de primeiro uso recomendado

O `/coach` detecta automaticamente dados em falta e guia-te — mas se preferires fazer o setup na ordem óptima:

```
/setup-profile     → quem és como surfista
/setup-goals       → 1 a 3 objectivos concretos
/setup-metrics     → baselines de saúde e performance
/setup-activities  → o que treinas fora de água e quando
/plan-gym          → programa de ginásio estruturado (tipos A/B/C)
/setup-nutrition   → perfil nutricional e preferências
/plan-week         → planear a primeira semana
```

Depois: vai surfar → `/log-session` → volta ao `/coach`. Repete.

---

## Comandos disponíveis

| Comando | Para que serve |
|---|---|
| `/coach` | **Começa aqui.** Lê tudo e faz coaching contigo com base nos teus dados reais |
| `/log-session` | Registar uma sessão de surf — logo a seguir a surfar |
| `/plan-week` | Planear a semana completa: forecast, surf, ginásio, refeições, lista de compras |
| `/consult [tema]` | Consulta multidisciplinar em profundidade sobre um tema específico (recuperação, técnica, saúde mental, hábitos, periodização) — 3 a 4 especialistas em sequência, cada um a ler o que o anterior escreveu |
| `/spiritual` | Conversa directa com o guia espiritual — presença, a relação com o oceano, o que o surf significa |
| `/setup-profile` | Configurar ou actualizar o perfil de surfista |
| `/setup-goals` | Definir ou actualizar objectivos |
| `/setup-metrics` | Registar métricas de saúde e performance |
| `/setup-activities` | Registar actividades de treino disponíveis e disponibilidade |
| `/plan-gym` | Criar programa de ginásio estruturado (força, funcional, recuperação activa) |
| `/setup-nutrition` | Configurar perfil nutricional e preferências |
| `/evolve` | Auditar e melhorar o próprio sistema de coaching — corre a cada 4–8 semanas |
| `/reset` | Apagar dados do atleta (para recomeçar ou passar a outro utilizador) |

---

## Os especialistas

O `/coach` orquestra uma equipa de 14 especialistas que trabalham em background:

| Especialista | Domínio |
|---|---|
| Psicólogo | Performance mental, stress, motivação, equilíbrio vida-surf |
| Coach de mobilidade | Postura, qualidade de movimento, yoga, bloqueadores técnicos |
| Nutricionista | Nutrição desportiva, composição corporal, recuperação |
| Coach de ginásio | Força e condicionamento, carga de treino, periodização |
| Coach de técnica de surf | Análise técnica, mecânica de manobras, progressão |
| Coach de respiração | Respiração funcional, tolerância a CO2, preparação para hold-downs |
| Especialista em sono | Ciência do sono, cronobiologia, recuperação noturna |
| Fisioterapeuta | Prevenção de lesões, prehab, carga músculo-esquelética |
| Coach de periodização | Arco de treino a longo prazo, mesociclos, janelas de swell |
| Life coach | Formação de hábitos, rotinas diárias, mudança comportamental |
| Health coach | Biohacking, suplementação, longevidade, HRV, inflamação sistémica |
| Médico de medicina chinesa | Padrões TCM, equilíbrio energético, ritmos sazonais |
| Médico psicossomático | Padrões mente-corpo, expressão somática do stress |
| Guia espiritual | Presença, prática contemplativa, relação com o oceano |

Os especialistas lêem os relatórios uns dos outros antes de escreverem os seus — o fisioterapeuta sabe o que o coach de ginásio prescreveu, o health coach sabe o que o especialista em sono identificou. O coach de surf faz a síntese final.

---

## O plano semanal em HTML

O `/plan-week` gera automaticamente uma página HTML do plano da semana em `public/plans/`. Inclui forecast, sessões de surf, treinos, refeições e lista de compras — optimizada para usar no telemóvel antes de uma sessão, no ginásio, ou no supermercado.

O sistema melhora-se a si próprio a cada semana: depois de gerar o plano, um agente de revisão lê a página, identifica problemas de usabilidade e actualiza a especificação de design para a semana seguinte.

---

## Os teus dados

Tudo o que é teu fica na pasta `private/` no teu computador. Não é enviado para lado nenhum, não é partilhado, não aparece no git. O sistema de coaching (skills, agentes, configuração) é partilhável — os teus dados não são.

```
private/
  data/
    sessions/          → um ficheiro por sessão de surf
    goals/             → objectivos activos
    profile/           → perfil de surfista
    metrics/           → snapshots de saúde e performance
    plans/             → planos semanais em markdown e HTML
    specialist-reports/→ relatórios dos especialistas por sessão
    activities.md      → actividades e disponibilidade
    gym-programme.md   → programa de ginásio
    nutrition-profile.md → perfil nutricional
```

---

## Como tirar partido ao máximo

1. **Regista sessões a seguir a surfar.** Enquanto é fresco. Com honestidade — o que não correu bem importa tanto como o que correu.
2. **Faz o setup com atenção.** Os primeiros passos podem parecer lentos. Não são. Cada campo que preenchas torna cada sessão futura mais precisa.
3. **Volta regularmente.** O valor acumula com o tempo. Três meses de dados são qualitativamente diferentes de três semanas.
4. **Traz perguntas reais.** Física, mental, técnica, vida — o sistema está preparado para complexidade.
5. **Usa `/consult` quando algo é persistente.** Se há um padrão que não resolve, uma lesão recorrente, ou um bloqueio mental — o modo de consulta aprofunda onde o `/coach` generaliza.

---

## A filosofia

O melhor coaching não é o mais entusiasta. É o mais preciso. Um coach que te conhece — os teus padrões, as tuas evasões, a tua capacidade real versus a que declaras — pode dizer menos e significar mais.

É isso que este sistema está desenhado para ser.
