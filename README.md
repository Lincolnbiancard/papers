# Papers para o dono

Blog estático com papers sobre IA nas empresas, traduzidos para o português, para donos de PME. O site é gerado com [Hugo](https://gohugo.io/) e publicado no GitHub Pages.

Endereço: https://lincolnbiancard.github.io/papers/

O visual segue o padrão de leitura longa do [Lil'Log](https://lilianweng.github.io/posts/2023-06-23-agent/): título, data, tempo de leitura, autor, sumário recolhível no topo, figuras com legenda, citações em destaque, notas e referências no fim, modo claro e escuro, e coluna estreita no celular. O tema fica neste repositório (`layouts/`, `assets/css/`), para o sumário permanecer no topo do post.

## Ver no computador

É preciso o Hugo extended 0.170.1, a mesma versão do workflow.

```bash
hugo server
```

Abra http://localhost:1313/papers/

## Publicar

Cada push na branch `main` dispara `.github/workflows/pages.yml`. O job de build gera o site com Hugo. O job de deploy envia o resultado ao GitHub Pages com `actions/deploy-pages`.

Na primeira vez, ative o Pages à mão:

1. No repositório, abra Settings, depois Pages.
2. Em Build and deployment, escolha Source: GitHub Actions.

O workflow não muda essa configuração. Sem esse passo, o deploy falha e o site não entra no ar. Depois de ativar, rode de novo o workflow em Actions, se o push da `main` já tiver falhado.

Pull requests só rodam o build. O deploy acontece no push da `main`.

## Como adicionar um paper

Cada post é uma pasta em `content/posts/`.

1. Crie a pasta com a data e o slug. Exemplo: `content/posts/2026-11-26-nome-do-paper/`.
2. Escreva o texto em `index.md`, com o front matter abaixo.
3. Coloque as figuras na mesma pasta (`fig1.png`, `fig2.png` e assim por diante). O HTML do post aponta para o arquivo pelo nome, sem subpasta.
4. Se houver PDF da tradução, coloque o arquivo na mesma pasta e use o nome no campo `pdf`. Não publique o PDF original do editor. No lugar dele, deixe o link oficial em `original_url`.
5. Rode `hugo server`. Leia o post numa largura perto de 390 px e confira o sumário, as figuras e os acentos.
6. Faça o commit e o push na `main`.

O comando abaixo cria o `index.md` a partir do modelo em `archetypes/posts.md`:

```bash
hugo new content posts/2026-11-26-nome-do-paper/index.md
```

O post novo nasce como rascunho (`draft: true`) e não entra no site até você apagar essa linha.

### Front matter

```yaml
---
title: "Título em português"
date: 2026-11-26
author: "Lincoln Biancardi"
summary: "Uma ou duas frases para a lista da página inicial."
description: "Frase curta para o resumo do link."
paper:
  original_title: "Title in the original language"
  original_url: "https://exemplo.com/paper"
  authors: "Nome e Nome"
  institution: "Instituição"
  published: "26/11/2026"
  kind: "Relatório técnico qualitativo, não revisado por pares"
  pdf: "nome-da-traducao.pdf"
---
```

Se o texto não tiver ficha, apague o bloco `paper`. O sumário é montado sozinho a partir dos títulos `h2` e `h3` (no Markdown, `##` e `###`).

Não reescreva a tradução ao colar o post. Títulos, falas, legendas e referências ficam como foram entregues. As referências permanecem no idioma original. Quando existir um bloco extra da BianCode, ele fica no fim e marcado como extra.

### Figuras

Na mesma pasta do `index.md`:

```html
<figure class="fig">
  <img src="fig1.png" alt="Figura 1: descrição curta.">
  <figcaption><b>Figura 1: título.</b> Legenda completa.</figcaption>
</figure>
```

O atalho do tema faz o mesmo. A legenda aceita Markdown.

~~~
{{< figure src="fig1.png" alt="Figura 1: descrição curta." caption="**Figura 1: título.** Legenda completa." >}}
~~~

### Vídeo do YouTube

O `id` é o código da URL `https://www.youtube.com/watch?v=ID_DO_VIDEO`. O vídeo entra em 16:9 e ocupa a largura do texto, inclusive no celular.

~~~
{{< youtube id="ID_DO_VIDEO" title="Título do vídeo" >}}
~~~

Também vale a forma curta, só com o código:

~~~
{{< youtube ID_DO_VIDEO >}}
~~~

### PDF

Coloque o PDF da tradução na pasta do post e use o nome no campo `pdf`. O link "Baixar o PDF desta tradução" aparece na ficha, no topo do post.

## Licenças das fontes

Source Serif 4 e Source Sans 3 estão em `static/fonts/`, sob a SIL Open Font License. Os textos das licenças estão na mesma pasta.
