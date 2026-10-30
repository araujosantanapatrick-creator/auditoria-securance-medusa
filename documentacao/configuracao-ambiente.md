# Configuração do ambiente — cenário proposto

> Documento de planejamento. As configurações abaixo descrevem um laboratório hipotético; não confirmam instalação ou execução.

## Componentes
- VirtualBox como hipervisor.
- Kali Linux como estação de auditoria.
- Metasploitable 2 como alvo vulnerável.
- DVWA como aplicação web de treinamento.
- Adaptadores de rede configurados em Host-only.

## Isolamento
A rede Host-only permite comunicação entre o host e as VMs sem expor diretamente os serviços vulneráveis à rede física. Para este exercício, não configurar encaminhamento de portas nem uma segunda interface em modo Bridge. Se for necessário baixar atualizações, fazê-lo de forma controlada e desligar a interface externa antes dos testes.

## Endereçamento ilustrativo
- Kali Linux: `192.168.56.101`
- Metasploitable 2: `192.168.56.102`

Os endereços devem ser confirmados na instalação real por meio das ferramentas de rede do sistema. Não assumir que o VirtualBox atribuirá necessariamente esses endereços.
