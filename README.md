# Similaridade de Cosseno Aplicada à Acessibilidade Digital
---

## Contexto do Projeto

Desenvolvimento de uma solução inteligente para garantir acessibilidade digital nos conteúdos de treinamento do Itaú Unibanco. Utilizando vetorização textual e similaridade de cosseno para identificar frases que se distanciam das boas práticas de inclusão.

### Objetivo
Comparar frases reais (potencialmente problemáticas) com boas práticas de acessibilidade, identificando trechos que mais precisam de ajuste.

---

## Corpus de Análise

### Frases Problemáticas
- **F6:** "Esse vídeo não possui legenda nem intérprete de Libras."
- **F7:** "Usuários com deficiência visual não conseguem acessar o conteúdo."
- **F8:** "A plataforma não tem suporte para tradução em Libras ou descrição de imagem."

### Boas Práticas
- **BP5:** "Adicione legenda e intérprete de Libras para todos os vídeos."
- **BP6:** "Garanta descrição de imagens e leitura por leitores de tela."

---

## Etapa 1: Vocabulário Comum

**Total de palavras únicas:** 35 palavras

```
adicione    acessar     comentar    conseguem   conteudo
deficiencia descricao   e           esse        garanta
imagem      imagens     interprete  legenda     leitura
leitores    libras      nao         nem         o
ou          para        plataforma  por         possui
precisa     suporte     tela        tem         todos
traducao    usuarios    video       videos      visual
```

### Processo de Normalização:
1. Conversão para minúsculas
2. Remoção de acentos e caracteres especiais
3. Eliminação de duplicatas
4. Ordenação alfabética

---

## Etapa 2: Matriz de Vetorização (TF - Term Frequency)

| Frase/Palavra | adicione | acessar | comentar | conseguem | conteudo | deficiencia | descricao | e | esse | garanta | imagem | imagens | interprete | legenda | leitura | leitores | libras | nao | nem | o | ou | para | plataforma | por | possui | precisa | suporte | tela | tem | todos | traducao | usuarios | video | videos | visual |
|---------------|----------|---------|----------|-----------|----------|-------------|-----------|---|------|---------|--------|---------|------------|---------|---------|----------|--------|-----|-----|---|----|----- |------------|-----|--------|---------|---------|------|-----|-------|----------|----------|-------|--------|--------|
| **F6**        | 0        | 0       | 0        | 0         | 0        | 0           | 0         | 0 | 1    | 0       | 0      | 0       | 1          | 1       | 0       | 0        | 1      | 1   | 1   | 0 | 0  | 0    | 0          | 0   | 1      | 0       | 0       | 0    | 0   | 0     | 0        | 0        | 1     | 0      | 0      |
| **F7**        | 0        | 1       | 0        | 1         | 1        | 1           | 0         | 0 | 0    | 0       | 0      | 0       | 0          | 0       | 0       | 0        | 0      | 1   | 0   | 1 | 0  | 0    | 0          | 0   | 0      | 0       | 0       | 0    | 0   | 0     | 0        | 1        | 0     | 0      | 1      |
| **F8**        | 0        | 0       | 0        | 0         | 0        | 0           | 1         | 1 | 0    | 0       | 1      | 0       | 0          | 0       | 0       | 0        | 1      | 1   | 0   | 0 | 1  | 1    | 1          | 0   | 0      | 0       | 1       | 0    | 1   | 0     | 1        | 0        | 0     | 0      | 0      |
| **BP5**       | 1        | 0       | 0        | 0         | 0        | 0           | 0         | 1 | 0    | 0       | 0      | 0       | 1          | 1       | 0       | 0        | 1      | 0   | 0   | 0 | 0  | 1    | 0          | 0   | 0      | 0       | 0       | 0    | 0   | 1     | 0        | 0        | 0     | 1      | 0      |
| **BP6**       | 0        | 0       | 0        | 0         | 0        | 0           | 1         | 1 | 0    | 1       | 0      | 1       | 0          | 0       | 1       | 1        | 0      | 0   | 0   | 0 | 0  | 0    | 0          | 1   | 0      | 0       | 0       | 1    | 0   | 0     | 0        | 0        | 0     | 0      | 0      |

