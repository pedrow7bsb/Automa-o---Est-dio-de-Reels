# 🎬 Estúdio de Reels: Orquestração e Edição Automatizada de Vídeos por IA

**Resumo Executivo:** Este repositório documenta a arquitetura de um pipeline de automação para edição de vídeos curtos (Reels). O sistema orquestra agentes de Inteligência Artificial para transformar vídeos brutos em material renderizado e finalizado, eliminando o trabalho braçal de edição manual e garantindo um padrão visual consistente em escala. 

*(Nota: O código fonte deste projeto é mantido privado por conter dados sensíveis e pessoais de clientes. Esta página detalha a engenharia, os processos de decisão e a arquitetura do agente.)*

---

## 🚩 O Desafio Operacional
A edição tradicional de vídeos curtos apresenta dois gargalos críticos para criadores e empresas:
1. **Tempo de Execução:** O processo de decupagem, cortes, legendagem e inserção de animações consome horas de trabalho manual por cada minuto de vídeo.
2. **Inconsistência Visual:** O resultado final varia drasticamente dependendo do fluxo de trabalho humano, dificultando a manutenção de uma identidade de marca sólida.

## 💡 A Arquitetura da Solução (Fluxo do Agente)

O sistema foi desenhado para processar o vídeo de forma autônoma com um loop de aprovação integrado, garantindo que o resultado ("Reel final") saia "igual toda vez"[cite: 4].

<img width="1886" height="584" alt="image" src="https://github.com/user-attachments/assets/23294f40-51bb-46ce-83bd-077eb81efc97" />


1. **Entrada e Triagem:** O sistema recebe o **Vídeo Bruto** (gravação do dia) e cruza com um banco de **Referências** (dados de estilo previamente aprendidos). O agente de **Triagem e Ficha** analisa o conteúdo falado ("o que o vídeo diz")[cite: 4].
2. **Roteirização Automática:** O agente de **Batidas** transforma essa análise em um roteiro de edição estruturado[cite: 4].
3. **Loop de Qualidade (Human/Agent-in-the-loop):** Uma etapa de decisão avalia se a **"Amostra está ok?"**[cite: 4]. Se reprovada, retorna para reajuste nas batidas. Se aprovada, aciona processos paralelos[cite: 4].
4. **Processamento Especializado (Serviços Paralelos):**
   * **Corte e Legenda:** Aplicação hierárquica de textos no vídeo[cite: 4].
   * **Cena por IA:** Geração de imagens suplementares quando o roteiro exige, mantendo a coerência visual do apresentador[cite: 4].
   * **Lettering e Motion:** Aplicação de variações visuais controladas[cite: 4].
5. **Renderização Determinística:** Os serviços convergem para o módulo de **Render**, construído com **Remotion** (renderização via código web), eliminando variáveis e entregando o arquivo final de forma programática e idêntica aos parâmetros aprovados[cite: 4].

---

## 📈 Metodologia de Desenvolvimento e Métricas
O projeto foi construído utilizando **Claude Code** sob rigorosos padrões de engenharia de software (Test-Driven Development - TDD). O ciclo adotado foi: elaboração da especificação (*spec*) → quebra em tarefas pequenas com critérios de aceite → testes escritos (vermelho) → implementação (verde) → execução da suíte completa.

* **Commit Log:** +270 commits documentados.
* **Confiabilidade:** +750 testes automatizados garantindo a integridade dos fluxos.
* **Especialização:** 18 *skills* (habilidades) especializadas desenvolvidas para os agentes.

---

## 🛡️ Princípios e Governança do Projeto

Para garantir a viabilidade comercial e a segurança da aplicação corporativa, o sistema opera sob três pilares:

* **Custo Previsível e Escalabilidade:** A infraestrutura roda integralmente em servidor próprio e serviços sob assinatura, erradicando a volatilidade de custos por chamadas de API avulsas.
* **Segurança e Isolamento (Zero Trust):**
  * Nenhum segredo ou credencial (*.env*) é versionado no repositório.
  * O acesso web é rigorosamente protegido por trás de camadas do **Cloudflare Access**.
  * **Proteção contra Prompt Injection:** Agentes possuem travas estritas de sistema que os proíbem de executar comandos ou alterar comportamentos com base no conteúdo falado do vídeo de entrada.
* **Rastreabilidade Total:** Toda decisão de arquitetura é documentada em um *Decision Log*, e cada alteração de esquema ou de base de dados gera automaticamente uma atualização no versionamento das especificações do projeto.
