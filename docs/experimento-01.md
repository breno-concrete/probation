# Experimento 01: a garantia ganha em inglês sobrevive em português?

> Escrito em 22/nov/2026, antes de qualquer execução. Fazer o commit antes de rodar o modelo.

## Pergunta

Um modelo aberto é aprovado em inglês para certos tipos de decisão, com garantia de acerto acima de 90%.
Se a empresa usar essa aprovação com clientes que falam português, **a garantia continua valendo?**

## Minha previsão (Breno preenche antes de rodar)

- Tipos aprovados em inglês, de 18:
- Desses, quantos continuam acima de 90% em português:
- Por quê:

## Dados

- [`mteb/amazon_massive_scenario`](https://huggingface.co/datasets/mteb/amazon_massive_scenario), derivado do MASSIVE (Amazon). Conferir a licença do original antes de publicar.
- 16.521 frases, 18 tipos (326 a 2.370 por tipo). As mesmas frases em inglês e em português, com o mesmo id e o mesmo gabarito.
- **Limite:** o português é o de Portugal. Não concluir sobre o do Brasil.

## Método

1. Modelo: `qwen2.5:7b` no Ollama, temperatura 0, um prompt fixo por idioma.
2. Divisão por hash do id, igual nos dois idiomas: 70% para aprovar, 30% para verificar.
3. Tipo de decisão = a resposta do modelo, porque em produção não existe gabarito na hora de decidir.
4. Uma carteira de fichas por tipo: começa em 1, acerto multiplica por 0,95/0,90, erro por 0,05/0,10.
5. São 18 tipos testados juntos, então promove com **20 × 18 = 360 fichas**, para manter 5% no total.
6. Verificar os tipos aprovados em inglês nos 30%, em inglês e em português.

## Métricas

- Cobertura: parte das decisões de verificação que cai num tipo aprovado.
- Acerto nos tipos aprovados, por idioma, com intervalo de 95%.
- Quantos certificados de inglês quebram em português.
- Segundos por decisão.

## Critério de 06/dez (não muda)

Continua se, em inglês, na verificação:

- cobertura de **pelo menos 20%**, e
- acerto de **pelo menos 90%** no conjunto aprovado.

O resultado em português não decide se o projeto vive: ele é a descoberta, seja qual for.

## Trabalhos próximos

- [BARGAIN](https://arxiv.org/abs/2509.02896): cascata barato/caro com garantia, em dataset fixo.
- [CELEUS](https://arxiv.org/abs/2606.20820): avaliação de LLM com e-process.
- [CRC por grupo](https://arxiv.org/abs/2607.24562): garantia global não vale por subgrupo e quebra entre datasets.
- [Regressão em troca de versão](https://arxiv.org/abs/2608.13607): média sobe e casos individuais pioram.
- [Understudy](https://github.com/Endgame-Labs/understudy): sombra, promoção, auditoria e rebaixamento.

Numa busca rápida em 22/nov, não apareceu este teste entre inglês e português. **Isso não prova ineditismo:** revisar a literatura antes de publicar.