---

## Etapa 3: Fórmula da Similaridade de Cosseno

```
cos(θ) = (A · B) / (||A|| × ||B||)

Onde:
• A · B = produto escalar (soma dos produtos termo a termo)
• ||A|| = norma euclidiana do vetor A = √(∑ᵢ aᵢ²)
• ||B|| = norma euclidiana do vetor B = √(∑ᵢ bᵢ²)
```

**Interpretação dos Valores:**
- `cos(θ) = 1`: Vetores idênticos (máxima similaridade)
- `cos(θ) = 0`: Vetores ortogonais (sem similaridade)
- `cos(θ) = -1`: Vetores opostos (mínima similaridade)

---

## 📊 Etapa 4: Cálculos Detalhados das Similaridades

### Cálculo F6 × BP5
```
F6 = [0,0,0,0,0,0,0,0,1,0,0,0,1,1,0,0,1,1,1,0,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0]
BP5 = [1,0,0,0,0,0,0,1,0,0,0,0,1,1,0,0,1,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0,0,1,0]

Produto Escalar: 0×1 + 0×0 + ... + 1×1 + 1×1 + 1×1 + 1×0 + 1×1 = 3
||F6|| = √(5) = 2.236
||BP5|| = √(6) = 2.449
Similaridade = 3 / (2.236 × 2.449) = 0.548
```

### Cálculo F6 × BP6
```
F6 = [0,0,0,0,0,0,0,0,1,0,0,0,1,1,0,0,1,1,1,0,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0]
BP6 = [0,0,0,0,0,0,1,1,0,1,0,1,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,1,0,0,0,0,0,0,0]

Produto Escalar: 0
||F6|| = √(5) = 2.236
||BP6|| = √(6) = 2.000
Similaridade = 0 / (2.236 × 2.000) = 0.000
```

### Cálculo F7 × BP5
```
F7 = [0,1,0,1,1,1,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,0,0,0,0,0,0,0,0,0,0,1,0,0,1]
BP5 = [1,0,0,0,0,0,0,1,0,0,0,0,1,1,0,0,1,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0,0,1,0]

Produto Escalar: 0
||F7|| = √(7) = 2.646
||BP5|| = √(6) = 2.449
Similaridade = 0 / (2.646 × 2.449) = 0.000
```

### Cálculo F7 × BP6
```
F7 = [0,1,0,1,1,1,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,0,0,0,0,0,0,0,0,0,0,1,0,0,1]
BP6 = [0,0,0,0,0,0,1,1,0,1,0,1,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,1,0,0,0,0,0,0,0]

Produto Escalar: 0
||F7|| = √(7) = 2.646
||BP6|| = √(6) = 2.000
Similaridade = 0 / (2.646 × 2.000) = 0.000
```

### Cálculo F8 × BP5
```
F8 = [0,0,0,0,0,0,1,1,0,0,1,0,0,0,0,0,1,1,0,0,1,1,1,0,0,0,1,0,1,0,1,0,0,0,0]
BP5 = [1,0,0,0,0,0,0,1,0,0,0,0,1,1,0,0,1,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0,0,1,0]

Produto Escalar: 0×1 + 1×1 + 1×1 = 1
||F8|| = √(8) = 2.828
||BP5|| = √(6) = 2.449
Similaridade = 1 / (2.828 × 2.449) = 0.144
```

### Cálculo F8 × BP6
```
F8 = [0,0,0,0,0,0,1,1,0,0,1,0,0,0,0,0,1,1,0,0,1,1,1,0,0,0,1,0,1,0,1,0,0,0,0]
BP6 = [0,0,0,0,0,0,1,1,0,1,0,1,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,1,0,0,0,0,0,0,0]

Produto Escalar: 1×1 + 1×1 = 2
||F8|| = √(8) = 2.828
||BP6|| = √(6) = 2.000
Similaridade = 2 / (2.828 × 2.000) = 0.354
```

