# Projeto de Rede Corporativa para a "Empresa Pastelinho"

<p align="center">
  <img src="https://img.shields.io/badge/Categoria-Projeto%20Académico-blue">
  <img src="https://img.shields.io/badge/Plataforma-GNS3-E9413A?logo=gns3">
  <img src="https://img.shields.io/badge/Equipamento-Cisco-1BA0D7?logo=cisco">
</p>

> [Projeto Académico] Projeto de uma rede corporativa para a empresa "Pastelinho", usando GNS3 para simular e configurar routers Cisco com OSPF, DHCP e NAT. Desenvolvido para a UC de Arquitetura e Protocolos de Comunicação (APC ) do CTeSP de IEA na ESTGA - Universidade de Aveiro.

---

## Índice

- O Desafio e o Contexto Académico
- Arquitetura da Rede: Topologia e Planeamento
- Implementação Técnica: Configuração de Dispositivos
- Testes e Validação do Funcionamento
- Conclusão e Aprendizagens
- Ficheiros de Configuração e Simulação
- Licença

---

### 1. O Desafio e o Contexto Académico

Este projeto foi desenvolvido no âmbito da unidade curricular **Arquitetura e Protocolos de Comunicação (APC)**, integrada no Curso Técnico Superior Profissional em Instalações Elétricas e Automação (CTeSP de IEA) da ESTGA - Universidade de Aveiro, no ano 2023.

O objetivo era projetar, simular e configurar a rede informática completa para a fictícia "Empresa Pastelinho", com base num enunciado técnico específico, utilizando o simulador **GNS3**. O desafio consistia em interligar três departamentos (Engenharia, Comercial e Datacenter) com redes públicas e privadas distintas, implementar serviços essenciais como DHCP, OSPF, NAT e servidores HTTP, e garantir a conectividade interna e externa, tudo através da configuração via linha de comandos (CLI) de equipamentos Cisco.

### 2. Arquitetura da Rede: Topologia e Planeamento

A solução proposta seguiu uma topologia hierárquica. Cada departamento foi ligado a uma rede de distribuição central (`172.109.7.0/24`), que, por sua vez, se conectava a um router ISP simulado, proporcionando acesso à Internet.

#### Planeamento de Sub-redes

| Departamento | Rede | Endereço de Rede | Tipo | Hosts |
| :--- | :--- | :--- | :--- | :---: |
| **Engenharia** | `staff_engenharia` | `109.4.38.0/25` | Pública | 126 |
| | `guest_engenharia` | `172.109.38.0/24` | Privada | 254 |
| **Comercial** | `staff_comercial` | `109.4.38.128/26` | Pública | 62 |
| | `guest_comercial` | `172.109.4.0/24` | Privada | 254 |
| **Datacenter** | `datacenter` | `109.4.38.192/27` | Pública | 30 |
| **Distribuição** | `rede_dist` | `172.109.7.0/24` | Privada | 254 |

O dimensionamento das máscaras de sub-rede (`/25`, `/26`, `/27`) foi calculado para satisfazer o número mínimo de hosts exigido em cada segmento, otimizando o espaço de endereçamento.

### 3. Implementação Técnica: Configuração de Dispositivos

A configuração foi realizada integralmente através da CLI (Command Line Interface) no GNS3.

#### 3.1 Configuração de Roteadores e Endereçamento Estático
Cada interface dos routers foi configurada com um endereço IP estático, atuando como gateway para a sua rede.
*Exemplo: Router Comercial*

```cisco
! interface FastEthernet0/0 (staff_comercial)
interface FastEthernet0/0
 ip address 109.4.38.129 255.255.255.192
 no shutdown

! interface FastEthernet0/1 (guest_comercial)
interface FastEthernet0/1
 ip address 172.109.4.1 255.255.255.0
 no shutdown

! interface FastEthernet1/0 (distribuição)
interface FastEthernet1/0
 ip address 172.109.7.1 255.255.255.0
 no shutdown
```

#### 3.2 Implementação de Serviços DHCP
Os pools DHCP foram configurados nos próprios routers de departamento para simplificar a gestão.
Exemplo: Pool no Router Engenharia

