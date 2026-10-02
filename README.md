# 🔥 Doom Fire

<div align="center">
  <img src="https://img.shields.io/badge/JavaScript-puro-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript puro">
  <img src="https://img.shields.io/badge/HTML5-Table-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5 Table">
  <img src="https://img.shields.io/badge/CSS-3-1572B6?style=for-the-badge&logo=css&logoColor=white" alt="CSS 3">
  <img src="https://img.shields.io/badge/Licen%C3%A7a-MIT-yellow?style=for-the-badge" alt="Licença MIT">
</div>

<br>

> 🎯 **Recriação do efeito de fogo do DOOM (PlayStation, 1995) em JavaScript puro**. Sem biblioteca, sem build, sem dependência: é só abrir o `index.html` no navegador.

Fiz esse projeto como exercício para aprender JavaScript, seguindo o tutorial do [Filipe Deschamps](https://github.com/filipedeschamps) sobre o [fogo do DOOM](https://youtu.be/fxm8cadCqbs). Os vídeos dele ensinam muito além da linguagem, ensinam a pensar como programador. Recomendo para qualquer pessoa que esteja começando.

<p align="center">
    <img alt="Doom-Fire" src="demo/Fire-Doom.gif" width="500px" />
</p>

## 📋 Índice

- [🎓 O que aprendi](#-o-que-aprendi)
- [🚀 Como rodar](#-como-rodar)
- [🧠 Decisões técnicas](#-decisões-técnicas)
- [📄 Licença](#-licença)

## 🎓 O que aprendi

- **Uma imagem é um array de números.** O fogo é uma grade de 120x60 guardada num array de uma dimensão só, o `firePixelsArray`. Cada posição tem uma intensidade de 0 a 36, que vira cor numa paleta de 37 tons, do quase preto ao branco.
- **Um efeito convincente sai de uma regra simples repetida.** A última linha fica sempre em 36, a brasa. A cada 50 ms, cada pixel copia a intensidade do pixel de baixo menos um valor aleatório, e a chama esfria linha após linha até sumir.
- **Parâmetros separados se calibram sem estragar um ao outro.** O `decay` controla a altura da chama, e o `wind`, que grava o valor algumas colunas à esquerda, controla o balanço. Por serem dois valores, dá para mexer em um sem desfazer o outro.
- **Ver os dados por trás da imagem ajuda a entender o algoritmo.** Com `debug = true` dentro do `fireRender()`, as cores dão lugar ao índice e à intensidade de cada pixel, e dá para acompanhar a propagação acontecendo.
- **Desenhar na tela tem custo.** O render remonta a tabela HTML inteira a cada quadro, via `innerHTML`. Nas 7.200 células atuais roda liso, mas em 240x120 já engasga.

## 🚀 Como rodar

Abra o `index.html` no navegador. Tudo o que muda o resultado está em poucas variáveis:

| Onde | Variável | Valor | O que controla |
|---|---|---|---|
| `fogo.js` | `fireWidth` / `fireHeight` | 120 / 60 | Tamanho da grade |
| `fogo.js` | `decay` | `random() * 2.5` | Altura da chama: menor sobe mais |
| `fogo.js` | `wind` | `random() * 2.5` | Balanço lateral: maior verga mais |
| `fogo.js` | `setInterval` | 50 | Milissegundos entre quadros |
| `style.css` | `.pixel` | 8px | Tamanho de cada pixel na tela |

A altura da chama é fixa em número de linhas, não em porcentagem da tela: dobrar o `fireHeight` sem mexer no `decay` faz o fogo parecer mais baixo.

## 🧠 Decisões técnicas

| Decisão | Alternativa | Por quê |
|---|---|---|
| Array de uma dimensão | Matriz de linhas e colunas | Um índice só por pixel; a posição de cima e a de baixo são contas simples |
| `decay` e `wind` separados | Um único valor aleatório | Cada um controla um aspecto da chama |
| `<table>` com uma `<td>` por pixel | `<canvas>` | Cada célula pode mostrar o índice e a intensidade no modo debug; o custo é o desempenho, e o `<canvas>` é o caminho para grades maiores |

## 📄 Licença

[MIT](LICENSE)

---

<div align="center">
  <p>Desenvolvido por <strong>Luiz Matos</strong></p>
  <p>
    <a href="https://github.com/luiz-matos">GitHub</a> •
    <a href="https://www.linkedin.com/in/luizeduardomatos/">LinkedIn</a>
  </p>
</div>