---

## Etapa 4: Resultados das Similaridades

| Comparação | Produto Escalar (A·B) | \\|A\\| (Norma A) | \\|B\\| (Norma B) | \\|A\\| × \\|B\\| | Similaridade cos(θ) | Classificação |
|------------|----------------------|-------------------|-------------------|-------------------|---------------------|---------------|
| **F6 × BP5** | 3 | 2.236 | 2.449 | 5.477 | **0.548** | Média |
| **F6 × BP6** | 0 | 2.236 | 2.000 | 4.472 | **0.000** | Muito Baixa |
| **F7 × BP5** | 0 | 2.646 | 2.449 | 6.482 | **0.000** | Muito Baixa |
| **F7 × BP6** | 0 | 2.646 | 2.000 | 5.292 | **0.000** | Muito Baixa |
| **F8 × BP5** | 1 | 2.828 | 2.449 | 6.928 | **0.144** | Baixa |
| **F8 × BP6** | 2 | 2.828 | 2.000 | 5.657 | **0.354** | Média |

---

## Etapa 5: Interpretação dos Resultados

### Frase com MENOR Similaridade (Mais Problemática)

**F7:** "Usuários com deficiência visual não conseguem acessar o conteúdo."

- **Similaridade com BP5:** 0.000
- **Similaridade com BP6:** 0.000  
- **Média de Similaridade:** 0.000

#### Por que F7 é a mais problemática?
1. **Linguagem Capacitista:** Usa "deficiência" sem abordagem pessoa-primeiro
2. **Foco no Problema:** Apenas identifica limitações, não sugere soluções
3. **Tom Negativo:** "não conseguem" é uma abordagem limitante
4. **Falta de Vocabulário Inclusivo:** Não compartilha termos-chave com as boas práticas
5. **Ausência de Palavras de Ação:** Não possui verbos que indiquem melhorias

### Frase com MAIOR Similaridade (Menos Problemática)

**F6:** "Esse vídeo não possui legenda nem intérprete de Libras."

- **Similaridade com BP5:** 0.548
- **Similaridade com BP6:** 0.000
- **Média de Similaridade:** 0.274

#### Por que F6 é menos problemática?
1. **Vocabulário Compartilhado:** Possui termos como "legenda", "interprete", "libras"
2. **Contexto Específico:** Foca em elementos técnicos concretos
3. **Linguagem Neutra:** Não usa termos capacitistas diretos

---

## Ranking das Frases (da mais problemática para a menos)

| Posição | Frase | Média de Similaridade | Status | Prioridade |
|---------|-------|----------------------|--------|------------|
| 1º      | **F7** | 0.000 | Extremamente problemática | **Crítica** |
| 2º      | **F8** | 0.249 | Muito problemática | Alta |
| 3º      | **F6** | 0.274 | Problemática | Média |

---

## Análise Aprofundada e Recomendações

### Análise da Frase Mais Problemática (F7)

#### Problemas Identificados:
- **Linguagem Capacitista:** "deficiência visual" 
- **Abordagem Negativa:** "não conseguem"
- **Falta de Soluções:** Apenas aponta o problema
- **Vocabulário Excludente:** Zero intersecção com boas práticas

#### Proposta de Melhoria:
```diff
- Versão Original: "Usuários com deficiência visual não conseguem acessar o conteúdo."
+ Versão Melhorada: "Garanta descrição de imagens e leitura por leitores de tela para usuários com deficiência visual."
```

#### Impacto da Melhoria:
- **Nova Similaridade com BP6:** ~0.750 (estimativa)
- **Palavras adicionadas:** garanta, descrição, imagens, leitura, leitores, tela
- **Tom:** De problema → solução

---

## 📈 Extras: Análise Estatística Avançada

