# Notas de Revisão — *A Realidade Como É* (Ajahn Sumedho)

Documento de apoio à revisão linguística da tradução (português europeu) dos
capítulos em `manuscript/tex/`. Resume o trabalho já feito e o que fica pendente,
para que uma próxima ronda de revisão possa retomar a partir daqui.

- **Data desta ronda:** 2 de junho de 2026
- **Âmbito:** todos os 30 ficheiros de capítulo em `manuscript/tex/` (de
  `00-01-sobre-o-autor.tex` a `26-como-as-coisas-sao.tex`), mais o glossário.
- **Método:** as observações foram inseridas como comentários LaTeX, no formato
  `% REVISÃO: ...`, **imediatamente acima do parágrafo a que dizem respeito**.
  Não afetam a compilação. Foram adicionadas **128 notas** no total.
- **Critério:** corrigir *erros* (gralhas, pontuação, gramática, regência,
  concordância) e *inconsistências de terminologia/grafia*. Não foram feitas
  alterações estilísticas, por o manuscrito já ter passado por edição.

> **Importante:** as notas **assinalam** os problemas; salvo raras exceções, **não
> alteram o texto**. A correção propriamente dita fica para uma fase seguinte,
> depois de decididas as convenções globais (ver secção 1).

---

## 1. Decisões editoriais globais a tomar (prioritárias)

Estas questões são transversais ao livro e devem ser **decididas primeiro** e
depois aplicadas numa passagem global (idealmente com `grep`/substituição
controlada), pois condicionam centenas de ocorrências.

### 1.1. Grafia: Acordo Ortográfico de 1990 (AO90) vs grafia anterior
O livro está dividido:
- **Capítulos 00–19:** grafia pré-AO90 (*actual, objecto, directo, percepção,
  acção, actividade, correcto, exacto, afecta, protecção*).
- **Capítulos 20–26 (e cap. 26-01):** grafia AO90 (*atual, objeto, direto,
  perceção, ação, atividade, correto, exato, afeta, proteção*).
- **Fugas isoladas de AO90 nos capítulos pré-AO90:** `atualizada` (00‑01),
  `objeto` (00‑02), `objeto`/`objetos`/`objetiva` (vários), `Correta` (19),
  `contractos` (10 — neste caso é antes hipercorreção: a forma correta é
  *contratos*).

**Ação sugerida:** escolher **uma** norma para todo o livro (a maioria do texto
está em pré-AO90) e uniformizar. Verificações úteis:
```
grep -rEno "direct[oa]s?|diret[oa]s?" *.tex
grep -rEno "percep|perce[çc]" *.tex
grep -rEno "ac[çc][ãa]o|a[çc][ãa]o" *.tex
grep -rEno "objec?t" *.tex
grep -rEno "correc?t[oa]" *.tex
```

### 1.2. «Buddha» vs «Buda»
- `Buddha`: 76 ocorrências. `Buda`: 45 ocorrências.
- Mistura inclusivamente dentro do mesmo capítulo/parágrafo (ex.: cap. 18 usa
  «Buda» e «Buddha-rūpa» lado a lado; cap. 25 usa ambos).
- **Recomendação:** uniformizar para **`Buddha`** (forma dominante, alinhada com
  o Pali e com o título/glossário). `grep -rnoP "\bBuda\b" *.tex`

### 1.3. Termo para `paṭiccasamuppāda`
Três traduções em uso:
- **«Geração Dependente»** — Introdução (00‑02).
- **«Génese Dependente»** — títulos dos capítulos 19–23.
- **«Originação Dependente»** — corpo dos capítulos 19 (nota de rodapé) e 20.

**Recomendação:** escolher **um** termo e aplicá-lo em títulos, corpo e notas.
(Os títulos dos capítulos dedicados usam «Génese Dependente».)

### 1.4. Diacríticos nos termos Pali (mácrons)

- **«anattā»** (adjetivo) é utilizado entre aspas (por exemplo, **«sabbe dhammā
  anattā»**), mas **«anatta»** (forma de raiz) é utilizado na prosa.

