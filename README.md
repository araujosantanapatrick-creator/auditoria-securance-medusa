# Auditoria de Segurança: Simulação de Ataques de Força Bruta com Kali Linux e Medusa

**Natureza do trabalho:** projeto prático de auditoria de segurança utilizando Kali Linux e Medusa.

O projeto contempla a configuração de um ambiente de laboratório, enumeração de serviços, identificação de vulnerabilidades e avaliação de mecanismos de autenticação nos protocolos FTP, HTTP e SMB.

São apresentados procedimentos técnicos, comandos utilizados, análise de segurança, identificação de riscos e recomendações de mitigação, incluindo políticas de senhas fortes, autenticação multifator (MFA), limitação de tentativas de acesso e monitoramento de eventos.

**Objetivo:** demonstrar conhecimentos em segurança ofensiva, testes de autenticação, análise de vulnerabilidades e aplicação de medidas de proteção em sistemas e serviços de rede.

## 1. Introdução

Este projeto apresenta um estudo controlado sobre enumeração de serviços e riscos associados a senhas fracas, com foco em FTP, autenticação web (DVWA) e SMB. O cenário didático considera o uso do Kali Linux como estação de auditoria e do Metasploitable 2 como alvo vulnerável, em conjunto com a aplicação DVWA.

O objetivo é demonstrar a compreensão do processo de auditoria: reconhecimento, enumeração, teste controlado de autenticação, análise dos resultados e proposição de medidas de mitigação.

## 2. Objetivos

- Compreender o funcionamento de tentativas automatizadas de autenticação.
- Identificar serviços expostos em um host de laboratório.
- Demonstrar, em cenário hipotético, os riscos de credenciais fracas e reutilizadas.
- Diferenciar força bruta de password spraying.
- Registrar resultados de maneira reproduzível e tecnicamente responsável.
- Recomendar controles preventivos e mecanismos de detecção.

## 3. Escopo e regras de segurança

O escopo proposto limita-se a máquinas virtuais próprias, em rede isolada e sem rota para redes externas. Nenhum endereço, serviço ou credencial de terceiros deve ser testado.

**Limites do estudo:**
- Não realizar tentativas contra sistemas públicos, corporativos ou de terceiros.
- Não utilizar credenciais reais.
- Usar listas pequenas e contas descartáveis no laboratório.
- Interromper os testes ao observar indisponibilidade ou bloqueio inesperado.
- Não publicar senhas, tokens ou dados pessoais.
- Os resultados deste repositório são simulados; nenhuma atividade de ataque é declarada como executada.

## 4. Arquitetura hipotética do laboratório

| Componente | Configuração didática |
|---|---|
| Hipervisor | Oracle VirtualBox |
| Rede | Host-only, sem encaminhamento para a rede externa |
| Estação de auditoria | Kali Linux |
| IP ilustrativo do Kali | `192.168.56.101` |
| Alvo vulnerável | Metasploitable 2 |
| IP ilustrativo do alvo | `192.168.56.102` |
| Aplicação web | DVWA em ambiente local de laboratório |
| Ferramentas | Nmap, Medusa e navegador |

Os IPs são exemplos fictícios. Em uma implantação real, devem ser substituídos pelos endereços efetivamente atribuídos pelo VirtualBox.

### Diagrama lógico

```text
             Rede Host-only (isolada)
        ┌────────────────────────────────┐
        │                                │
┌───────▼────────┐                ┌──────▼──────────┐
│ Kali Linux     │                │ Metasploitable 2│
│ 192.168.56.101 │                │ 192.168.56.102  │
│ Nmap / Medusa  │                │ FTP / SMB       │
└────────────────┘                └─────────────────┘
                                         │
                                         │ Serviço web
                                  ┌──────▼──────────┐
                                  │ DVWA            │
                                  │ aplicação local │
                                  └─────────────────┘
```

## 5. Metodologia

A sequência metodológica proposta é:

