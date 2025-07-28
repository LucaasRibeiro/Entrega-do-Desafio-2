# Entrega-do-Desafio-FInal-Modulo-1

Relatório Técnico – Avaliação de Segurança Interna

Autor: Lucas Ribeiro Gomes da Silva  
Data: 28/07/2025  
Versão: v1.0

# 1\. Sumário Executivo

Durante a análise da rede interna da fictícia empresa Zé Corp, foram identificadas três vulnerabilidades críticas:  
\- Servidor SMB com acesso anônimo (porta 445);  
\- Protocolo SNMP exposto com community string padrão (public);  
\- Serviço HTTP exposto sem autenticação interna.  
Recomendamos isolar os ativos vulneráveis, aplicar correções e reforçar as políticas de controle de acesso.

# 2\. Objetivo

Avaliar os principais serviços expostos na rede interna da empresa Zé Corp, identificando riscos de segurança e propondo ações corretivas.

# 3\. Escopo e Contexto

A análise foi realizada sobre a rede interna 192.168.0.0/24. O escopo incluiu servidores Windows/Linux, dispositivos de rede e serviços TCP/UDP ativos.  
Ficaram fora do escopo os serviços em nuvem e redes Wi-Fi de visitantes.

# 4\. Metodologia

Ferramentas utilizadas: nmap, enum4linux-ng, snmpwalk, Wireshark.  
Etapas:  
\- Coleta de dados de rede (IP, portas, serviços);  
\- Enumeração de protocolos vulneráveis (SMB, SNMP);  
\- Análise de exposição e risco baseada em MITRE ATT&CK.  
A análise buscou evidências técnicas para suportar as conclusões.

# 5\. Diagnóstico Técnico (Achados)

| Achado | Evidência | Impacto |
| --- | --- | --- |
| SMB com acesso anônimo | enum4linux-ng revelou compartilhamentos acessíveis sem autenticação | Exposição de dados sensíveis, risco de ransomware |
| SNMP com string "public" | snmpwalk retornou dados do sistema, versão do OS e configurações de rede | Facilita reconhecimento e exploração da infraestrutura |
| HTTP sem autenticação | Serviço na porta 8080 expõe painel administrativo sem login | Possível controle não autorizado do sistema interno |

# 6\. Recomendações Técnicas

\- Restringir o acesso SMB com autenticação obrigatória e política de senha forte;  
\- Substituir a community string SNMP padrão por valores seguros e segmentar IPs com acesso;  
\- Implementar autenticação no serviço HTTP e limitar IPs permitidos via firewall.

# 7\. Plano de Ação (80/20)

| Ação | Impacto | Facilidade | Prioridade |
| --- | --- | --- | --- |
| Aplicar autenticação no SMB | Alto | Alta | Alta |
| Trocar community string SNMP | Médio | Alta | Alta |
| Configurar autenticação HTTP | Médio | Média | Média |

# 8\. Conclusão

A análise identificou brechas significativas na rede interna da ACME Corp que podem comprometer a integridade e confidencialidade de dados.  
As recomendações aplicadas trarão melhorias imediatas à postura de segurança. Recomendamos reavaliação após 30 dias.

nmap -sV -Pn 192.168.0.0/24
enum4linux-ng -A 192.168.0.10
snmpwalk -v 2c -c public 192.168.0.15

# 9\. Anexos

**Diagrama Red Team completo com:**

1. **Internet + Kali Linux (máquina atacante)**
2. **Firewall protegendo a rede**
3. **DMZ com Web Server vulnerável**
4. **Rede interna com:**
    - Servidor SMB com acesso anônimo
    - Servidor SNMP com string "public"
5. **Fases da Cyber Kill Chain (Reconnaissance → Exploitation → Pivot)**
6. **Setas bem visíveis e organização lógica**
