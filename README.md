# DevSecOps Pipeline - VAmPI
Este projeto demonstra a implementação de uma esteira de DevSecOps utilizando o ecossistema GitHub Actions. A aplicação alvo é o VAmPI (Vulnerable API), uma API baseada em Flask que contém vulnerabilidades de segurança reais para fins de estudo e testes.

# Objetivo
O objetivo desta pipeline é identificar vulnerabilidades em diferentes estágios do desenvolvimento (estático e dinâmico), impedindo que falhas críticas cheguem a ambientes de produção e automatizando a documentação de riscos através de Issues no GitHub.

# Ferramentas e Processo de Implementação
A pipeline está dividida em camadas de segurança complementares:

1. **SAST (Static Application Security Testing)**
Ferramenta: Semgrep

Finalidade: Analisa o código-fonte em busca de padrões de código inseguros sem a necessidade de executar a aplicação.

Implementação: Utiliza regras de security-audit e boas práticas para python.

Varre o código em busca de segredos expostos, configurações de segurança fracas e uso de funções perigosas.

2. **DAST (Dynamic Application Security Testing)**
Ferramenta: OWASP ZAP (Baseline Scan)

Finalidade: Analisa a aplicação em tempo de execução, simulando ataques externos para encontrar vulnerabilidades que só aparecem com o serviço ativo.

Implementação:

A API é subida via Docker dentro do Runner do GitHub.

O ZAP realiza um scan de linha de base (Baseline) contra o `http://localhost:5000`.

Gestão de Falsos Positivos: Utilizamos um arquivo de configuração em `.zap/rules.tsv` para ignorar alertas de baixo risco ou informativos, focando no que é relevante.

3. **Gestão de Vulnerabilidades**
GitHub Issues: A pipeline está configurada para criar automaticamente uma Issue no repositório sempre que o scan de segurança encontrar alertas novos. Isso garante a rastreabilidade e obriga a correção (Remediação) das falhas encontradas.

# Como Executar
**Pré-requisitos:**
Para que a pipeline funcione corretamente, é necessário configurar as permissões de escrita do `GITHUB_TOKEN`:

**Estrutura de Regras (ZAP)**
Para personalizar quais alertas devem ser ignorados ou notificados, edite o arquivo: `.zap/rules.tsv`

**Execução**
A pipeline é disparada automaticamente em cada push ou pull_request para a branch main.

# Próximos Passos
- Integrar SCA (Software Composition Analysis) com Trivy ou Snyk para analisar vulnerabilidades em bibliotecas de terceiros.
- Implementar Análise de Imagem Docker para verificar vulnerabilidades no sistema operacional base do container.

___

> Desenvolvido para fins educacionais de Segurança de Aplicações.