1. Preparar as VMs e confirmar o isolamento da rede.
2. Identificar o endereço do alvo no laboratório.
3. Fazer reconhecimento de portas e serviços.
4. Enumerar informações disponibilizadas pelos serviços.
5. Avaliar a resistência de autenticação em contas de teste.
6. Consolidar observações e resultados.
7. Recomendar controles de prevenção e detecção.

## 6. Reconhecimento e enumeração

Exemplo de comando Nmap para uso **somente no alvo próprio e isolado**:

```bash
nmap -sV -sC -p 21,80,139,445 192.168.56.102
```

- `-sV`: tenta identificar versões dos serviços.
- `-sC`: executa scripts padrão de enumeração do Nmap.
- `-p`: define as portas a verificar.

### Resultado ilustrativo (simulado)

| Porta | Serviço hipotético | Observação |
|---:|---|---|
| 21/tcp | FTP | Serviço disponível no cenário |
| 80/tcp | HTTP | Interface web/DVWA no cenário |
| 139/tcp | NetBIOS-SSN | Serviço relacionado a compartilhamento |
| 445/tcp | SMB | Serviço de compartilhamento |

Esta tabela não foi obtida por varredura real. É uma composição didática de serviços comumente encontrados em laboratórios vulneráveis.

## 7. Auditoria de autenticação FTP com Medusa

A força bruta testa várias combinações de credenciais para uma conta ou conjunto de contas. Em auditoria autorizada, listas pequenas e contas descartáveis ajudam a avaliar se políticas de senha e bloqueio estão funcionando.

Exemplo de sintaxe para um laboratório isolado, com usuário e lista de senhas **de teste**:

```bash
medusa -h 192.168.56.102 -u labuser -P ./wordlists/senhas-teste.txt -M ftp -t 2
```

O comando é apenas uma referência de sintaxe. A disponibilidade do módulo e o comportamento dependem da versão instalada do Medusa e da configuração do serviço FTP. Não execute fora de um laboratório próprio e autorizado.

### Resultado ilustrativo (simulado)

| Indicador | Valor fictício |
|---|---:|
| Conta de teste avaliada | `labuser` |
| Tentativas previstas na lista | 5 |
| Autenticações aceitas no cenário | 1 |
| Autenticações recusadas no cenário | 4 |
| Conclusão hipotética | A senha de teste seria fraca e precisaria ser substituída |

Nenhuma credencial real foi testada. A senha não é publicada neste projeto.

## 8. Avaliação do formulário web DVWA

O DVWA é uma aplicação deliberadamente vulnerável, destinada a treinamento em ambiente local. O cenário didático considera o módulo de força bruta da aplicação, configurado em nível de segurança baixo, com uma conta descartável.

Procedimento proposto:
1. Iniciar a aplicação DVWA localmente.
2. Confirmar que a URL pertence ao laboratório.
3. Criar/usar somente uma conta de teste.
4. Observar como a aplicação responde a credenciais incorretas.
5. Registrar se há atraso, limitação de tentativas, CAPTCHA ou bloqueio.
6. Repetir a avaliação após aplicar controles defensivos.

**Nota técnica:** a automação de formulários web depende dos parâmetros HTTP, cookies de sessão, tokens anti-CSRF e do mecanismo de autenticação da aplicação. Não há um comando Medusa universal que funcione em qualquer formulário. A ferramenta e o módulo precisam ser compatíveis com o formulário e seus parâmetros. Este estudo não declara ter realizado requisições reais contra o DVWA.

### Resultado ilustrativo (simulado)

| Indicador | Cenário sem controles | Cenário com controles |
|---|---:|---:|
| Tentativas demonstrativas | 10 | 10 |
| Respostas de falha | 9 | 10 |
| Acesso de teste hipotético | 1 | 0 |
| Limitação de tentativas | Não observada | Ativada |
| Registro de eventos | Básico | Completo |

Os números são fictícios e servem apenas para ilustrar a comparação. Não são medições de desempenho nem evidências de execução.

## 9. Password spraying e SMB