### 1.5. Aspas
- **Capítulos 00–16:** `` ``...'' `` (aspas curvas TeX duplas).
- **Capítulos 17–26:** `«...»` (aspas angulares/guillemets).
- **Mistura interna:** caps. 17, 22, 23, 25 usam simultaneamente `` ``...'' ``,
  `«...»` e `` `...' ``.
- **Recomendação:** escolher **um** estilo de aspas para todo o livro.
  `grep -rln "«" *.tex` lista os ficheiros com guillemets.

### 1.6. Itálico dos termos Pali
Inconsistente: por vezes `\emph{anatta}`, por vezes `anatta` sem itálico (ex.:
cap. 13 «arahant» com e sem `\emph`; cap. 26 termos sem itálico). Definir regra
(ex.: termos Pali sempre em itálico, exceto nomes próprios/estabelecidos).

### 1.7. Forma de tratamento
Os capítulos mais tardios (sobretudo 19, 22, 23, 24, 25, 26) alternam entre
**«tu»**, **«você»** e **«vós»**, por vezes no mesmo parágrafo. Decidir a forma
de tratamento e uniformizar.

### 1.8. Gentílicos e nomes de línguas
Em português escrevem-se com **minúscula**. Surgem com maiúscula: `Laosiano`
(08), `Tailandês` (14), `Italiano, Dinamarquês, Suíço, Inglês, Americano` (03).

### 1.9. «cerimónia» vs «cerimônia»
No cap. 14 o corpo usa `cerimónia` (PT-PT) e a nota de rodapé usa `cerimônia`
(circunflexo, PT-BR). Verificar circunflexos brasileiros noutros pontos.

---

## 2. Padrões recorrentes de erro (a vigiar em qualquer ronda futura)

1. **Vírgula entre sujeito e verbo** — ex.: «O nosso desejo (…) de deleite,
   leva-nos»; «Pessoas que viveram vidas muito egoístas, têm de beber»; «O
   potencial espiritual de cada ser, deve ser».
2. **Colocação pronominal do PT-BR** (próclise sem fator atrativo; gerúndio) —
   ex.: «querendo nos livrar» → «querendo livrar-nos»; «decidir nos pautarmos»;
   «não devíamos nos preocupar»; «está vindo» → «está a vir».
3. **Pronome clítico duplicado** — ex.: «se tornar-se», «nos elevar-nos»,
   «sentir-se feliz» depois de «se pode».
4. **Regência verbal** — «gostar» rege *de* («coisas de que não gostava»);
   «aperceber-se» rege *de* («apercebo-me de que»); «precisar» rege *de*
   («precise de sentir»); «inerente» rege *a* («inerente a essas»); crase em
   «abandonar-se àquilo».
5. **«dever» + infinitivo:** obrigação escreve-se sem *de* («não devia ser»),
   não «não devia de ser».
6. **Artigo definido antes de possessivo** (PT-PT) — «a sua própria respiração»,
   «as nossas vidas», «com os nossos sonhos».
7. **Contração `em`+artigo** — «num movimento», não «em um movimento».
8. **«todo» + substantivo** — PT-PT usa artigo: «todo o sofrimento», «toda a
   experiência».
9. **Interrogativas** — «Porque é que…?» (PT-PT) em vez de «Por que…?» (PT-BR).
10. **Marcas de oralidade** (só no cap. 26, transcrição) — «uh», repetições
    («nós, nós pensamos»), frases corridas.

---

## 3. Estado por ficheiro (nº de notas + itens não-sistémicos relevantes)

> Itens não-sistémicos = gralhas/erros pontuais que precisam de correção direta,
> para além das questões globais da secção 1.

- **00-01-sobre-o-autor.tex (1):** `atualizada` → `actualizada`.
- **00-02-introducao.tex (10):** «anatta»→«anattā»; «Geração» vs «Génese»; aspas
  `` `Geração Dependente' `` (estilo) + vírgula sujeito/verbo; «Isto trata-se
  de» (incorreto); vírgula→ponto e vírgula na enumeração; «lamento»/«lamentação»
  divergentes nos dois quotes da fórmula; «formações-karmicas» (hífen + grafia);
  vírgula sujeito/verbo; «objeto»→«objecto».
- **00-03-felicidade-para-sempre.tex (1):** «querendo nos livrar» → «livrar-nos».
- **01-investigando-a-mente.tex (9):** `annica`→`anicca` (gralha); 2× vírgula
  sujeito/verbo; «onde quando como ignorantes» (truncado); concordância de tempos
  («experimentará… cheirar… pense»); «experiência»→«experiencia» (verbo, 2×);
  «preconceitos e preconceitos» (repetição); «inerente nessas»→«a essas»;
  «Por que… comigo» (PT-BR).
- **02-tudo-o-que-surge-acaba.tex (5):** «Buda»→«Buddha»; «todo sofrimento»→«todo
  o sofrimento» (2×); «anatta»→«anattā»; «a razão porque»→«por que»; «esses
  tempos são passado» (concordância/expressão).
