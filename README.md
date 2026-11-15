# rastreio-adaptativo.github.io

> **Protótipo de pesquisa.** Regras provisórias, calculadas sobre uma amostra parcial. Não usar com o público nem em decisões clínicas.

Página web que aplica as 15 perguntas do GAD-7 e do PHQ-8 uma por vez e encerra o rastreio assim que as respostas já indicam, com a confiança escolhida, o resultado que o questionário completo daria.

Faz parte de uma tese de doutorado em psicologia sobre rastreio conjunto de ansiedade e depressão com número adaptativo de perguntas e erro controlado.

## O que a página faz

- **Uma pergunta por vez.** Usa a redação oficial em português do Brasil do GAD-7 e dos itens 1 a 8 do PHQ-9.
- **Encerramento adaptativo.** A cada resposta, estima a chance de a pessoa terminar em cada um de quatro grupos e encerra quando a confiança atinge o nível escolhido:
  - nenhuma escala acima do ponto de corte;
  - só ansiedade (GAD-7 ≥ 10);
  - só depressão (PHQ-8 ≥ 10);
  - ambas.
- **Resultado.** Mostra o grupo, quantas perguntas foram respondidas e a confiança estimada. A pessoa pode responder o restante para ver os escores completos.
- **Modo profissional.** Permite escolher o nível de erro aceito e mostra o desempenho de cada nível.
- **Privacidade.** Tudo roda no navegador. Nenhuma resposta é enviada ou armazenada.

## Desempenho do protótipo

Medido em 1.277 respostas de teste que não participaram do cálculo das regras. O padrão de referência é a classificação do questionário completo, não um diagnóstico clínico.

| Nível | Perguntas (média) | Erro total | Erro em "só ansiedade" | Erro em "só depressão" |
|---|---|---|---|---|
| Até 5% | 6,3 | 3,5% | 18,5% | 13,2% |
| Até 3% (padrão) | 7,3 | 2,2% | 9,3% | 10,9% |
| Rigoroso | 10,0 | 0,3% | 1,9% | 0,8% |
| Exato | 11,7 | 0% | 0% | 0% |
| Completo | 15 | 0% | 0% | 0% |

No nível de 3%:

| | Sensibilidade | Especificidade | VPP | VPN |
|---|---|---|---|---|
| Ansiedade | 99,9% | 98,3% | 99,0% | 99,8% |
| Depressão | 98,9% | 97,7% | 98,8% | 97,9% |

Os valores preditivos estão inflados pela alta proporção de casos na amostra (cerca de 65% por escala). Em populações com menos casos, eles serão menores.

## Como funciona

1. **Ordem das perguntas (fixa):** PHQ2, GAD3, PHQ4, GAD1, PHQ8, GAD7, GAD4, GAD6, GAD2, GAD5, PHQ7, PHQ5, PHQ6, PHQ3, PHQ1.
2. **Estimativa.** Após cada resposta, as somas parciais de cada escala entram numa tabela de probabilidades, calculada por regressão logística multinomial. Grupos que já se tornaram impossíveis pela pontuação recebem probabilidade zero.
3. **Encerramento.** O rastreio para quando a maior probabilidade atinge o limiar do nível escolhido. O limiar foi calibrado em dados separados, como o menor valor cujo limite superior de 90% para o erro ficou abaixo do alvo.
4. **Regras embutidas.** A tabela de regras e os limiares estão dentro do `index.html` (constante `RULES`), em forma agregada. O arquivo não contém respostas individuais.

## Dados

- **Origem:** amostra de 5.107 respostas de adultos brasileiros, recrutados por rede social em 2024 e 2025.
- **Divisão:** 2.553 respostas para estimar a tabela, 1.277 para calibrar o encerramento e 1.277 para medir o erro.
- **Perfil da amostra:** majoritariamente feminina, escolarizada e com sintomas elevados. Em outros públicos o erro pode ser diferente.
- **Disponibilidade:** os dados não estão neste repositório.

## Limites

- Regras provisórias, a substituir pelas calculadas no banco completo.
- O erro total fica dentro do nível escolhido, mas é maior em quem tem só ansiedade ou só depressão.
- Ordem fixa das perguntas; a ordem aleatória está em estudo.
- Validação feita apenas por simulação sobre respostas já coletadas, sem teste com usuários.
- Reproduz a classificação do questionário e não é diagnóstico.
- O item 9 do PHQ-9 (pensamentos de se ferir) não é perguntado. A página não substitui avaliação de risco.

## Como usar

- **No navegador:** baixe o `index.html` e abra com dois cliques. Funciona sem internet; só a fonte do título muda.
- **Pelo GitHub Pages:** em *Settings → Pages*, escolha publicar a partir da branch `main`, pasta raiz.

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `index.html` | A página completa: interface, regras e motor de decisão |
| `README.md` | Este documento |

## Se precisar de ajuda

Se você está em sofrimento intenso ou pensando em se ferir, ligue 188 (CVV, 24 horas) ou procure um serviço de emergência.

## Créditos

- **Autoria:** [Nome do autor], doutorando em Psicologia, [Programa e instituição].
- **Orientação:** [Nome do orientador].
- **Instrumentos:** GAD-7 e PHQ-9 foram desenvolvidos pelos Drs. Robert L. Spitzer, Janet B.W. Williams, Kurt Kroenke e colegas, com um subsídio educacional da Pfizer Inc. Não é necessária permissão para reproduzir, traduzir, exibir ou distribuir.

## Licença

[Escolher a licença do código. Sugestão: MIT.]

## Como citar

[Autor]. (2026). *Rastreio Adaptativo GAD-7 + PHQ-8* (versão protótipo) [Software]. [Endereço do repositório]