Password spraying consiste em testar uma senha comum contra várias contas, em vez de testar muitas senhas contra uma única conta. A técnica pode reduzir a chance de disparar certos bloqueios por conta, mas continua sendo uma atividade de alto risco e deve ser avaliada apenas com contas fictícias e autorização explícita.

No cenário proposto, a enumeração de usuários antecederia a avaliação de autenticação SMB. O objetivo defensivo é verificar se:
- contas desnecessárias estão habilitadas;
- existe política de senha robusta;
- há bloqueio ou limitação após falhas;
- eventos de autenticação são registrados e monitorados;
- o SMB está restrito aos hosts que realmente precisam dele.

### Resultado ilustrativo (simulado)

| Indicador | Valor fictício |
|---|---:|
| Contas de laboratório consideradas | 4 |
| Senha de teste avaliada | 1 |
| Contas que recusaram autenticação | 3 |
| Conta com credencial fraca no cenário | 1 |
| Recomendação | Remover/alterar credencial fraca e revisar política |

Este relatório não fornece uma lista de usuários reais nem afirma que houve enumeração ou autenticação efetiva.

## 10. Consolidação dos resultados simulados

| Área | Achado hipotético | Risco | Recomendação prioritária |
|---|---|---|---|
| FTP | Credencial de teste fraca | Acesso não autorizado | Desativar FTP quando possível; preferir SFTP/FTPS |
| DVWA | Formulário sem limitação suficiente | Tentativas automatizadas | Rate limiting, atraso progressivo e MFA quando aplicável |
| SMB | Conta de teste com senha fraca | Acesso a compartilhamentos | Senhas fortes, menor privilégio e restrição de SMB |
| Monitoramento | Registro insuficiente de falhas | Detecção tardia | Centralizar logs e criar alertas |

## 11. Medidas de mitigação

### Política de autenticação
- Exigir senhas longas, únicas e não reutilizadas.
- Implementar MFA nos serviços compatíveis.
- Desabilitar contas padrão, inativas ou desnecessárias.
- Utilizar bloqueio temporário ou limitação progressiva, evitando causar negação de serviço.

### Proteção de serviços
- Desabilitar FTP sem criptografia e preferir SFTP ou FTPS.
- Restringir SMB por firewall e segmentação de rede.
- Desabilitar SMBv1 quando não houver necessidade legada.
- Aplicar atualizações e remover serviços não utilizados.

### Aplicações web
- Implementar rate limiting por conta e por origem.
- Adotar atraso progressivo após falhas.
- Registrar falhas e sucessos de autenticação.
- Usar mensagens de erro que não revelem se o usuário existe.
- Proteger sessões e tokens anti-CSRF.

### Monitoramento
- Correlacionar várias falhas de autenticação em curto intervalo.
- Alertar para tentativas distribuídas contra várias contas.
- Preservar logs com horário sincronizado.
- Investigar padrões anormais sem expor credenciais nos registros.

## 12. Conclusão

O estudo de caso demonstra como reconhecimento, enumeração e avaliação de autenticação se relacionam em uma auditoria de segurança. A simulação evidencia que credenciais fracas, serviços desnecessários e ausência de controles contra tentativas repetidas podem aumentar a superfície de ataque.

A principal conclusão é que a prevenção depende de camadas complementares: políticas de identidade, restrição de serviços, atualização, segmentação de rede, monitoramento e resposta a incidentes.

**Limitação:** este repositório é um exercício documental com dados simulados. Para transformar o estudo em relatório de execução, seria necessário montar o laboratório, executar os procedimentos autorizados e substituir os exemplos pelas evidências reais coletadas.

## 13. Referências

- Kali Linux: https://www.kali.org/
- Medusa: http://www.foofus.net/jmk/medusa/medusa.html
- Nmap Reference Guide: https://nmap.org/book/
- DVWA: https://github.com/digininja/DVWA
- GitHub Markdown: https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github

## 14. Aviso de uso

Material exclusivamente educacional. Qualquer teste de segurança deve ocorrer em ativos próprios ou mediante autorização expressa, dentro de escopo definido. Os dados e resultados apresentados são fictícios.
