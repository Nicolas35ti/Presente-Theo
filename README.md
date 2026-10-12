# Cinnamoroll Site (Vue 3 + Vite)

## Rodar
    npm install
    npm run dev      # desenvolvimento
    npm run build    # gera a pasta dist/ para publicar

## Onde mexer
- src/data/profile.js     -> textos, listas e caminhos das imagens
- src/styles/variables.css -> cores e fontes
- public/images/          -> suas imagens: foto.png, cinna-doodle.png (doodle do topo da folha), cinna-corner.png

## Estrutura
    src/
      main.js            ponto de entrada
      App.vue            raiz
      views/             páginas
      components/        NotebookPage, NoteSection, PhotoCard, CornerDecor
      data/              conteúdo
      styles/            variáveis e estilos globais
      assets/            clouds.svg