- **03-os-cinco-khandhas.tex (9):** «em um movimento»→«num»; «sua própria
  respiração»→«a sua»; falta «?» em frase interrogativa; `(\emph{saññā)}`
  (chaveta mal colocada); quebra de parágrafo indevida entre «quer» e «nos
  consideremos»; `seriamos`→`seríamos`; gentílicos com maiúscula;
  «anatta»→«anattā»; falta «aniccā» na fórmula «sabbe saṅkhārā…».
- **04-todo-o-tempo-no-mundo.tex (1):** vírgula sujeito/verbo («querer
  livrar-me da dor, era»).
- **05-preceitos.tex (6):** «sila»→«sīla»; vírgula sujeito/verbo; «nos
  elevar-nos»→«elevarmos»; «coisas que não gostava»→«de que»; «abandonar-se
  aquilo»→«àquilo» (+ vírgula); «se tornar-se algo» (clítico duplicado).
- **06-a-realidade-como-e.tex (4):** «não devia de ser»→«não devia ser»;
  `enfâse`→`ênfase`; «decidir nos pautarmos»→«pautar-nos»; «de sua postura»→«da
  sua».
- **07-a-jangada.tex (2):** «me apercebo que»→«de que»; inciso «na verdade» sem
  vírgulas a ladear.
- **08-a-paciencia.tex (3):** `Laosiano` (maiúscula, 2×); «Ele falar podia»→«Ele
  podia falar»; «para realmente para» (repetição de «para»).
- **09-reflexoes-sobre-a-comida.tex (0):** sem notas (texto limpo).
- **10-aceitando-as-coisas-como-sao.tex (3):** «se tornar-se aquilo» (clítico
  duplicado); «com nossos sonhos»→«com os nossos»; `contractos`→`contratos`.
- **11-consciencia-e-sensibilidade.tex (3):** «controlar nossas vidas»→«as
  nossas»; onomatopeia `glup`/`gulp` divergente; «toda experiência»→«toda a
  experiência».
- **12-o-som-do-silencio.tex (2):** «formações cármicas» (+ `saṅkhāras` vs
  `saṅkhārā`); pontuação/frase corrida em «oferece às condições como a raiva,
  uma saída…, deixamos…».
- **13-uma-inspiracao-apenas.tex (4):** «Por é que»→«Porque é que»;
  `canadense`→`canadiano`; mudança de pessoa na citação («Tive…»/«pensaste que
  eras») + `arahant` sem itálico; `caia`→`caía`.
- **14-quietude-e-resposta.tex (4):** «Pode se ser»→«Pode-se ser»;
  `Tailandês`→`tailandês`; nota de rodapé `cerimônia`→`cerimónia`;
  `Nibbana`→`Nibbāna`.
- **15-virando-em-direccao-ao-vazio.tex (4):** «adversos a isso»→«avessos»;
  «não devíamos nos preocupar»→«preocupar-nos»; «nada em que pensamento for»
  (truncado); «querer nos livrar»→«livrar-nos».
- **16-para-alem-da-crenca.tex (3):** «nas extremas de Amaravati»→«nas
  extremidades»; «conseguem duvidar» (provável erro de tradução — contexto é
  *sentir/ter consciência*); «anatta»→«anattā».
