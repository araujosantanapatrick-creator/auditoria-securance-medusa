# Recomendações de mitigação

## FTP
- Preferir SFTP ou FTPS; desabilitar FTP sem criptografia quando possível.
- Restringir o acesso por firewall e segmentação.
- Remover contas padrão e exigir credenciais fortes.
- Monitorar falhas e acessos fora do padrão.

## DVWA / aplicações web
- Aplicar limitação de tentativas e atraso progressivo.
- Implementar MFA quando aplicável.
- Proteger sessões e tokens anti-CSRF.
- Evitar mensagens que revelem a existência de usuários.
- Registrar e alertar sobre padrões anormais de autenticação.

## SMB
- Restringir portas 139/445 aos segmentos necessários.
- Desabilitar SMBv1 quando não houver dependência legada.
- Remover contas inativas e revisar permissões de compartilhamento.
- Exigir senhas fortes e MFA onde houver suporte.
- Monitorar falhas repetidas e tentativas contra múltiplas contas.

## Governança
- Manter inventário de ativos e serviços.
- Definir escopo e autorização antes dos testes.
- Centralizar logs, sincronizar horários e revisar alertas.
- Repetir avaliações após correções para verificar sua eficácia.
