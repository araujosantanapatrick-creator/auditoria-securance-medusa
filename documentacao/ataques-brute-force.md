# Avaliação de autenticação — FTP, DVWA e SMB

> Este é um roteiro didático. Os resultados são fictícios; não houve execução real.

## FTP com Medusa
Exemplo de sintaxe para conta descartável em rede isolada:

```bash
medusa -h 192.168.56.102 -u labuser -P ./wordlists/senhas-teste.txt -M ftp -t 2
```

Ajustar a sintaxe à versão do Medusa e confirmar o módulo disponível com a documentação local. Usar apenas lista curta de senhas artificiais e conta criada exclusivamente para o laboratório.

## DVWA
O teste web depende do formulário, do método HTTP, dos nomes dos campos, dos cookies e de eventuais tokens CSRF. Registrar manualmente a configuração do módulo de força bruta, o nível de segurança e as proteções observadas. Não presumir que um comando genérico de ferramenta funcionará em qualquer formulário.

## SMB / password spraying
Password spraying é a avaliação de uma senha de teste contra um conjunto pequeno de contas fictícias. A finalidade defensiva é verificar política de senhas, limitação de tentativas, bloqueio, registro de eventos e exposição desnecessária de contas.

## Cuidados
- Escopo restrito a laboratório próprio.
- Contas e senhas descartáveis.
- Baixa taxa de tentativas.
- Interrupção imediata diante de instabilidade.
- Nunca testar credenciais reais ou reutilizadas.