- **17-ser-ninguem.tex (7):** mistura de aspas (`` ``…'' ``/«…»/`` `…' ``);
  mistura tu/vocês; «ninguém raramente» (dupla negação); `Luan Por`→`Luang Por`;
  «que os fiéis apressariam-se para ver» (próclise + «apressar-se a»); «tempo
  tedo»→«todo»; «anatta»→«anattā».
- **18-nao-dualismo.tex (3):** «por que me abandonaste»→«porque»; «ao qual…por
  isso e ao qual…» (construção truncada/redundante); «Buda» vs «Buddha-rūpa».
- **18-01-dasadhamma-sutta.tex (2):** item 4 truncado/sem sentido («Surge na
  minha mente algum sabiamente pela minha conduta?» — falta o substantivo, p.
  ex. «censura»); «não precise sentir»→«precise de sentir».
- **19-genese-dependente-01.tex (7):** «no/o anatta»→«anattā» + terminologia
  «Génese/Originação/Geração»; «formações kármicas»→«kammicas»; **pontuação
  corrompida** (`tudo isto?;` / `;Será…`; `cósmico?;`); «estás… a sua mente»→«a
  tua»; «não é assim que de sair»→«que se sai»; «do Compreensão Correta»→«da
  Compreensão Correcta».
- **20-genese-dependente-02.tex (4):** nota global de ortografia AO90; «Génese»
  (título) vs «Originação» (corpo); `Nibbana`→`Nibbāna`; «Buda»→«Buddha».
- **21-genese-dependente-03.tex (3):** nota global ortografia AO90 +
  «kármica»→«kammica» + «Buda»→«Buddha»; aspas/frase corrompida em «Eu quero
  livrar-me do -- «Eu quero.»».
- **22-genese-dependente-04.tex (4):** nota global ortografia AO90; anglicismo
  «insight» (vs «compreensão lúcida»/«discernimento») + «Buda»→«Buddha»; mistura
  de aspas; «desejas-o»→«deseja-lo» (verbo terminado em -s).
- **23-genese-dependente-05.tex (4):** nota global ortografia AO90; mistura
  aspas + tratamento (você/tu/vós) + «Buda»→«Buddha»; «está vindo» (gerúndio
  PT-BR); aspa de abertura em falta («Olha para mim…»).
- **24-irradiacao-do-divino.tex (4):** nota global ortografia AO90; mistura
  tu/você; «anatta»→«anattā»; «a forma como uma forma como esta sobrevive»
  (repetição).
- **25-um-momento-para-amar.tex (5):** nota global ortografia AO90; mistura
  tu/você + «Buda»/«Buddha» + «anatta»→«anattā»; «Não se pode sentir-se feliz»
  (clítico duplicado); `anagairikas`→`anagārikas`.
- **26-01-benevolencia.tex (2):** concordância «Que todos permaneçam… Livre»→
  «Livres» (plural); ortografia AO90 («ações», «atos»).
- **26-como-as-coisas-sao.tex (9):** **transcrição de palestra (2021)** — nota
  global de ortografia AO90 + tratamento + «Buda»→«Buddha» + marcas de oralidade
  a limpar; «6\textsuperscript{de} março» (erro de marcação); «observares com
  um» (truncado); `dhukka`/`annata`→`dukkha`/`anattā`; `Amravati`→`Amaravati`;
  `anata`→`anattā`; «Luang Po»→«Luang Por».

---

## 4. Observações sobre marcadores `% FIXME` pré-existentes

O manuscrito já continha alguns comentários `% FIXME` do tradutor/editor que
**não foram resolvidos** nesta ronda (apenas registados aqui):
- `00-02-introducao.tex`: `% FIXME: domanassa missing` (na glosa da fórmula, o
  termo *domanassa* não está traduzido).
- `02-tudo-o-que-surge-acaba.tex`: `% FIXME ordenação => taking precepts`.
- `21-genese-dependente-03.tex`: `% FIXME: Verse reference is not 860` (dúvida
  sobre a referência do verso do Sutta-Nipāta citado em nota de rodapé).

---

## 5. Itens fora de âmbito / não tratados

- **Front matter** (`copyright.tex`, `copyright-details.tex`, `titlepage.tex`,
  `glossary.tex`): não são capítulos traduzidos; não foram anotados. Nota: o
  `copyright.tex` usa aspas curvas `‘ ’`, diferente do corpo do livro — verificar
  se é intencional.
- **Glossário** (`glossary.tex`): está em inglês (apenas duas entradas, *anicca*
  e *borapet*) e contém comentários de secção `=== A ===` etc. vazios. Avaliar se
  deve ser traduzido/preenchido para a edição portuguesa.
- **Coerência das traduções da fórmula de `paṭiccasamuppāda`** entre a Introdução
  e os capítulos 19–23 (termos como *soka/parideva/dukkha/domanassa/upāyāsa*):
  merece uma verificação dedicada para garantir a mesma tradução em todo o lado.

---

## 6. Como retomar

1. Decidir as convenções globais da **secção 1** (grafia, «Buddha», termo de
   *paṭiccasamuppāda*, mácrons, aspas, itálico, tratamento).
2. Aplicar essas decisões numa passagem global (com `grep` + substituição
   revista caso a caso — atenção a falsos positivos, sobretudo nas trocas de
   grafia AO90/pré-AO90).
3. Percorrer as notas `% REVISÃO:` ficheiro a ficheiro e aplicar as correções
   pontuais (secção 3), removendo cada nota depois de tratada.
4. Resolver os `% FIXME` pendentes (secção 4).
5. Reler em particular o **cap. 26** (transcrição) para limpeza de oralidade e os
   pontos de **pontuação corrompida** (caps. 19, 21, 23), que sugerem perda de
   caracteres `«»` numa conversão anterior.

Para localizar rapidamente todas as notas desta ronda:
```
grep -rn "% REVISÃO" manuscript/tex/*.tex
```
