## Olá!, Sou o Pedro Henrique e Bem vindo(a) ao meu Github!👋

💻Bem-vindo(a) ao meu espaço no GitHub🌟🌟! Por aqui, você vai encontrar um pouco da minha jornada no mundo da tecnologia. Sou um desenvolvedor apaixonado por transformar ideias em código.

🎓Minha jornada é marcada pela curiosidade em construir e otimizar soluções. No Back-end, tenho experiência com Java, Spring e Spring Security, focando em sistemas robustos e seguros.

🎓Para o Front-end, mergulho em JavaScript, TypeScript, HTML e CSS, criando interfaces dinâmicas e amigáveis. Tenho um forte interesse em Banco de Dados, com experiência prática em MySQL, e também me aventuro no universo da linguagem C para entender a fundo os fundamentos.

🌄Quando não estou imerso em linhas de código, minhas paixões se voltam para o mundo dos jogos eletrônicos 🎮, que me inspiram na lógica e resolução de problemas. Além disso, dedico tempo a esportes ⚽, mantendo o corpo e a mente em equilíbrio. Estou sempre em busca de novos aprendizados e aberto a colaborações!


![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=phccoelho&show_icons=true&theme=tokyonight,discussions_started,discussions_answered,prs_merged,prs_merged_percentage)


##

name: GitHub Snake Game

on:
  # Schedule the workflow to run daily at midnight UTC
  schedule:
    - cron: "0 0 * * *"
  # Allow manual triggering of the workflow
  workflow_dispatch:
  # Trigger the workflow on pushes to the main branch
  push:
    branches:
      - main
jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      # Step 1: Checkout the repository
      - name: Checkout Repository
        uses: actions/checkout@v3
      # Step 2: Generate the snake animations
      - name: Generate GitHub Contributions Snake Animations
        uses: Platane/snk@v3
        with:
          # GitHub username to generate the animation for
          github_user_name: ${{ github.repository_owner }}
          # Define the output files and their configurations
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      # Step 3: Deploy the generated files to the 'output' branch
      - name: Deploy to Output Branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
          # Optionally, you can set a custom commit message
          commit_message: "Update snake animation [skip ci]"