```cisco
ip dhcp pool staff_engenharia
 network 109.4.38.0 255.255.255.128
 default-router 109.4.38.1
 lease infinite
```

#### 3.3 Protocolo de Encaminhamento OSPF
O protocolo OSPF foi configurado em todos os routers para partilhar rotas dinamicamente dentro da rede interna. Todas as interfaces foram anunciadas na Área 0. O router ISP foi configurado como origem da rota padrão (default-information originate).

```cisco
router ospf 1
 network 172.109.7.0 0.0.0.255 area 0
 network 109.4.38.0 0.0.0.127 area 0
```
#### 3.4 Network Address Translation (NAT)
No router ISP, foi configurado NAT Overload (PAT) para traduzir todos os endereços das redes privadas para o único endereço IP público da interface externa (FastEthernet0/1), permitindo o acesso à Internet.

```cisco
! Definir a lista de acesso para as redes internas a serem traduzidas
access-list 1 permit 172.109.4.0 0.0.0.255
access-list 1 permit 172.109.38.0 0.0.0.255
access-list 1 permit 172.109.7.0 0.0.0.255

! Aplicar NAT Overload na interface de saída
ip nat inside source list 1 interface FastEthernet0/1 overload
```
#### 3.5 Servidores Web (HTTP)
Inicialmente, os servidores foram configurados dentro da rede usando ip http server num router Cisco. No entanto, devido a dificuldades com a NAT, a solução final optou por usar máquinas Debian com Apache2, conectadas à rede externa simulada.
Configuração no servidor Debian
```cisco
sudo apt install apache2
sudo systemctl start apache2
sudo systemctl enable apache2
```
### 4. Testes e Validação do Funcionamento
A rede foi exaustivamente testada para garantir o cumprimento de todos os requisitos:
- Conectividade Interna: Utilizando o comando ping, foi verificada a comunicação bem-sucedida entre hosts de diferentes sub-redes (ex: PC em guest_engenharia para servidor no datacenter ), comprovando o correto encaminhamento pelo OSPF.
- DHCP: Todos os PCs obtiveram automaticamente um endereço IP, máscara e gateway da pool correta.
- NAT e Acesso Externo: A partir de um PC numa rede privada, foi possível fazer ping a um endereço IP público externo (ex: 8.8.8.8), confirmando a tradução de endereços.
- Serviços HTTP: As páginas web dos servidores foram acessíveis a partir de um browser dentro da simulação.
- Análise com Wireshark: O Wireshark, integrado no GNS3, foi utilizado para analisar o tráfego, confirmar o funcionamento da NAT e diagnosticar pacotes mal formados durante a fase de depuração.
### 5. Conclusão e Aprendizagens
Este projeto foi um exercício prático abrangente que consolidou o conhecimento em arquitetura de redes. Partindo da teoria, foi possível:
- Projetar uma topologia lógica e eficiente.
- Configurar dispositivos de rede reais (simulados) via CLI.
- Integrar múltiplos protocolos (OSPF, DHCP, NAT, HTTP) para criar uma rede funcional.
- Testar e resolver problemas de conectividade, utilizando ferramentas como ping, traceroute e Wireshark.

O principal desafio e aprendizagem foi a implementação da NAT e a compreensão do fluxo de pacotes entre redes públicas e privadas. A necessidade de adaptar a solução inicial para os servidores web também destacou a importância da praticabilidade e do troubleshooting em engenharia de redes. Este trabalho forneceu uma base sólida e prática para compreender a complexidade e a interdependência dos elementos que constituem uma infraestrutura de rede corporativa moderna.

### 6. Ficheiros de Configuração e Simulação
Ficheiros de Configuração: Os códigos completos para cada dispositivo de rede estão disponíveis na pasta configs/.
Ficheiro de Simulação GNS3: O ficheiro do projeto GNS3 (.gns3) e a sua estrutura de pastas associada estão disponíveis para download na secção de Releases deste repositório.

### 7. Licença
Este projeto está licenciado sob a MIT License. Veja o ficheiro LICENSE para mais detalhes.
