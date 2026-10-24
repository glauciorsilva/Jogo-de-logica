# Labirinto das Contas

Jogo de lógica e matemática para o 3º ano do Ensino Fundamental. A criança anda por um labirinto até a bandeira e, no caminho, precisa resolver uma conta para abrir a porta trancada.

## Como jogar

1. Escreva seu nome (e a turma, se quiser) na tela de entrada.
2. Escolha uma trilha do labirinto ou o Desafio de Matemática.
3. No labirinto, toque no lugar para onde quer ir ou arraste o dedo pelo caminho (no computador, as setas do teclado também funcionam).
4. Na porta, escolha a resposta certa. Errou? Aparece uma dica.

## Conteúdo

| Nível | Trilha do labirinto (60 fases) | Desafio de Matemática (10 perguntas) |
|---|---|---|
| Iniciante | Soma e subtração até 10, sequências | Contas até 10, maior número, sequência |
| Intermediário | Contas até 50, tabuada do 2, 3 e 5, número que falta | Contas até 20, dobro, metade, tabuada do 2 e 3 |
| Avançado | Contas até 100, tabuada até 5, duas operações | Contas até 50, tabuada até 5, dezenas e unidades |
| Hard | Multiplicação com soma, parênteses, problemas | Contas até 100, tabuada até 10, repartir igualmente |

Cada trilha tem duas partes: as fases 1 a 30 e as fases 31 a 60, um pouco mais desafiadoras e com tipos novos de pergunta (número que falta, maior e menor, dobro e metade, dezenas e unidades, repartir igualmente, sequência que dobra). O labirinto também cresce ao longo da trilha.

Cada trilha tem um **Gabarito do professor** com os 60 exercícios e as respostas.

## Pontos e ranking

- Cada estrela do labirinto vale 10 pontos (3 estrelas sem erro, 2 com um erro, 1 com mais).
- No Desafio, cada acerto vale 10, 20, 30 ou 40 pontos, conforme o nível. Conta o melhor resultado de cada nível.
- O ranking é online, no Firebase (Firestore, projeto `jogologico-fc23d`): todos os aparelhos da turma veem o mesmo placar, ao vivo.
- Se o Firebase estiver fora do ar, o jogo continua funcionando e mostra o ranking salvo no próprio aparelho.
- Ao abrir o jogo, todos os jogadores já salvos naquele aparelho são enviados para o ranking online, juntando com o que já estiver lá (vale sempre o melhor resultado de cada fase e de cada Desafio).
- O ranking mostra **todos** os jogadores que já entraram, inclusive quem ainda está com 0 ponto, e aparece no topo da tela inicial com a posição de quem está jogando.

### Recomeçar do zero (nova temporada)

No código, a constante `SEASON` marca a temporada atual (hoje é a **2**). Quando um aparelho abre uma temporada nova, ele zera as fases, estrelas e recordes de todos os jogadores salvos nele, mas mantém os nomes. Para recomeçar de novo no futuro: aumente o número de `SEASON` e apague os documentos da coleção `ranking` no console do Firebase.

## Configurar o Firebase (uma vez só)

1. Abra o [console do Firebase](https://console.firebase.google.com/) → projeto **jogologico-fc23d** → **Firestore Database**.
2. Na aba **Regras**, apague o que estiver lá, cole o conteúdo do arquivo [`firestore.rules`](firestore.rules) e clique em **Publicar**.

O que a regra faz:

- Qualquer pessoa pode **ver** o ranking.
- Cada jogador pode **criar e atualizar** o próprio registro, só com dados válidos: nome de 2 a 24 letras, turma até 10, no máximo 720 estrelas e 1000 pontos de Desafio, e os pontos têm que bater com a conta (estrelas × 10 + Desafio).
- Ninguém **apaga** pelo jogo. Para zerar o ranking, apague os documentos da coleção `ranking` pelo console.
- Qualquer outra coleção fica bloqueada.

## Onde o jogo está publicado

O jogo está na **Vercel**: [joglog.vercel.app](https://joglog.vercel.app). O projeto `joglog` está ligado a este repositório, então cada commit na branch `main` é publicado sozinho em cerca de um minuto.
