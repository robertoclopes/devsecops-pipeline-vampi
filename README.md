# VAmPI: Secure SDLC Lab
## Finalidade
Este repositório é uma demonstração de uma Paved Road de segurança aplicada a uma API vulnerável. O objetivo é interceptar falhas do OWASP Top 10:2025 (como A01: Broken Access Control e A03: Supply Chain Failures) antes que cheguem em produção.

## Processo de Implementação
SAST (Static Application Security Testing): Utilizou-se o Semgrep para análise de código. Ele busca por vulnerabilidades como injeção de SQL e segredos hardcoded.

DAST (Dynamic Application Security Testing): Utilizou-se o OWASP ZAP para testar a aplicação em runtime. O pipeline sobe um container Docker do VAmPI e realiza ataques de caixa-preta contra os endpoints.

## Observabilidade
Os resultados são consolidados no Security Tab do GitHub.

## Trade-offs
Segurança vs. Velocidade: O ZAP Baseline foi escolhido em vez do Full Scan para manter o pipeline abaixo de 5 minutos, garantindo uma boa experiência do desenvolvedor.