### Matriz de Confusão das Similaridades

| Frase | BP5 | BP6 | Média | Status |
|-------|-----|-----|-------|--------|
| **F6** | 0.548 | 0.000 | 0.274 | ⚠️ Atenção |
| **F7** | 0.000 | 0.000 | 0.000 | 🔴 Crítico |
| **F8** | 0.144 | 0.354 | 0.249 | ⚠️ Atenção |

### Estatísticas Descritivas

| Métrica | Valor |
|---------|-------|
| **Média Geral** | 0.174 |
| **Desvio Padrão** | 0.195 |
| **Mediana** | 0.144 |
| **Coeficiente de Variação** | 104.8% |
| **Quartil Inferior (Q1)** | 0.000 |
| **Quartil Superior (Q3)** | 0.354 |
| **Amplitude** | 0.548 |

### Distribuição por Classificação

```
🔴 Similaridade Muito Baixa (0.000): 66.7% (4/6 comparações)
🟡 Similaridade Média (0.300-0.600): 33.3% (2/6 comparações)
🟢 Similaridade Alta (>0.600): 0% (0/6 comparações)
```

---

## 🚀 Aplicações Práticas na Engenharia de Software

### 1. Sistema de Alertas Automatizado
```python
def classify_accessibility_risk(similarity_score):
    if similarity_score < 0.3:
        return "CRÍTICO - Revisão Imediata"
    elif similarity_score < 0.6:
        return "ATENÇÃO - Revisão Recomendada"
    else:
        return "OK - Dentro dos Padrões"
```

### 2. Pipeline de Validação de Conteúdo
- **Input:** Texto novo inserido no sistema
- **Processamento:** Vetorização e cálculo de similaridade
- **Output:** Score de acessibilidade e sugestões de melhoria

### 3. Métricas de Qualidade
- **KPI:** Percentual de conteúdos com similaridade > 0.6
- **Meta:** 95% dos conteúdos aprovados
- **Monitoramento:** Dashboard em tempo real

---

## 🎯 Conclusões Técnicas

### Resposta à Pergunta Principal
**Qual frase foi a pior e por quê?**

A frase **F7** ("Usuários com deficiência visual não conseguem acessar o conteúdo") é inequivocamente a mais problemática, com similaridade **0.000** com ambas as boas práticas.

### Justificativas Técnicas:

1. **Análise Vetorial:** F7 não possui intersecção de vocabulário com nenhuma boa prática
2. **Análise Semântica:** Linguagem focada em limitações ao invés de soluções
3. **Análise de Impacto:** Reforça estereótipos negativos sobre acessibilidade

### Recomendações para o Sistema:

1. **Implementar filtros automáticos** para similaridade < 0.3
2. **Criar biblioteca de termos inclusivos** para sugestões automáticas
3. **Desenvolver sistema de scoring** baseado em similaridade de cosseno
4. **Integrar com ferramentas de revisão** de conteúdo corporativo

---

## 📚 Metodologia Aplicada

### Pré-processamento de Texto:
1. Normalização (minúsculas, sem acentos)
2. Tokenização por palavras
3. Remoção de stop words básicas
4. Construção do vocabulário único

### Vetorização:
- **Método:** Term Frequency (TF)
- **Dimensionalidade:** 35 features
- **Esparsidade:** Alta (muitos zeros)

### Cálculo de Similaridade:
- **Algoritmo:** Similaridade de Cosseno
- **Complexidade:** O(n) por comparação
- **Interpretação:** [0,1] onde 1 = máxima similaridade

---

## Resultados Finais

| Métrica | Resultado |
|---------|-----------|
| **Frase Mais Problemática** | F7 (similaridade média: 0.000) |
| **Frase Menos Problemática** | F6 (similaridade média: 0.274) |
| **Maior Similaridade Individual** | F6 × BP5 (0.548) |
| **Vocabulário Único** | 35 palavras |
| **Total de Comparações** | 6 análises |

