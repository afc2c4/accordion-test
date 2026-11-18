---
name: buscar-landing-pages-previdenciario
description: Pesquisa e analisa landing pages de advogados previdenciários voltadas a público com mais de 60 anos. Use quando o usuário pedir referências, benchmarks, análise ou exemplos de landing pages de advocacia previdenciária (aposentadoria, BPC/LOAS, pensão por morte, revisão de benefício, auxílio-doença/incapacidade) pensadas para pessoas idosas.
---

# Buscar landing pages de advogados previdenciários (público 60+)

## Objetivo

Encontrar, abrir e analisar landing pages reais de escritórios e advogados previdenciários cujo público é de pessoas com 60 anos ou mais, e devolver um relatório com exemplos, padrões de conteúdo e boas práticas de acessibilidade. A skill pesquisa e analisa; não copia textos nem imagens de terceiros.

## Entradas (perguntar só se faltar algo essencial)

- **Tema principal**: aposentadoria por idade, BPC/LOAS, pensão por morte, revisão da vida toda, auxílio-doença/incapacidade, outro. Se não informado, pesquisar os cinco primeiros.
- **Região**: cidade ou estado, se o usuário quiser foco local. Caso contrário, nacional.
- **Quantidade**: padrão de 10 landing pages.
- **Destino do relatório**: padrão é um arquivo Markdown em `/tmp/claude-0/-home-user-accordion-test/a25f77c3-7a4a-538b-beee-c0ef12466e91/scratchpad/` ou, se o usuário pedir, em `docs/` do repositório.

## Fluxo

1. **Montar consultas.** Combinar tema + "advogado previdenciário" + termos de landing page, por exemplo:
   - "advogado previdenciário aposentadoria landing page"
   - "advogado BPC LOAS idoso consulta gratuita"
   - "revisão da vida toda advogado aposentados"
   - "pensão por morte advogado escritório idosos"
   Rodar as consultas em paralelo com WebSearch, modo "standard". Usar "extended" só se o resultado vier fraco ou desatualizado.

2. **Filtrar candidatos.** Manter apenas páginas que:
   - sejam de advogado, escritório ou sociedade de advogados (não agregador, não portal de notícias, não fórum);
   - tenham foco em clientes idosos ou em benefícios que atendem esse público;
   - sejam landing pages (uma página com chamada para ação), não o blog inteiro.
   Descartar sites com sinais de captação ilícita ou promessas de resultado garantido, e anotar o motivo.

3. **Abrir e ler cada página.** Se as ferramentas do navegador embutido (`mcp__Claude_Browser__*` ou `mcp__remote-devices__Claude_Browser__*`) estiverem disponíveis, usar `preview_start` com a URL e `get_page_text` / `read_page` para ler o conteúdo real; `computer` com screenshot só se o layout visual for o ponto. Se não estiverem, usar WebFetch ou um subagente `web-fetch` com a URL. Se uma página recusar acesso, registrar e seguir em frente.

4. **Analisar cada página** com o checklist abaixo.

5. **Montar o relatório** no formato de saída abaixo e salvar no destino combinado.

## Checklist de análise

### Acessibilidade para público 60+
- Tamanho de fonte do corpo de texto (ideal: 18px ou mais) e títulos legíveis.
- Contraste entre texto e fundo (ideal: WCAG AA no mínimo, AAA desejável).
- Botões grandes, com texto descritivo ("Falar com a advogada pelo WhatsApp", não só "Clique aqui").
- Layout simples, uma ação principal por tela, pouca distração.
- Funciona bem em celular, com área de toque suficiente.
- Textos alternativos em imagens e rótulos em formulários.

### Linguagem e confiança
- Linguagem simples, sem jargão jurídico não explicado (ex.: "carência", "DIB", "salário de benefício" devem ter explicação).
- Explicação do benefício em passos curtos.
- Identificação clara do advogado: nome, OAB, especialidade.
- Ausência de promessas de resultado ou de "aposentadoria garantida".
- Presença de aviso de que o resultado depende da análise do caso.

### Conversão e contato
- Canal de contato evidente (telefone, WhatsApp), com horário de atendimento.
- Formulário curto (nome, telefone, benefício de interesse), sem exigir muitos dados de cara.
- Opção de ligação direta para quem não gosta de formulário.
- Consulta inicial gratuita, se houver, e como ela funciona.

### Conformidade com publicidade da advocacia (OAB)
- Verificar se há informações de publicidade permitidas: nome, OAB, áreas de atuação, contato.
- Anotar sinais de problema: promessa de resultado, comparação com outros advogados, captação de clientes por meios vedados, uso de depoimentos de clientes sem o devido cuidado, valores de honorários como chamariz.
- Não afirmar que uma página viola a regra sem indicar o trecho e a norma; tratar como "ponto de atenção".

## Formato de saída

Relatório em Markdown com:

1. **Resumo**: quantas páginas foram analisadas, tema(s) cobertos e os três padrões mais comuns.
2. **Tabela de páginas**: URL | escritório/advogado | tema | nota de acessibilidade (1 a 5) | nota de clareza (1 a 5) | pontos de atenção.
3. **Análise por página**: 3 a 5 frases, com pontos fortes e fracos.
4. **Boas práticas recorrentes**: lista curta de padrões que funcionam para 60+.
5. **Pontos de atenção de conformidade**: página e trecho, sem julgamento definitivo.
6. **Limitações**: páginas que não abriram, conteúdo carregado por JavaScript que não foi lido, data da pesquisa.

Não incluir dados pessoais de clientes nem prints de depoimentos. Sempre registrar a data da pesquisa.

## Regras

- Não copiar textos, imagens ou marcas de terceiros para o novo material; usar só para análise.
- Não entrar em áreas logadas nem preencher formulários de contato em sites de terceiros.
- Não fazer scraping em massa; abrir só as páginas necessárias para a análise.
- Se o usuário quiser criar uma landing page própria a partir disso, usar a análise como referência e escrever um conteúdo novo, observando as mesmas regras de publicidade da OAB.
