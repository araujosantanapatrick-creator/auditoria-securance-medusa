# Reconhecimento e enumeração

> Resultados descritos neste documento são simulados.

## Objetivo
Identificar hosts e serviços presentes no escopo autorizado antes de avaliar controles de autenticação.

## Comando demonstrativo

```bash
nmap -sV -sC -p 21,80,139,445 192.168.56.102
```

## Interpretação
- Porta 21: normalmente associada a FTP.
- Porta 80: normalmente associada a HTTP.
- Portas 139 e 445: normalmente associadas a serviços SMB/NetBIOS.

A presença de uma porta aberta não prova, por si só, que exista uma vulnerabilidade. É necessário identificar versão, configuração, exposição e controles compensatórios.

## Registro simulado
O cenário considera FTP, HTTP e SMB disponíveis no host de laboratório. Essa informação é fictícia e não foi coletada por uma varredura real.
