# Diário LKM

Site da ORG **Diário LKM** de Free Fire. O Diário é um battle royale pago, todo mundo contra todo mundo: **R$ 6 de entrada** e **R$ 4 por kill**. O objetivo do site é explicar como funciona e levar o jogador para o Discord (https://discord.gg/NhVkNQe33T).

## Como rodar

É um site estático, sem build. Na pasta do projeto:

```bash
python -m http.server 5500
```

Depois abra http://localhost:5500. Também dá para abrir o `index.html` direto com dois cliques, mas o contador do Discord pode não carregar fora de um servidor.

## Estrutura

```
DiarioLKM/
├── index.html      # página inteira: HTML, CSS e JS juntos
├── assets/
│   └── logo.jpg    # logo oficial (usada no topo, na abertura, no favicon e na prévia de links)
└── README.md
```

## O que o site tem

- **Fundo animado de fogo:** fagulhas e cinzas subindo em tela cheia (canvas). Elas fogem do mouse ou do dedo e são empurradas pela rolagem como vento.
- **Abertura:** logo grande, título "Diário LKM" em degradê de fogo igual às letras da logo, botões "Jogar o diário" e "Como funciona", e a dica "Role para baixo".
- **Quanto custa, quanto paga:** R$ 6 e R$ 4 em destaque, mais uma calculadora com barra de kills que mostra quanto o jogador recebe e o lucro depois da entrada.
- **Cartão do Discord:** nome, ícone, membros online e total do servidor, lidos do convite público do Discord. Se o Discord bloquear essa consulta, os números ficam escondidos e os botões continuam funcionando. Tem também o botão "Copiar convite".
- **Como jogar o diário:** 3 passos (entrar no Discord, pagar a entrada, jogar e receber).
- **Efeito de rolagem:** a logo e o texto da abertura se movem em ritmos diferentes (parallax) e as seções entram deslizando ao aparecer.

## Identidade visual

| Nome | Cor | Uso |
|---|---|---|
| carvão | `#140d0a` | fundo |
| brasa | `#ff4a14` | vermelho do fogo |
| chama | `#ff8c1f` | laranja, números dos passos |
| ouro | `#ffc94d` | destaques e valores |
| cinza | `#b3a398` | texto secundário |
| osso | `#fff0da` | texto principal |

Fontes: **Saira Condensed** itálico pesado nos títulos (inclinado como o "LKM" da logo) e **Saira** no texto, pelo Google Fonts.

## Desempenho (60 fps)

- As fagulhas usam brilhos pré-desenhados (16 tons, de ouro a brasa) carimbados com `drawImage`, em vez de `shadowBlur`, que era o que derrubava para 30 fps.
- O movimento usa tempo real entre quadros, então a velocidade é a mesma em telas de 60, 90 ou 120 Hz.
- Celular: no máximo 90 partículas e resolução do canvas limitada a 1.5x. PC: 190 partículas e 2x.
- Foram removidos: `mix-blend-mode` na logo, a animação de `filter` na logo e o `backdrop-filter` do cartão do Discord.
- Com "reduzir movimento" ativado no aparelho, o fogo fica parado e os efeitos de rolagem são desligados.

## Onde paramos

Última sessão: 30/09/2026.

**Feito**
- [x] Site completo com fundo de fogo, abertura, valores, calculadora, Discord e passos
- [x] Textos ajustados para o formato real do Diário (R$ 6 de entrada, R$ 4 por kill)
- [x] Otimização para 60 fps no PC e no celular
- [x] Efeito de rolagem (parallax e entrada das seções)
- [x] Servidor local em http://localhost:5500

**Falta confirmar**
- [ ] Os 60 fps na prática, no PC e no celular. Foi otimizado, mas ainda não foi medido.
- [ ] Se o contador de membros do Discord aparece de fato no navegador.
- [ ] **Forma de pagamento da entrada.** Hoje o texto diz "a staff confirma seu nome na lista e passa a sala". Se for por Pix, colocar a chave ou instrução no site.
- [ ] **Horários do Diário.** Se houver horário fixo, mostrar a próxima partida no site.
- [ ] Regras do Diário (por exemplo, o que conta como kill, o que acontece se cair da partida, quando o pagamento é feito).

**Próximos passos sugeridos**
- [ ] Publicar o site com link próprio de graça (Netlify ou Vercel).
- [ ] Ranking de quem mais fez kills ou mais ganhou (precisa de alguém da staff atualizando).
- [ ] Prints ou clipes de partidas do Diário.

## Observações

- O rodapé avisa que a LKM não tem vínculo com a Garena.
- Todo o código está em `index.html`. Para trocar valores, procure `ENTRADA` e `POR_KILL` no script e os textos "R$&nbsp;6" e "R$&nbsp;4" no HTML.
